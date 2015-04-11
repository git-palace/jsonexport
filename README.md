# jsonexport
This module makes easy to convert JSON to CSV and its very customizable.

# Usage

Installation command is `npm install jsonexport`.

```javascript
var jsonexport = require('jsonexport');

jsonexport({lang: 'Node.js',module: 'jsonexport'}, {rowDelimiter: '|'}, function(err, csv){
    if(err) return console.log(err);
    console.log(csv);
});
```

## JSON Array Example

### Simple Array

#### Code

```javascript
var jsonexport = require('jsonexport');

var contacts = [{
    name: 'Bob',
    lastname: 'Smith'
},{
    name: 'James',
    lastname: 'David'
},{
    name: 'Robert',
    lastname: 'Miller'
},{
    name: 'David',
    lastname: 'Martin'
}];

jsonexport(contacts,function(err, csv){
    if(err) return console.log(err);
    console.log(csv);
});
```

#### Result

```
name;lastname
Bob;Smith
James;David
Robert;Miller
David;Martin
```

### Complex Array

#### Code

```javascript
var jsonexport = require('jsonexport');

var contacts = [{
   name: 'Bob',
   lastname: 'Smith',
   family: {
       name: 'Peter',
       type: 'Father'
   }
},{
   name: 'James',
   lastname: 'David',
   family:{
       name: 'Julie',
       type: 'Mother'
   }
},{
   name: 'Robert',
   lastname: 'Miller',
   family: null,
   location: [1231,3214,4214]
},{
   name: 'David',
   lastname: 'Martin',
   nickname: 'dmartin'
}];

jsonexport(contacts,function(err, csv){
    if(err) return console.log(err);
    console.log(csv);
});
```

#### Result

```
lastname;name;family.type;family.name;nickname;location
Smith;Bob;Father;Peter;;
David;James;Mother;Julie;;
Miller;Robert;;;;1231,3214,4214
Martin;David;;;dmartin;
```

## JSON Object Example

### Simple Object

#### Code

```javascript
var jsonexport = require('jsonexport');

var stats = {
    cars: 12,
    roads: 5,
    traffic: 'slow'
};

jsonexport(stats,function(err, csv){
    if(err) return console.log(err);
    console.log(csv);
});
```

#### Result

```
cars;12
roads;5
traffic;slow
```

### Complex Object

#### Code

```javascript
var jsonexport = require('jsonexport');

var stats = {
    cars: 12,
    roads: 5,
    traffic: 'slow',
    speed: {
        max: 123,
        avg: 20,
        min: 5
    },
    size: [10,20]
};

jsonexport(stats,function(err, csv){
    if(err) return console.log(err);
    console.log(csv);
});
```

#### Result

```
cars;12
roads;5
traffic;slow
speed.max;123
speed.avg;20
speed.min;5
size;10,20
```

## Customization

In order to get the most of out of this module, you can customize many parameters, check the list:

```
Option : Default Value
headerPathString: '.',
rowDelimiter: ';',
endOfLine: null,
mainPathItem: null,
arrayPathString: ',',
booleanTrueString: null,
booleanFalseString: null,
includeHeaders: true,
orderHeaders: true,
undefinedString: '',
verticalOutput: true,
handleString: null,
handleNumber: null,
handleBoolean: null,
handleDate: null,
handleArray: null,
handleObject: null
```
####Options

- `headerPathString` - `String` Used to create the propriety path, `contact.name`.
- `rowDelimiter` - `String` Change the file row delimiter, defaults to `;`.
- `endOfLine` - `String` Replace the OS default EOL.
- `mainPathItem` - `String` Every header will have the `mainPathItem` as the base.
- `arrayPathString` - `String` This is used to output primitive arrays in a single column, defaults to `,`
- `booleanTrueString` - `String` Will be used instead of `true`.
- `booleanFalseString` - `String` Will be used instead of `false`.
- `includeHeaders` - `Boolean` Set this option to false to hide the CSV headers.
- `orderHeaders` - `Boolean` By default the most used columns are shown first.
- `undefinedString` - `String` If you want to display a custom value for undefined strings, use this option.
- `verticalOutput` - `Boolean` Set this option to false to create a horizontal output for JSON Objects, headers in the first row, values in the second.
- `handleString` - `Function` Use this to customize all `Strings` in the CSV file.
- `handleNumber` - `Function` Use this to customize all `Numbers` in the CSV file.
- `handleBoolean` - `Function` Use this to customize all `Booleans` in the CSV file.
- `handleDate` - `Function` Use this to customize all `Dates` in the CSV file.
- `handleArray` - `Function` Use this to customize all `Arrays` in the CSV file.
- `handleObject` - `Function` Use this to customize all `Objects` in the CSV file.

### Handle Customization

Lets say you want to prepend a text to every string in your CSV file, how to do it?

```javascript
var jsonexport = require('jsonexport');

var options = {
    handleString: function(string, name){
        return 'Hey - ' + string;
    }
};

jsonexport({lang: 'Node.js',module: 'jsonexport'}, options, function(err, csv){
    if(err) return console.log(err);
    console.log(csv);
});
```

The output would be:

```
lang;Hey - Node.js
module;Hey - jsonexport
```
