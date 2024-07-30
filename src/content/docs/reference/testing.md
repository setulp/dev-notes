---
title: Software Testing
---

# About Unit Testing

Simple test creation process:
- Test after
- 
- Test Driven Development


For test driven development
...
 
 
# API Testing with Alba
 
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
 
Write what you understand about this code. What is Alba? Where did that come from? What is `Program`?