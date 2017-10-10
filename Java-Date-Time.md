## Date/Time manipulation in Java

**java.util.Date** is the key class that holds time. 
It doesnt store any localization or internationalization information, but stores time with respect to **universal time (UTC)/Greenwich mean time (GMT) zone**.
Usually the information it holds is the number of milliseconds between the current time and midnight, January 1, 1970 UTC.

### Parsing and Formatting:
It is very common you need to Parse a string to get Date & Formatting date to a String for printing/display. Following example is self explanatory

```
////For Parsing date from a string
SimpleDateFormat sdf = new SimpleDateFormat("MMM dd, yyyy HH:mm:ss z");
Date d = sdf.parse("Oct 25, 2007 18:35:07 EDT");
System.out.println("Timestamp: " + d.getTime());
// prints "1193351707000"

////For Display - generate string from date
SimpleDateFormat sdf = new SimpleDateFormat("yyyy/MM/dd  HH:mm:ss z'('Z')'");
TimeZone ist = TimeZone.getTimeZone("India/Chennai");
sdf.setTimeZone(ist);
System.out.println(sdf.format(d));
// prints "2014/05/07  18:35:07 IST(+0530)"

sdf.setTimeZone(TimeZone.getTimeZone("UTC"));
System.out.println("UTC date: " + sdf.format(d));
// prints "2014/05/07  13:05:07 UTC(+0000)"
```

### Locale usage with date formatting:
The Locale determines specific properties of user computer. It is mostly used
in client side of client/server architecture.
Following code snippet explains usage of Locale with date formatting.

```
  // get client locale
  java.util.Locale locale = request.getLocale();

  // get Dateformat for client's locale
  java.text.DateFormat df =
  java.text.DateFormat.getDateTimeInstance(
   java.text.DateFormat.LONG,
   java.text.DateFormat.LONG, locale);

  System.out.println( df.format( new java.util.Date() ));
  // prints "5 May 2014  13:05:07 IST"
```

**df.format()** always returns standard format. If you need customized format
we need to declare SimpleDateFormat object and set the custom format in addition to this.
