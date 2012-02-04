## Get rich: be Miserly

Miser is a Python library that can be used for writing scripts that'll help you
project costs and figure out how to accumulate money. It is in super-secret
alpha stealth mode, so it's not packaged properly, lacks tests, and is unstable.
For now.

## Example

Here's a simple usage:

```python
from miser import *
from miser.scheduling import *

# instantiate a Miser instance
m = Miser("sample")

# set a goal
g = Goal("enough to buy some dj equipment",
         amount = 6e3, # $6,000
         by = Date(2012, 8, 1)) # by Aug. 1, 2012

m.addGoal(g)

m.addTransactions(

    # Expenses
    Expense(name = "MATH315 tuition",
            amount = 1.3e3,
            on = Date(2011, 8, 29)), # non-recurring
                        
    Expense(name = "netflix",
            amount = 7.,
            on = MonthlyRecurring(15)), # 15th day of the month
                                 
    Expense(name = "weekly beer",
            amount = 10.,
            on = WeeklyRecurring(FR)), # every week on Friday
                                  
    Expense(name = "lunch",
            amount = 6.,
            on = WeeklyRecurring((MO, TU, TH))),
                                   
    Expense(name = "debt",
            amount = 4e3,
            on = Date(2011, 8, 29)),
                                  
    # Income
    Income(name = "job",
           amount = 1.5e3,
           on = MonthlyRecurring((7, 22))),
)

# Print a simulation of the year
def summary(fromdt, todt):
  args = (m, fromdt, todt)
  GoalPrinter(*args)
  Histogram(*args)

if __name__ == '__main__':
  summary(Date(2011, 8, 20), Date(2012, 9, 1))
```

which produces

    sample: 2011-08-20 00:00:00 to 2012-09-01 00:00:00
    Total saved: 29116.00

    Goals:
    Goal 'enough to buy some serious dj equipment' met with 23116.00 to spare!

    Profile of expenses:

     debt            -4000.0 ----------------------------------------------------------
     MATH315 tuition -1300.0 ------------------
     lunch           -960.0  -------------
     weekly beer     -540.0  -------
     netflix         -84.0   -

