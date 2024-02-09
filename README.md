Aviation Crash Analysis
================
Group 6

## Summary

The goal of this project was to research the reliability of aircrafts
using this historical plane accident dataset. We were curious if there
any variables such as dates, seasons, locations, aircraft types or
operators that stand out in the number of accidents We are also looking
at overall trends in accidents per year and want to see if accidents are
decreasing or increasing over the last decades.

## Presentation

Our presentation can be found [here](presentation/presentation.html).

## Total Accidents

The visualization on slide 4 shows that zero accidents per day is the
most common, with one accident per day being somewhat frequent. Two
accidents per day is not extremely unlikely either. Three accidents on
one day are very rare and a big part of these days in this dataset were
during WW2. Four accidents on the same day only oceurred once one
08/31/1988 and once on 09/11/2001.

As seen on slide 5, accidents over time increased in general till about
1950 and then slowly decreased till 2000 before dropping quite rapidly.
The increase at first can be explained by the increasing number of
flights as flying became more popular, especially for military purposes
at first. Although the total flight numbers further increased since
1950, accident numbers decreased as technology (safety technology in
cockpits) advanced, air traffic control improved and pilot training was
enhanced.

## Total Fatalities

Slide 6 shows the frequency of fatalities based on their fatality number
with binwidhts of 50. One can clearly see that most accidents involve
fatality numbers of below 50 people. The frequency of fatality numbers
drops very quickly as fatality numbers increase.

For summary statistics, the mean fatality number for accidents is around
22.3 and the median is at 11. This was expected as the plot is heavily
right-skewed. The standard deviation of the fatality number in accidents
is 35.0.

Over time, one can see that fatalities per year were constantly low
until about 1940. Then they increased rapidly as commercial flights with
many passengers became increasingly popular after the end of the second
world war. Fatality numbers still increased up to around 1975 before
decreasing again till 2019 where the dataset ends (slide 7).

## Association between Accidents and Fatalities

On slide 8, one can observe a clear linear trend in number of fatalities
based on number of accidents per year. This was expexcted based on the
similar trends in both accidents and fatalities over time. The model
gives a linear regression of:
\[\widehat{fatalities} = -170.07486  + 26.96004 \times accidents\] The
r-squared value is about 0.70, indicating that this model can predict
about 70% of the fatality values based on the predictor variable, which
is number of accidents per year.

## Time Variable

Slide 10 visualizes the time with the highest number of fatalities. We
can see the number of fatalities peak around 11:00.

Slide 11 visualizes the time with the highest number of crashes. It
makes sense that these graphs look similar because since there are more
crashes there are more fatalities.

Slide 12 Shows the time with the highest number of crashes, and assigns
a linear model to crashes and the hour of the day. From the model, we
see as is gets earlier in the day(starting at 0:00), the number of
crashes decrease by 1.365. The r squared shows that about 17% of the
variability of the number of crashes is predicted by the model. This low
r squared means time might not be the best predictor of plane crashes.

## Month and Season

Slide 14 visualizes total fatalities over each month, investigating
weather or not time of year influences aviation safety. There is a weak
positive linear trend, with a R-Squared value of 0.41 making this
association weak. Time of year is not a good predictor of plane crash
fatalities.

Slide 15 visualizes the proportion of fatalities among all on board an
aircraft, by month and split into seasons. There is no strong trend,
except for that there are lost mortality rates in Summer compared to the
other months.

Slide 16 is a similar visualization, except it shows total crashes per
month and split into seasons. There is even less of a clear association
between these variables, indicating that month and season are not good
predictors of plane crash rates and mortality rates.

## Operator

Slide 17 visualizes top ten amount of crashes per operator and top 10
fatalities per operator. There seems to be a relationship that the more
crashes an operator has the more fatalities an operator has .

Slide 18 visualizes the linear model between crashes per operator and
fatalities per operator . The linear regression model predicts that for
every additional crash per operator the number of fatalities is expected
to be more on average by 29.18 persons. The R^2 of the model is .87
which means 87% of the variability in the response variable (fatalities)
is explained by the regression model. The higher the value of R^2 is the
better the model fits the data. That means the more crashes the operator
has the more deaths the operators have. While it may seem intuitive it
is important to analyze the data and create a model that can predict
this idea. It is also important to check how well the model fits the
data by checking the value of R^2.

Slide 19 visualizes the linear model between year, crashes per operator
and fatalities per operator. The slope year of the linear model tells
us, all else held constant for each additional year, we would expect the
number of crashes to decrease by .7%. All else held constant each
additional crash per operator per year has .9% more fatalities per
operator. The R^2 value of the model is 27% which means that the model
does not fit the data very well.

## Limitations

The dataset only included accidents and not every single flight. Hence,
we were only able to analyze the accidents themselves but not the
relationship between accident numbers and total flights. The locations
given in the dataset were not in similar formats, which made mapping the
data impossible without manually reformatting almost 5000 observations.

## Conclusions

Aviation is getting safer, as there has been a decrease in fatalities
and accidents over the last years, but the variables we explored (time,
month/season, and operator) are not reliable predictors of when a plane
is more likely to crash.

## Data

Gurkan, C 2019, Airplane Crash Data Since 1908, viewed 22 March 2022,
<https://www.kaggle.com/datasets/cgurkan/airplane-crash-data-since-1908>.

The data frame airplane contains 4967 observations and 17 variables in
the dataset. Each row represents a crash.

The data was scraped from planecrashinfo.com and published on Kaggle
(<https://www.kaggle.com/datasets/cgurkan/airplane-crash-data-since-1908>).

The dataset contains aviation accidents throughout the world from
1908-2019. This includes all civil and commercial aviation accidents of
scheduled and non-scheduled passenger airliners worldwide, all cargo,
positioning, ferry and test flight fatal accidents, all military
transport accidents with 10 or more fatalities, all commercial and
military helicopter accidents with greater than 10 fatalities, all civil
and military airship accidents involving fatalities, aviation accidents
involving the death of famous people and aviation accidents or incidents
of noteworthy interest.

The variables included in the dataset are:

Date: Date of accident, in the format - January 01, 2001 Time: Local
time, in 24 hr. format unless otherwise specified Operator: Airline or
operator of the aircraft Flight \#: Flight number assigned by the
aircraft operator Route: Complete or partial route flown prior to the
accident AC Type: Aircraft type Registration: ICAO registration of the
aircraft cn / ln: Construction or serial number / Line or fuselage
number Aboard: Total aboard (passengers and crew) Aboard passengers:
Passengers aboard Aboard crew: Crew aboard Fatalities: Total fatalities
aboard (passengers and crew) Fatalities passengers: Passenger fatalities
aboard Fatalities crew: Crew fatalities aboard Ground: Total killed on
the ground Summary: Brief description of the accident and cause if known

Every observation in the dataset represents one accident.

## References

Gurkan, C 2019, Airplane Crash Data Since 1908, viewed 22 March 2022,
<https://www.kaggle.com/datasets/cgurkan/airplane-crash-data-since-1908>.