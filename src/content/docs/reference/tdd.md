---
title: Test Driven Development
---

# More about TDD

See `Software Testing` for overview.

## Test Driven Development (TDD)

For teams, there are many methods for development. Agile is a common one.
A popular method in the past was Waterfall.
This is where Requirments, Design, Coding, Testing, Stablization, and Push to Production are done one after another with no communication (most of the time) between them.
This usually ended in long lead times and a lot of wasted code. People have adopted Agile because it follows a code and get feedback and then code again paradigm.
This is similarly used in TDD, where you write meaningful test first and then write the code that can pass the test. After that, you edit the code to be better.
For example, in some cases we needed a bonus calculator but in other we didn't, thus this interface was born:

```csharp
// needs calc
var stubbedCalulator = Substitute.For<ICalculateBonuses>();
stubbedCalulator.CalculateBonusForDepositOn(7000M, 100M).Returns(42.69M);

// doesn't need calc
var account = new Account(new DummyBonusCalculator());

public class StandaredBonusCalculator
{
    [Fact]
    public void GivesBonusToAccountsWithSufficientBalance()
    {
        var bonusCalculator = new BonusCalculator();
        decimal balance = 5000M;
        decimal amountToDeposit = 100M;

        decimal bonus = bonusCalculator.CalculateBonusForDepositOn(balance, amountToDeposit);

        Assert.Equal(10M, bonus);
    }
}

public class DummyBonusCalculator : ICalculateBonuses
{
    public decimal CalculateBonusForDepositOn(decimal currentBalance, decimal amount)
    {
        return 0;
    }
}
```

Another example is the need to switch from using the `Currency` metaphor to using `TransactionAmount`.
This was needed because we didn't want a zero to be a value amount.

```csharp
private static bool ArgsAreValid(uint dollars, uint cents)
{

    if (dollars == 0)
    {
        if (cents <= 0)
        {
            return false;
        }
    }

    if (cents > 99)
    {
        return false;
    }
    if (dollars == 0 && cents == 0)
    {
        return false;
    }
    return true;


}

public static TransactionAmount FromUsd(uint dollars, uint cents)
{
    if (ArgsAreValid(dollars, cents))
    {
        return new TransactionAmount(dollars, cents, "USD");
    }
    else
    {
        throw new InvalidCurrencyException();
    }
}
```


## Method/Operator Overloading

Methods can be overloaded to use multiple types of variables. This is useful since you cannot change the variable type in .NET.
Operators can be overloaded as well such as implicit/explicit operators that allow conversions of hardcoded values or variables into a new variable.

```csharp
// implicit
public static implicit operator decimal(TransactionAmount currency)
{
    return currency.GetValue();
}
// usage
decimal value = amount;

// explicit
public static explicit operator TransactionAmount(decimal amount)
{
    uint dollars = (uint)amount;
    var remainder = amount - dollars;
    uint cents = (uint)(remainder * 100);
    return TransactionAmount.FromUsd(dollars, cents);

}
// usage
(TransactionAmount)amountToWithdraw
```