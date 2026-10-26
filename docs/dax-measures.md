# DAX Measure Reference

The expressions below are transcribed from the supplied PBIP semantic model. Names and logic are preserved.

```DAX
Total Bookings =
DISTINCTCOUNT(Bookings[Booking_ID])

Cancelled Bookings =
CALCULATE([Total Bookings], Bookings[Booking_Cancelled] = "Yes")

Cancellation Rate =
DIVIDE([Cancelled Bookings], [Total Bookings], 0)

Average Satisfaction =
AVERAGE(Bookings[Guest_Satisfaction_Score])

Average Stay Cost =
AVERAGE(Bookings[Estimated_Stay_Cost_USD])

Estimated Completed-Stay Revenue =
SUM(Bookings[Estimated Revenue from Completed Stays])

Average Check-in Delay =
AVERAGE(Bookings[Check_in_Delay_Minutes])

Repeat Visitor Rate =
DIVIDE(
    CALCULATE([Total Bookings], Bookings[Repeat_Visitor] = "Yes"),
    CALCULATE([Total Bookings], Bookings[Repeat_Visitor] IN {"Yes", "No"}),
    0
)

Bookings Above Min Satisfaction =
VAR MinScore = [Minimum Satisfaction Value]
RETURN
    CALCULATE(
        [Total Bookings],
        FILTER(Bookings, Bookings[Guest_Satisfaction_Score] >= MinScore)
    )

Minimum Satisfaction Value =
SELECTEDVALUE('Minimum Satisfaction'[Minimum Satisfaction], 7)
```

The model also includes a field parameter named `Metric Selector` with these options:

```DAX
{
    ("Total Bookings", NAMEOF('Bookings'[Total Bookings]), 0),
    ("Average Satisfaction", NAMEOF('Bookings'[Average Satisfaction]), 1),
    ("Average Stay Cost", NAMEOF('Bookings'[Average Stay Cost]), 2)
}
```

## Interpretation

- `Estimated Completed-Stay Revenue` depends on a calculated estimated cost for bookings not marked cancelled. It is not verified revenue or profit.
- `Repeat Visitor Rate` is calculated over booking records marked Yes/No; there is no guest identifier to count distinct returning people.
- `Cancellation Rate` honors the `Booking_Cancelled` filter. Selecting only `Yes` can produce a 100% rate because both the numerator and denominator are evaluated in that filtered context.
