# Timespan formatter kata

## The problem

We have a task that takes some amount of time. We know this duration in minutes, but we want to print it out in a more human-readable form, i.e., in weeks, days, hours, and minutes.

## Objective

Write a function or method that takes as input an amount of time expressed as an arbitrary number of minutes, and returns 
a string with a human-readable description of that amount of time expressed in weeks, days, hours, and minutes.

For example: given <code>12345</code>, return: <code>"1 week 1 day 13 hours 45 minutes"</code>

The solution must satisfy the following:

* Zero values should generally not be output; for example, given <code>10345</code>, return <code>"1 week 4 hours 25 minutes"</code> (i.e., skip days, as that would be 0)
* There's only one exception to the rule above: for input <code>0</code>, return <code>"0 minutes"</code>
* Use singular and plural as needed
* In the basic version, don't use commas or other conjuctions.

The kata should be solved in TDD. Optionally, use a functional programming language and try to stick to pure FP.

## Optional tasks

### 1. Use conjunctions

Use commas and "and" appropriately, for example: <code>"1 week, 1 day, 13 hours, and 45 minutes"</code>.

### 2. Provide a compact alternative

Write another method or function with the same behavior as above, but that outputs time spans in a compact format using "w" for weeks, "d" for days, "h" for hours, and "m" for minutes.

For example: given <code>12345</code>, return: <code>"1w 1d 13h 45m"</code>

Keep your original function, and try to end up with as little duplicated code as possible.

### 3. Round the less significant parts
In many context, it makes little sense to use widely different units of time. For example, in estimating the time you will take to complete a kata, "20 minutes" makes sense, "2 weeks" makes sense, but "2 weeks and 2 minutes" doesn't.

Let's define the **depth** of the output string produced by our function as the distance between the *largest* and 
the *smallest* unit of time that is being used. "Weeks" are one step away from "days", two steps away from "hours", three steps away from "minutes". For example:

* <code>"1 week 1 day 13 hours 45 minutes"</code> has depth 3 (weeks, the largest unit of time being used, is "3 steps" away from minutes, the smallest)
* <code>"1 week 45 minutes"</code> also has depth 3 (same as above)
* <code>"1 hour 45 minutes"</code> has depth 1 (hours is "1 step" away from minutes)
* <code>"1 hour"</code> has depth 0 (hours is both the largest and smallest unit of time)

Add an argument for your function, to specify the maximum depth allowed in the output, by omitting the less significant parts of the amount of time, and round to the nearest value. For example:

* given <code>12345</code> and maximum depth <code>3</code>, return: <code>"1 week 1 day 13 hours 45 minutes"</code> as usual (depth 3 is allowed)
* given <code>12345</code> and maximum depth <code>2</code>, return: <code>"1 week 1 day 14 hours"</code> (depth 3 is not allowed; minutes must be skipped, and they are rounded up to one full hour)
* given <code>12345</code> and maximum depth <code>1</code>, return: <code>"1 week 2 days"</code> (depth 2 is not allowed: hours must be skipped and again get rounded up to one full day)
* given <code>12345</code> and maximum depth <code>0</code>, return: <code>"1 week"</code> (days get rounded down to 0 as 2 days are less than 1/2 week)

### 3bis. Combine 2 and 3 :-)



