---
title: Software Testing
---

# About Unit Testing

Simple test creation process:
- Test after
- Test during
- Test Driven Development

---

For test driven development, this is a good paradigm to follow:

- Create a testing outline
- Write most basic code to pass test
- Refactor
- Commit

Repeat until satified or code exceeds expectations.

 
 
## API Testing with Alba
 
Alba is a library that you can use to help with unit testing.
It can work with things like xUnit.Net to test APIs on .NET Core (using HTTP).
The following piece of code is doing three main things:
- Looks for the "host", aka the project where we defined `Program` and setup the API.
- Runs a scenario to get the API URL (which was configured in the `Program` project to return a value).
- Checks that API return code was 200 OK.

```csharp
 
using Alba;
 
namespace HelpDesk.Tests.Software;
public class GettingSoftware
{
    // Test that we can make an HTTP GET requests to /api/software
 
    [Fact]
    public async Task CanGetSoftware()
    {
        var host = await AlbaHost.For<Program>();
 
        await host.Scenario(api =>
        {
            api.Get.Url("/api/software");
            api.StatusCodeShouldBeOk();
        });
 
 
    }
}
```