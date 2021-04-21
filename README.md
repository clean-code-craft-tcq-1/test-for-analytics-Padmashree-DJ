# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. CSV file to PDF converter plugins.
3. List of Recipients to be notified every week.
4. Breach limits information.
5. Real Time Clock data for timestamp information for recording trends.
6. Trend setting information as to what is to be considered as a trend.
7. The means of notifying mechanism to be known e.g. is it email alert or controller alert or any other system alert.

(add more if needed)

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | Yes           | This is the plugin being used.
Counting the breaches       | Yes           | Tracking when the BMS reading is breached with the Pure function.
Detecting trends            | Yes           | Once the trend setting is done , we could take timestamp when the trend detected with the help of Real time clock.
Notification utility        | Yes           | Alert functionality could be implemented once the notification means is known to the developer.

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write "Breach exists" from the values provided when Breach is detected.
4. Measure number of breaches when the breaching happens over a period of time with respect to RTC.
5. Check Trend is recorded when the reading was behaving according to rules of trend setting.
6. Check Notification is sent when a week is passed.
7. Check the notifcation has returned with NULL data when the CSV file is empty.
8. Check that the exception is thrown when recorded Timestamp does not alighn with Real time clock.

(add more)

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | New PDF report | Notification over email   | Fake the email notification
Report inaccessible server | Access to Server | PDF with reading invalid input           |Fake teh PDF print.
Find minimum and maximum   | CSV data | Minimum and Maximum values               | None - it's a pure function
Detect trend               | Trend setting input | Observe the reading for the trend setting.           | None - it's a pure function
Write to PDF               | Analysed Data | PDF file             | Fake- Print statements to check.
