---
title: Good Code and More TDD
---


## Good Code

Good code can be a multitude of things.
In general, good code is testable, easy to understand, easy to maintain/edit which means it is easy to understand. It should also work well and is efficient.

> Testing is easy in the presence of good code.

Good code is not necessarily done through BDUF (Big Design Up Front, which is relevant to the waterfall method).
This is because using TDD and multiple iterations of code helps get you to good code. Initially, the code may not be good, but it does its job and can be implemented. As time goes on, the edits eventually make the code good while still working.


Here is an example of the iterations

```csharp

// req 1
public int Add(string numbers)
{
    return 0;
}

// req 2
public int Add(string numbers)
{
    if (numbers == "") return 0;

    return int.Parse(numbers);
}

// req 3
public int Add(string numbers)
{
    if (numbers == "") return 0;

    if (numbers.Contains(','))
    {
        var nums = numbers.Split(',');
        var total = 0;
        for (int i = 0; i < nums.Length(); i++) 
        {
            total += nums[i];
        }
        return total;
    }

    return int.Parse(numbers);
}

```

As the code implements more and more requirements, it starts to get better.

## Notes on unit testing
Some failures in your tests may be external and not under your control. In general, unit test cannot access
- File system
- Database
- Network
- Clock
- Etc. (external things)
