# Google-Spreadsheet-to-Calendar
How to Convert Google Spreadsheet to Google Calendar
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
