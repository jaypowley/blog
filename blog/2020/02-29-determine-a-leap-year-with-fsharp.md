@{
    Layout = "blogpost";
    Title = "Determine A Leap Year With F#";
    AddedDate = "2020-02-29T12:00:00";
    Tags = "F#, Scripts";
    Description = "";
 }
 
## Determine A Leap Year With F#

With this year being a leap year, and today being a leap day, I thought it would be an easy calculation to do in F# to figure out if a given year was a leap year.

To be honest, I seriously thought leap years were easily discernible. Is the current year evenly divisible by 4? Yes &mdash; Leap Year. It wasn't until I read a [Microsoft Tech Community blog](https://techcommunity.microsoft.com/t5/azure-developer-community-blog/it-s-2020-is-your-code-ready-for-leap-day/ba-p/1157279) post earlier this week that I learned there were a couple more rules in play.

>Many think leap years occur every four years, but the exact algorithm is slightly more complicated:  
>Is the year evenly divisible by 4? Then it **is a leap year**. (Examples: 2012, 2016, 2020, 2024)  
> … Unless it is also evenly divisible by 100. Those are **not leap years**. (Examples: 1800, 1900, 2100)  
> … Except those years that are evenly divisible by 400 **are leap years**. (Examples: 1600, 2000, 2400)  

I broke each rule into a function and return the state based on the given year value. Since rule 2 and 3 are directly dependent on each other, I grouped them together for the result.

```fsharp
let isEvenlyDivisibleByFour (year:int) : bool = year % 4 = 0
let isEvenlyDivisibleByOneHundred (year:int) : bool = year % 100 = 0
let isEvenlyDivisibleByFourHundred (year:int) : bool = year % 400 = 0

let isLeapYear (year:int) : bool =
    let divisibleByFour = isEvenlyDivisibleByFour year
    let divisibleByOneHundred = isEvenlyDivisibleByOneHundred year
    let divisibleByFourHundred = isEvenlyDivisibleByFourHundred year
    divisibleByFour && (not divisibleByOneHundred || divisibleByFourHundred)

isLeapYear 2016;;
isLeapYear 2020;;
isLeapYear 2021;;
isLeapYear 2024;;
isLeapYear 1800;;
isLeapYear 1900;;
isLeapYear 2100;;
isLeapYear 1600;;
isLeapYear 2000;;
isLeapYear 2400;;
```

Output:
```
> isLeapYear 2016;;
val it : bool = true

> isLeapYear 2020;;
val it : bool = true

> isLeapYear 2021;;
val it : bool = false

> isLeapYear 2024;;
val it : bool = true

> isLeapYear 1800;;
val it : bool = false

> isLeapYear 1900;;
val it : bool = false

> isLeapYear 2100;;
val it : bool = false

> isLeapYear 1600;;
val it : bool = true

> isLeapYear 2000;;
val it : bool = true

> isLeapYear 2400;;;;
val it : bool = true
```

```fsharp
let years = [1998 .. 2014]
for year in years do
    printf "Is %d a Leap Year? %b\r\n" year (isLeapYear year)
```

Output:  
Is 1998 a Leap Year? false  
Is 1999 a Leap Year? false  
Is 2000 a Leap Year? true  
Is 2001 a Leap Year? false  
Is 2002 a Leap Year? false  
Is 2003 a Leap Year? false  
Is 2004 a Leap Year? true  
Is 2005 a Leap Year? false  
Is 2006 a Leap Year? false  
Is 2007 a Leap Year? false  
Is 2008 a Leap Year? true  
Is 2009 a Leap Year? false  
Is 2010 a Leap Year? false  
Is 2011 a Leap Year? false  
Is 2012 a Leap Year? true  
Is 2013 a Leap Year? false  
Is 2014 a Leap Year? false  
