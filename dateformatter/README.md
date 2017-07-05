# Timespan formatter kata

## The problem

We have a system that processes tasks. Each task takes some amount of time. We know these durations in minutes, but we want to print them out in a more human-readable form, i.e., in weeks, days, hours, and minutes.

## Objective

Write a function or method that takes as input an amount of time expressed as an arbitrary positive number of minutes, and returns a string with a human-readable description of that amount of time expressed in weeks, days, hours, and minutes.

For example: given <code>12345</code>, return: <code>"1 week 1 day 13 hours 45 minutes"</code>

The solution must satisfy the following:

* Zero values should generally not be output; for example, given <code>10345</code>, return <code>"1 week 4 hours 25 minutes"</code> (i.e., skip days, as that would be 0)
* There's only one exception to the rule above: for input <code>0</code>, return <code>"0 minutes"</code>
* Use singular and plural as needed
* In the basic version, don't use commas or other conjuctions.

The kata should be solved in TDD. Optionally, use a functional programming language and try to keep it pure FP.

## Optional tasks

### 1. Use conjunctions

Use commas and "and" appropriately, for example: <code>"1 week, 1 day, 13 hours, and 45 minutes"</code>.

### 2. Provide a compact alternative

Write another method or function with the same behavior as above (or add an optional behavior to the original function) to produce a compact output using "w" for weeks, "d" for days, "h" for hours, and "m" for minutes, like this:

* given <code>12345</code>, return: <code>"1w 1d 13h 45m"</code>

Keep your original function, and try to end up with as little duplicated code as possible.

### 3. Round the less significant parts
Often, it makes little sense to use widely different units of time when describing time spans. For example, it makes sense to say that resolving a kata will take "2 minutes" or "2 weeks", but "2 weeks and 2 minutes" sounds weird. In order to make our timespan description more "human", we want to rule out weird sentences like that.

Let's start by looking at the stack of units of time we are using:

weeks<br>
days<br>
hours<br> 
minutes

Let's also define the **depth** of a timespan description as the distance (in "steps") between the *largest* and 
the *smallest* unit of time that is being used. For example, "weeks" are one step above "days", so "1 week 2 days" has depth 1; on the other hand, weeks are 3 steps above minutes, so "1 week 2 minutes" has depth 3.

**Your goal**: Add an argument to your function to specify the maximum depth allowed in the output. Then modify the function to omit the less significant parts of the description accordingly. For example, here's how the description should change based on the maximum depth argument:

basic description | maximum depth | resulting description
------------------|---------------|----------------------
1 week 1 day 1 hour 1 minute | 3 | 1 week 1 day 1 hour 1 minute
2 weeks 1 hour 13 minutes | 2 | 2 weeks 1 hour 
2 weeks 1 day 2 hours 1 minute | 1 | 2 weeks 1 day
1 day 1 minute | 1 | 1 day 
1 day 1 minute | 2 | 1 day 1 minute 

When omitting parts of the timespan, round to the *nearest value allowed by your maximum depth*, i.e., if omitting minutes, increment the hours if minutes are >30; if omitting hours, increment the days if the hours are >12; if omitting days, increment the weeks if the days are >3. Here's some more example:

basic description | maximum depth | resulting description
------------------|---------------|----------------------
1 week 1 day 13 hours 45 minutes | 2 | 1 week 1 day 14 hours
1 week 1 day 13 hours 45 minutes | 1 | 1 week 2 days
1 week 3 days 12 hours 31 minutes | 0 | 2 weeks

(The last example is the trickiest; make sure to have a test for it).

### 3bis. Combine 2 and 3 :-)
