# Google-Spreadsheet-to-Calendar

Before you dig into the code, we recommend that you reformat dates in your spreadsheet  to make it easier to program. 
### Go to Format > Number > Date Time.


###Step 1: Identify the calendar

First, we need to decide which Calendar we want to add information into. In this example, we want to add information from a spreadsheet into a team calendar. We use SpreadsheetApp to retrieve information from the spreadsheet that we’re working in. Then, the code will help us retrieve the value of the calendar ID from the cell that it lives in.

How to Convert Google Spreadsheet to Google Calendar
```javascript
var spreadsheet = SpreadsheetApp.getActiveSheet();
var calendarId = spreadsheet.getRange("C4").getValue();
```
Where getRange is the cell where you put your CalendarId


Next acces your calendar Id and paste it into sell

```javascript 
var eventCal = CalendarApp.getCalendarById(calendarId);
```

###Step 2: Select data from the Google Sheet

We need to identify the specific cells that we want to grab data from within our spreadsheet.
In this Sheet, the shifts are in column A-F, rows 2-11.

```javascript
 var signups = spreadsheet.getRange("A2:F11").getValues();
```


###Step 3: write the loop

```javascript
 for (x=0; x<signups.length; x++) {
      var shift = signups[x];
      
      var startTime = shift[0]; //A2
      var endTime = shift[1];//B2
      var title = shift[2];//C2
    var description = `
${shift[3]} //D2
${shift[4]} //E2
${shift[5]}`//F2
    var location = 'Home'
    var event = {
      'location' : location,
       'description': description,
        }// THE FOURTH PARAMETR FOR createEvent is an object so we have to put everething in object to show the description
```

###Step 4: Create events
```javascript
eventCal.createEvent(title,startTime,endTime,event)
```


```javascript
function scheduleShifts() {
  var spreadsheet = SpreadsheetApp.getActiveSheet();
  var calendarId = spreadsheet.getRange('A62').getValue();
  var eventCal = CalendarApp.getCalendarById(calendarId);
  var signups = spreadsheet.getRange("A2:F11").getValues();
 
  for (x=0; x<signups.length; x++) {
      var shift = signups[x];
      
      var startTime = shift[0];
      var endTime = shift[1];
      var title = shift[2];
    var description = `
${shift[3]} 
${shift[4]} 
${shift[5]}`
    var location = 'Home'
    var event = {
      'location' : location,
       'description': description,
        }
 
    eventCal.createEvent(title,startTime,endTime,event)
      }
   
}

```

###Step 5: Run the function
