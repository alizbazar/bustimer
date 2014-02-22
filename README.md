# HSL Bus Timer (Bussiajastin)

Follow upcoming transport on selected bus/tram stop

1. Select a stop on the map
2. Select routes that you want to follow
3. See a time estimate on when the next bus will arrive to the stop

The app memorizes your last selection, so opening it the next time suggests you the past 3 bus followings. Clicking on one immediately gives you a time estimate for the upcoming bus.

Challenge here is really in estimating the time that it takes for the bus to arrive. This probably would need to use some **reinforcement learning** techniques with state defined, for example, using

* distance from the bus to the stop (better even if it's path distance of the bus)
* "rush hourness" of the current time of day

Rush-hourness could be statistically defined for each stop, or each bus.
Separate learning can be used for each stop or each bus.

**Another alternative** could be to try to measure "on-timeness" of the bus as the schedules are available. That would only require to follow the bus until it gets to the next stop, and measure the time difference with the schedule. That time difference could just be added to the official timetable of the stop.

The **on-timeness data** could also be gathered for extended period of time so that prediction could be made based on the time of day and the bus route.

**Third way** (maybe the easiest one) could be to estimate bus on-timeness based on its predicted location using the following algorithm:

1. Get bus location.
2. Detect next and previous stops on the route.
3. Calculate relative position on the path between stops, meaning 0% would be at stop 1, 100% would be at stop 2
4. Get timetables for both of the stops.
5. Calculate on-timeness by

    Delta = 
    CurrentTime
    - RelPosition * (NextStopPredictedTime - PreviousStopPredictedTime)
    - PreviousStopPredictedTime

**Challenge here is to know the next and the previous stop of the bus.** As we know legs of the route, perhaps one way would be to find the two closest points to the bus that are connected by a leg AND the bus is approx. in between them. This is probably prone to errors, perhaps there's a better way?

Error here comes mostly from the RelPosition, however usually bus stops are fairly close. Perhaps RelPosition could calculated better based on the location on the path leg. 

There is also a service that sort of shows predicted times for particular busses on particular stops, however it may be very difficult to plug that into the app:
http://www.thoreb.se/webdeparture/HKL/358/dep.asp?line=506&stopno=4010&stopname=Palkkatilanportti&dir=2&sort=0
