# jQuery.iNumberEntry
A customizable number entry plugin for jQuery.

## Configuration
```javascript
$("#iNumberEntry").iNumberEntry(NumberEntry);
```

### NumberEntry

Name | Type | Defaults | Description
:--- | :--- | :--- | :---
linked | bool | false | If true, the numeric value will be linked to the previous numeric value, which will adjust depending on "minValue" and "maxValue". For example, a date entry of 12/01 will become 11/30 when decreasing the day part.
numberParts | array | [] (**Required**) | The array of NumberPart's that combine to create the full numeric entry.

### NumberPart

Name | Type | Defaults | Description
:--- | :--- | :--- | :---
length | int | null (**Required**) | The length of the numeric input.
maxValue | int<hr/>function | 10^length - 1 or Number.MAX_SAFE_INTEGER, whichever is smaller | The maximum numeric value allowed for input.<hr/>If a function is supplied, the function will receive all the number parts as an array parameter when being called.
minValue | int<hr/>function | 0 | The minimum numeric value allowed for input.<hr/>If a function is supplied, the function will receive all the number parts as an array parameter when being called.
prefix | string | "" | The prefix to the numeric input.
postfix | string | "" | The postfix to the numeric input.
snapToStep | bool | false | If true, setting the numeric value will snap it to the closest "step". If the numeric value is greater than the "maxValue", then the numeric value will overflow to the "minValue" and vice-versa.
step | int | 1 | The numeric unit to increase/decrease the numeric value.
toString | function | | Function that returns the formatted numeric input including the "prefix" and "postfix".
totalLength | function | | Function that returns the total length of the numeric value including the "prefix" and "postfix".
value | string | "" | The numeric value. If the value is less digits than "length", the display value will be prepadded with 0's to equal the specified length. For example, if the length is 4 and the value is "12", then the display value will be "0012".
<!--<table>
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Defaults</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>length</td>
    <td>int</td>
    <td>null (<strong>Required</strong>)</td>
    <td>The length of the numeric input.</td>
  </tr>
  <tr>
    <td rowspan="2">maxValue</td>
    <td>int</td>
    <td>10^length - 1 or Number.MAX_SAFE_INTEGER, whichever is smaller</td>
    <td>The maximum numeric value allowed for input.</td>
  </tr>
  <tr>
    <td>function</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>minValue</td>
    <td>int<br/>function</td>
    <td>0</td>
    <td>The minimum numeric value allowed for input.</td>
  </tr>
  <tr>
    <td>prefix</td>
    <td>string</td>
    <td>""</td>
    <td>The prefix to the numeric input.</td>
  </tr>
  <tr>
    <td>postfix</td>
    <td>string</td>
    <td>""</td>
    <td>The postfix to the numeric input.</td>
  </tr>
  <tr>
    <td>snapToStep</td>
    <td>bool</td>
    <td>false</td>
    <td>If true, setting the numeric value will snap it to the closest "step". If the numeric value is greater than the "maxValue", then the numeric value will overflow to the "minValue" and vice-versa.</td>
  </tr>
  <tr>
    <td>step</td>
    <td>int</td>
    <td>1</td>
    <td>The numeric unit to increase/decrease the numeric value.</td>
  </tr>
  <tr>
    <td>toString</td>
    <td>function</td>
    <td></td>
    <td>Function that returns the formatted numeric input including the "prefix" and "postfix".</td>
  </tr>
  <tr>
    <td>totalLength</td>
    <td>function</td>
    <td></td>
    <td>Function that returns the total length of the numeric value including the "prefix" and "postfix".</td>
  </tr>
  <tr>
    <td>value</td>
    <td>string</td>
    <td>""</td>
    <td>The numeric value. If the value is less digits than "length", the display value will be prepadded with 0's to equal the specified length. For example, if the length is 4 and the value is "12", then the display value will be "0012".</td>
  </tr>
</table>-->

## Examples
```javascript
$("#iNumberEntry").iNumberEntry({
  numberParts:[
    {
      length:3,
      prefix:"(",
      postfix:") ",
      value:"123"
    },
    {
      length:3,
      postfix:"-",
      value:"456"
    },
    {
      length:4,
      value:"7890"
    }
  ]
});
```
### Predefined Number Entries
#### iPhoneNumberEntry
```javascript
$("#iPhoneNumberEntry").iPhoneNumberEntry([NumberEntry]);
```
By default, this will display in the format (123) 456-7890. If you wish to change any of the prefixes or postfixes, you would need to supply the following to get a display of 123 456 7890:
```javascript
$("#iPhoneNumberEntry").iPhoneNumberEntry({
  numberParts: [
    {
      prefix: "",
      postfix: " "
    },
    {
      postfix: " "
    }
  ]
});
```
The last part can be ignored if no changes are being made, however, any previous parts would need to be supplied with a empty object notation, i.e. '{}', if the last part is being changed.
#### iDateNumberEntry
```javascript
$("#iDateNumberEntry").iDateNumberEntry(format, [NumberEntry]);
```
The first parameter is the format. The supported formats are as follows:

- mm/dd
- mm/dd/yy
- mm/dd/yyyy

You can supply additional options as well in the second parameter, same as above for iPhoneNumberEntry.
#### iTimeNumberEntry
```javascript
$("#iTimeNumberEntry").iTimeNumberEntry(format, [NumberEntry]);
```
The first parameter is the format. The supported formats are as follows:

- hh:mm
- hh:mm:ss

You can supply additional options as well in the second parameter, same as above for iPhoneNumberEntry.
#### iSocialSecurityNumberEntry
```javascript
$("#iSocialSecurityNumberEntry").iSocialSecurityNumberEntry([NumberEntry]);
```
By default, this will display in the format 123-45-6789. You can supply additional options as well in the second parameter, same as above for iSocialSecurityNumberEntry.
## Events
```javascript
$("#iNumberEntry").iNumberEntry().on('change.iNumberEntry', function(e) {
  console.log("The display value is " + e.value.displayValue);
  
  for (var i = 0; i < e.value.parts.length; i++)
  {
    console.log("The value at index " + i + " is " + e.value.parts[i]);
  }
});
```
## Acknowledgements
Inspiration for this plugin is thanks to Joris de Wit (@jdewit) and his implementation of the <a href="https://github.com/jdewit/bootstrap-timepicker">bootstrap-timepicker</a>.
