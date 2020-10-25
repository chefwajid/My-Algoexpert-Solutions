# Problem Statement:

Imagine that you want to schedule a meeting of a certain duration with a co-worker. You have access to your calendar and your co-worker's calendar both of which contain your respective meetings for the day, in the form of ( [startTime, endTime] ), as well as both of your daily bounds (i.e., the earliest and the latest times at which you're available for meetings every day, in the form of [earliestTime, latestTime] ).

Write a function that takes in your calendar, your daily bounds, your co-worker's calendar, your co-worker's daily bounds, and the duration of the meeting that you want to schedule, and that returns a list of all the time blocks (in the form of |[startTime, endTime] ) during which you could schedule the meeting, ordered from earliest time block to latest.

Note that times will be given and should be returned in military time. For example: 8:36 , 9:61 ,and 23:56 .

Also note that the given calendar times will be sorted by start time in ascending order, as you would expect them to be in a calender like Google Calendar.

## Sample Input

```cpp
calendar1 = [['9:00', '10:30'], ['12:00', '13:00'], ['16:00', '18:00']]
dailyBounds1 = ['9:00', '20:00']
calendar2 = [['10:00', '11:30'], ['12:30', '14:30'], ['14:30', '15:00'], ['16:00', '17:00']]
dailyBounds2 = ['10:00', '18:30']
meetingDuration = 30
```

## Sample Output

```cpp
[['11:30', '12:00'], ['15:00', '16:00'], ['18:00', '18:30']]
```

# *Solution 1 :*

- [ ]  Done on my own

## Explanation :

1. Add *0 to 1rst Daily Bound[0]* & *DailyBound[1] to 23:59* as an occupied meeting for both
2. Convert String to integers in minutes for ease of calculations
3. Merge Calendars based on starting time using concept of merging sorted arrays
4. Flatten The Calendar arrays based on logic **PREVIOUS END > = CURRENT END then MERGE**
5. Find all availability time greater than meeting duration, and add to an array (also int to string)
6. Return that array

Pretty neat solution with modular code i'd say. Touche Clement !

## Code :

```cpp
def calendarMatching(calendar1, dailyBounds1, calendar2, dailyBounds2, meetingDuration):

	calendar1 = updateCalendar(calendar1,dailyBounds1)
	calendar2 = updateCalendar(calendar2,dailyBounds2)
	mergedCalendar = mergeCalendars(calendar1,calendar2)
	flattenedCalendar = flattenCalendar(mergedCalendar)
	availabilityTimes = availabilitySlots(flattenedCalendar,meetingDuration)
	
	return availabilityTimes

def updateCalendar(calendar,dailyBounds):

	updatedCalendar = calendar[:]
	updatedCalendar.insert(0,["0:00",dailyBounds[0]])
	updatedCalendar.append([dailyBounds[1],"23:59"])

	return list(map(lambda m:[timeToMinutes(m[0]),timeToMinutes(m[1])],updatedCalendar))

def mergeCalendars(calendar1,calendar2):

	mergedCalendars = []
	i=0
	j=0

	while i < len(calendar1) and j < len(calendar2):

		if calendar1[i][0] < calendar2[j][0]:
			mergedCalendars.append(calendar1[i])
			i+=1

		else: 
			mergedCalendars.append(calendar2[j])
			j+=1

	while(i<len(calendar1)):
		mergedCalendars.append(calendar1[i])
		i+=1 
	while(j<len(calendar2)):
		mergedCalendars.append(calendar2[j])
		j+=1

	return mergedCalendars 

def flattenCalendar(mergedCalendar):

	flattenedCalendar = [mergedCalendar[0]]

	for i in range(1,len(mergedCalendar)):

		prevStart = flattenedCalendar[-1][0]
		prevEnd = flattenedCalendar[-1][1]

		currentStart = mergedCalendar[i][0]
		currentEnd = mergedCalendar[i][1]

		if prevEnd >= currentStart:
			newPrev = [prevStart,max(prevEnd,currentEnd)]
			flattenedCalendar[-1] = newPrev

		else:
			flattenedCalendar.append(mergedCalendar[i])

	return flattenedCalendar
	
def timeToMinutes(time):
	hour,minute = list(map(int,time.split(":")))
	minutes = hour * 60 + minute
	return minutes

def timeToString(time):
	hour = time // 60
	minute = time % 60
	minute = '0' + str(minute) if minute < 10 else str(minute)
	return str(hour) + ":" + minute

def availabilitySlots(flattenedCalendar,meetingDuration):
	availableSlots = []
	for i in range(1,len(flattenedCalendar)):
		if abs(flattenedCalendar[i][0] - flattenedCalendar[i-1][1]) >= meetingDuration: 
			availableSlots.append([flattenedCalendar[i-1][1],flattenedCalendar[i][0]])

	return list(map(lambda m : [timeToString(m[0]),timeToString(m[1])],availableSlots))
```

## Time Space Complexity :

( C1 + C2 ) Time | ( C1 + C2 ) Space