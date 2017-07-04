# Date formatter kata

Write a function or method that takes as input an amount of time, expressed as an arbitrary number of minutes, and returns 
a string with a human-readable description of that amount of time expressed in weeks, days, hours, and minutes.

For example: given <code>12345</code>, return: <code>"1 week 1 day 13 hours 45 minutes"</code>

The solution must satisfy the following:

* Zero values should generally not be output; for example, given <code>10345</code>, return <code>"1 week 4 hours 25 minutes"</code> (i.e., skip days, as that would be 0)
* There's only one exception to the rule above: for input <code>0</code>, return <code>"0 minutes"</code>
* Use singular and plural as needed

The kata should be solved in TDD, possibly using a functional programming language.

## Optional tasks

### Use conjunctions

Use commas and "and" appropriately, for example: <code>"1 week, 1 day, 13 hours, and 45 minutes"</code>.

### Round the less significant parts

Let's define the "depth" of the output string produced by our function as the number of "steps" between the *largest* and 
the *smallest* unit of time that is being used. For example:

<code>"1 week 1 day 13 hours 45 minutes"</code> has depth 3 (weeks is "3 steps" away from minutes)<br>
<code>"1 week 45 minutes"</code> also has depth 3 (idem)<br>
<code>"1 hour 45 minutes"</code> has depth 1 (hours is "1 step" away from minutes)<br>
<code>"1 hour"</code> has depth 0 (hours is both the largest and smallest unit of time)

Add an argument for your function to specify the maximum depth allowed in the output. Round the less significant parts
of the amount of time as needed to satisfy this constraint. Rounding is to the nearest value. For example:

given <code>12345</code> and maximum depth <code>3</code>, return: <code>"1 week 1 day 13 hours 45 minutes"</code> as usual (depth 3 is allowed)<br>
given <code>12345</code> and maximum depth <code>2</code>, return: <code>"1 week 1 day 14 hours"</code> (depth 3 is not allowed; minutes must be skipped, and they are rounded up to one full hour)<br>
given <code>12345</code> and maximum depth <code>1</code>, return: <code>"1 week 2 days"</code> (depth 2 is not allowed: hours must be skipped and again get rounded up to one full day)<br>
given <code>12345</code> and maximum depth <code>0</code>, return: <code>"1 week"</code> (days get rounded down to 0 as 2 days are less than 1/2 week)<br>


