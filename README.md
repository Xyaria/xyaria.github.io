# CSVtoJSON
Convert .csv files into .json.  

### Features
- conversion to flat JSON or JSON Array
- conversion of string into primary type
- nested objects support
- keyed JSON support
- variable key/value support

### Usage
Download and open the `index.html`, or go to [xyaria.github.io](https://wyaria.github.io).  
Configure the app with the options on the right.  
Click on "Open file" and select your .csv.  

The conversion happens directly, you can then copy the result as text or download a .json file using the respective buttons.  

### Syntax
To fully use the app, there are a few special syntax to use in your .csv: 
- A column named `_key` will use its value as the key of each element
- A column named with several keys separated with a dot (`.`) with convert into successive objects
- A column named with at least one key and ending with `._key` will create a property named after its value
- A column named with at least one key and ending with `._value` will assign its value to the child property of the previous key
- A column containing a list of values separated by `|` will convert into an array

> :warning: in case of `_key` or `_value` missing...  
> If a `_key` does not have a `_value` counterpart, its value will be null, even if you have not included null values  
> If a `_value` does not have a `_key` counterpart, it will simply be ignored

### Example
|food.green.veggie|food.green.fruit|food.meat._key|food.meat._value|drink|
|---              |---             |---           |---             |---  |
|carrot           |apple           |beef          |100             |true |
|leek             |banana          |chicken       |180             |false|

```json
[{
  "food": {
    "green": {
      "veggie": "carrot",
      "fruit": "apple"
    },
    "meat": {
      "beef": 100
    }
  },
  "drink": true
},
{
  "food": {
    "green": {
      "veggie": "leek",
      "fruit": "banana"
    },
    "meat": {
      "chicken": 180
    }
  },
  "drink": false
}]
```

### Why ?
I've made this little thing while helping the making of another project, where I've been making a database of assets in JSON. For ease of use, I've complied informations into an spreadsheet with the intention of using an online converter to get a JSON.  
And I've been oh so surprise to see absolutely 0 converters allowing the automatic conversion into nested objects, or the use of variable key/value pair.  
There have been *one* [converter](https://www.convertcsv.com/csv-to-json.htm) which is super powerful and waaay more complete than my little one, but 1) I could not get the auto-nested object feature to work, and 2) the custom templates were a hassle to use, I've never understood the script behind to fully use them.  
So there I was, with my only strong langage being JavaScript, deciding to make one myself.  
At first very specific to my existing spreadsheet, I decided to make a generic program for the next ones. I ended up quite happy with the result, and so decided to put it up in here! I had needed it, someone else probably would too.  
So yeah, a little HTML page badly coded half-styled with quite an ugly script (according to my standards), but a standalone web app containing a useful program.