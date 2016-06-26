# Dates-and-Times-with-lubridate
swirl Lesson 1: Dates and Times with lubridate
1/this_day <- today() # for today
[1] "2016-06-26"
---------------------------------
2/ Print the contents of this_day to the
| console.

> this_day 
[1] "2016-06-26"
------------------------------------
3/The today() function returns today's
| date. Give it a try, storing the result
| in a new variable called this_day.
year(this_day)
[1] 2016
-----------------------------
4/We can also get the day of the week
| from this_day using the wday()
| function. It will be represented as a
| number, such that 1 = Sunday, 2 =
| Monday, 3 = Tuesday, etc. Give it a
| shot.
wday(this_day)
[1] 1
----------------------------------------
5/Now try the same thing again, except
| this time add a second argument, label
| = TRUE, to display the *name* of the
| weekday (represented as an ordered
| factor).

wday(this_day, label = TRUE)
[1] Sun
7 Levels: Sun < Mon < Tues < ... < Sat
-----------------------------------
6/In addition to handling dates,
| lubridate is great for working with
| date and time combinations, referred to
| as date-times. The now() function
| returns the date-time representing this
| exact moment in time. Give it a try and
| store the result in a variable called
| this_moment.
=this_moment<-now()
-------------------------------
7/| View the contents of this_moment.

> this_moment
[1] "2016-06-26 22:52:12 AST"
----------------------------------
8/Just like with dates, we can extract
| the year, month, day, or day of week.
| However, we can also use hour(),
| minute(), and second() to extract
| specific time information. Try any of
| these three new functions now to
| extract one piece of time information
| from this_moment.
> minute(this_moment)
[1] 52
--------------------------------------
9/today() and now() provide neatly
| formatted date-time information. When
| working with dates and times 'in the
| wild', this won't always (and perhaps
| rarely will) be the case.

-------------------------------------
10/
| Fortunately, lubridate offers a variety
| of functions for parsing date-times.
| These functions take the form of ymd(),
| dmy(), hms(), ymd_hms(), etc., where
| each letter in the name of the function
| stands for the location of years (y),
| months (m), days (d), hours (h),
| minutes (m), and/or seconds (s) in the
| date-time being read in.

...
--------------------------------------------
11/To see how these functions work, try
| ymd("1989-05-17"). You must surround
| the date with quotes. Store the result
| in a variable called my_date.

my_date<-ymd("1989-05-17")
============================

12/Now take a look at my_date.
<-my_date
[1] "1989-05-17"
-------------------------------
13/It looks almost the same, except for
| the addition of a time zone, which
| we'll discuss later in the lesson.
| Below the surface, there's another
| important change that takes place when
| lubridate parses a date. Type
| class(my_date) to see what that is.

> class(my_date)
[1] "Date"
[1] "1989-05-17"
-----------------------------------------
14/"1989-05-17" is a fairly standard
| format, but lubridate is 'smart' enough
| to figure out many different date-time
| formats. Use ymd() to parse "1989 May
| 17". Don't forget to put quotes around
| the date!

> ymd( "1989 May 17")
[1] "1989-05-17"
-------------------------------------
15/
| So ymd() took a character string as
| input and returned an object of class
| POSIXct. It's not necessary that you
| understand what POSIXct is, but just
| know that it is one way that R stores
| date-time information internally.
> mdy("March 12, 1975")
[1] "1975-03-12"
------------------------------
16/We can even throw something funky at it
| and lubridate will often know the right
| thing to do. Parse 25081985, which is
| supposed to represent the 25th day of
| August 1985. Note that we are actually
| parsing a numeric value here -- not a
| character string -- so leave off the
| quotes.

>> 25081985
[1] 25081985
-----------------------------

| 17/Not quite right, but keep trying. Or,
| type info() for more options.

| Use dmy(25081985) to see how lubridate
| handles something a little different
| from what we've seen so far.
> dmy(25081985)
[1] "1985-08-25"
---------------------------------

18/But be careful, it's not magic. Try
| ymd("192012") to see what happens when
| we give it something more ambiguous.
| Surround the number with quotes again,
| just to be consistent with the way most
| dates are represented (as character
| strings).
> ymd("192012")
[1] NA
------------------------------
19/You got a warning message because it
| was unclear what date you wanted. When
| in doubt, it's best to be more
| explicit. Repeat the same command, but
| add two dashes OR two forward slashes
| to "192012" so that it's clear we want
| January 2, 1920.

> ymd("1920/1/2")
[1] "1920-01-02"

---------------------------
20/
| In addition to dates, we can parse
| date-times. I've created a date-time
| object called dt1. Take a look at it
| now.

> dt1
[1] "2014-08-23 17:23:02"
-------------------------------
21/Now parse dt1 with ymd_hms().

> ymd_hms(dt1)
[1] "2014-08-23 17:23:02 UTC"

-----------------------------------
22/
| You got a warning message because it
| was unclear what date you wanted. When
| in doubt, it's best to be more
| explicit. Repeat the same command, but
| add two dashes OR two forward slashes
| to "192012" so that it's clear we want
| January 2, 1920.
> hms("03:22:14")
[1] "3H 22M 14S"

-----------------------------------
23/lubridate is also capable of handling
| vectors of dates, which is particularly
| helpful when you need to parse an
| entire column of data. I've created a
| vector of dates called dt2. View its
| contents now.
------------------------------------
23/Now parse dt2 using the appropriate
| lubridate function.
> ymd(dt2) 
[1] "2014-05-14" "2014-09-22" "2014-07-11"
-----------------------------------------
24/
| The update() function allows us to
| update one or more components of a
| date-time. For example, let's say the
| current time is 08:34:55 (hh:mm:ss).
| Update this_moment to the new time
| using the following command:
| 
| update(this_moment, hours = 8, minutes= 34, seconds = 55).
[1] "2016-06-26 08:34:55 AST"
-----------------------------------------------------------
25/It's important to recognize that the
| previous command does not alter
| this_moment unless we reassign the
| result to this_moment. To see this,
| print the contents of this_moment

> this_moment
[1] "2016-06-26 22:52:12 AST"
--------------------------------------
26/Unless you're a superhero, some time
| has passed since you first created
| this_moment. Use update() to make it
| match the current time, specifying at
| least hours and minutes. Assign the
| result to this_moment, so that
| this_moment will contain the new time.
> this_moment<-update(this_moment, hours = 8, minutes = 34, seconds = 55)

-------------------------------
27/ake one more look at this_moment to
| see that it's been updated.

> this_moment
[1] "2016-06-26 08:34:55 AST"
-----------------------------
28/Now, pretend you are in New York City
| and you are planning to visit a friend
| in Hong Kong. You seem to have
| misplaced your itinerary, but you know
| that your flight departs New York at
| 17:34 (5:34pm) the day after tomorrow.
| You also know that your flight is
| scheduled to arrive in Hong Kong
| exactly 15 hours and 50 minutes after
| departure.
----------------------------------------
29/
To find the current date in New York,
| we'll use the now() function again.
| This time, however, we'll specify the
| time zone that we want:
| "America/New_York". Store the result in
| a variable called nyc. Check out ?now
| if you need help.

> nyc<-now("America/New_York")
------------------------------
30/or a complete list of valid time zones
| for use with lubridate, check out the
| following Wikipedia page:
| 
| http://en.wikipedia.org/wiki/List_of_tz_database_time_zones

...
-------------------------------
31/View the contents of nyc, which now
| contains the current date and time in
| New York.
> nyc
[1] "2016-06-26 17:20:49 EDT
---------------------------------
32/
| Your flight is the day after tomorrow
| (in New York time), so we want to add
| two days to nyc. One nice aspect of
| lubridate is that it allows you to use
| arithmetic operators on dates and
| times. In this case, we'd like to add
| two days to nyc, so we can use the
| following expression: nyc + days(2).
| Give it a try, storing the result in a
| variable called depart.

> depart<- (nyc + days(2)
-------------------------------
33/Take a look at depart.

> depart
[1] "2016-06-28 17:20:49 EDT"
-------------------------------
34/So now depart contains the date of the
| day after tomorrow. Use update() to add
| the correct hours (17) and minutes (34)
| to depart. Reassign the result to
| depart.
>  depart <- update(depart, hours = 17, minutes = 34)
----------------------------------------------
35/Take one more look at depart.

> depart
[1] "2016-06-28 17:34:49 EDT"
-----------------------------------------
36/
Your friend wants to know what time she
| should pick you up from the airport in
| Hong Kong. Now that we have the exact
| date and time of your departure from
| New York, we can figure out the exact
| time of your arrival in Hong Kong.
------------------------------------------
37/o now depart contains the date of the
| day after tomorrow. Use update() to add
| the correct hours (17) and minutes (34)
| to depart. Reassign the result to
| depart.
>arrive<-arrive <- depart + hours(15) + minutes(50)
---------------------------------
38/he with_tz() function returns a
| date-time as it would appear in another
| time zone. Use ?with_tz to check out
| the documentation.
?with_tz
-----------------------------
39/Use with_tz() to convert arrive to the
| "Asia/Hong_Kong" time zone. Reassign
| the result to arrive, so that it will
| get the new value.
arrive<-with_tz(arrive,("Asia/Hong_Kong) 
---------
40/rint the value of arrive to the
| console, so that you can tell your
| friend what time to pick you up from
| the airport.
> arrive
[1] "2016-06-29 21:24:49 HKT"

--------------------------
41/Fast forward to your arrival in Hong
| Kong. You and your friend have just met
| at the airport and you realize that the
| last time you were together was in
| Singapore on June 17, 2008. Naturally,
| you'd like to know exactly how long it
| has been.

...
-----------------------------
42/Use the appropriate lubridate function
| to parse "June 17, 2008", just like you
| did near the beginning of this lesson.
| This time, however, you should specify
| an extra argument, tz = "Singapore".
| Store the result in a variable called
| last_time.
> last_time <- mdy("June 17, 2008", tz = "Singapore")
----------------------------------------------
43/View the contents of last_time.

> last_time
[1] "2008-06-17 SGT"

------------------------
44/ Pull up the documentation for
| interval(), which we'll use to explore
| how much time has passed between arrive
| and last_time
?interval
-----------------
45/Create an interval() that spans from
| last_time to arrive. Store it in a new
| variable called how_long.

> how_long<-interval(last_time,arrive)
------------------------------------------
46/
| Now use as.period(how_long) to see how
| long it's been.

> as.period(how_long)
[1] "8y 0m 12d 21H 24M 49.9415609836578S"

--------------------------------------------
47/ This is where things get a little
| tricky. Because of things like leap
| years, leap seconds, and daylight
| savings time, the length of any given
| minute, day, month, week, or year is
| relative to when it occurs. In
| contrast, the length of a second is
| always the same, regardless of when it
| occurs.

...
----------------------------
48/ This is where things get a little
| tricky. Because of things like leap
| years, leap seconds, and daylight
| savings time, the length of any given
| minute, day, month, week, or year is
| relative to when it occurs. In
| contrast, the length of a second is
| always the same, regardless of when it
| occurs.

...
-------------------------
49/
| This is where things get a little
| tricky. Because of things like leap
| years, leap seconds, and daylight
| savings time, the length of any given
| minute, day, month, week, or year is
| relative to when it occurs. In
| contrast, the length of a second is
| always the same, regardless of when it
| occurs.

...

  |=============================== |  97%
50/
| To address these complexities, the
| authors of lubridate introduce four
| classes of time related objects:
| instants, intervals, durations, and
| periods. These topics are beyond the
| scope of this lesson, but you can find
| a complete discussion in the 2011
| Journal of Statistical Software paper
| titled 'Dates and Times Made Easy with
| lubridate'.

...

  |=============================== |  98%
51/
| This concludes our introduction to
| working with dates and times in
| lubridate. I created a little timer
| that started running in the background
| when you began this lesson. Type
| stopwatch() to see how long you've been
| working!

> stopwatch()
[1] "2H 48M 47.2059810161591S"
--------------------------
52/
