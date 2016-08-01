# Vue Time Picker

A dropdown time picker for [Vue.js](http://vuejs.org/)

## Dependencies

Require: [Vue.js](http://vuejs.org/)

## Get Started

Step 1: Import the `vue-timepicker.vue`

```javascript
// ES6 import
import VueTimepicker from 'yoursrc/vue-timepicker.vue'

// Or, use require
var VueTimepicker = require('yoursrc/vue-timepicker.vue')
```

Step 2: Include VueTimepicker in your component

```javascript
var yourComponent = new Vue({
  components: {VueTimepicker},
  ...
})
```

Step 3: Then, you can introduce the `vue-timepicker` tag anywhere you like in your component's template

```html
<vue-timepicker></vue-timepicker>
```

## Usage

### Basic Usage

```html
<!-- Default to 24-Hour format HH:mm -->
<vue-timepicker></vue-timepicker>
```

### Customized Time Format

```html
<!-- Show seconds picker -->
<vue-timepicker format="HH:mm:ss"></vue-timepicker>

<!-- 12-hour format, with AM/PM picker -->
<vue-timepicker format="hh:mm A"></vue-timepicker>

<!-- 12-hour format, with seconds picker and am/pm picker -->
<vue-timepicker format="hh:mm:ss a"></vue-timepicker>
```

VueTimepicker will recognizes the following tokens in the format string

Section | Token | Output
------- | ----- | -------------
AM/PM   | A     | AM PM
        |       | a             | am pm
Hour    | H     | 0 1 ... 22 23
        |       | HH            | 00 01 ... 22 23
        |       | h             | 1 2 ... 11 12
        |       | hh            | 01 02 ... 11 12
        |       | k             | 1 2 ... 23 24
        |       | kk            | 01 02 ... 23 24
Minute  | m     | 0 1 ... 58 59
        |       | mm            | 00 01 ... 58 59
Second  | s     | 0 1 ... 58 59
        |       | ss            | 00 01 ... 58 59

> If not set, `format` string will be default to "HH:mm"

### Customized Picker interval

```html
<!-- Show minute picker's value in the form of 0, 5, 10, ... 55, 60 -->
<vue-timepicker :minute-interval="5"></vue-timepicker>

<!-- Show second picker's value in the form of 0, 10, 20, ... 50, 60 -->
<vue-timepicker :second-interval="10"></vue-timepicker>

<!-- Bind interval config with your own data variable -->
<vue-timepicker :minute-interval="yourMinuteInterval"></vue-timepicker>
```

**Note:** Please do remember to add the `:` or `v-bind:` sign before the interval properties

### Hide Clear Button

```html
<vue-timepicker hide-clear-button></vue-timepicker>
```

### Initalise Time Picker Value

```javascript
// e.g. If you want to assign "10:05:00" as the initial value of vue-timepicker
var yourComponent = new Vue({
  components: {VueTimepicker},
  data: function () {
    return {
      yourTimeValue: {
        HH: "10",
        mm: "05",
        ss: "00"
      },
      ...
    }
  },
  ...
})
```

```html
<!-- HTML -->
<vue-timepicker :time-value.sync="yourTimeValue" format="HH:mm:ss"></vue-timepicker>
```

### Get Time Picker's Current Value

**Method 1:** Read the two-way synced `time-value` variable

```html
<!-- In the last section, we've set the initial value (yourTimeValue) to "10:05:00" -->
<vue-timepicker :time-value.sync="yourTimeValue" format="HH:mm:ss"></vue-timepicker>
```

```javascript
// Then, open the dropdown picker and pick a new time.
// Like setting to "14:30:15" for example
// Check the value after that
console.log(this.yourTimeValue)
// outputs -> {HH: "14", mm: "30", ss: "15"}
```

**Method 2:** Listen to the `vue-timepicker-update` event

```javascript
// 1) Use `events`
var yourComponent = new Vue({
  components: {VueTimepicker},
  events: {
    'vue-timepicker-update': function (eventData) {
      // `eventData` includes the current value of vue-timepicker
      // Add your handler here
    },
    ...
  },
  ...
})

// Or, 2) Use `$on`
this.$on('vue-timepicker-update', function (eventData) {
  // `eventData` includes the current value of vue-timepicker
  // Your handler here
})
```

Unlike the sync `time-value`, which only returns the defined time format you provided in format string (`HH`, `mm` and `ss` in the above case), the `vue-timepicker-update` event will return **all** time format.

In the example above, when picker is set to "14:30:15" in HH:mm:ss format, `vue-timepicker-update` will return the following data:

```javascript
// `vue-timepicker-update` event data
{
  HH: "14",
  H: "14",
  hh: "14",
  a: "am",
  A: "AM",
  h: "14",
  kk: "14",
  k: "14",
  m: "30",
  mm: "30",
  s: "15",
  ss: "15"
}
```

Whereas the `time-value` will only return the data with defined tokens in format string

```javascript
// Previously defined format="HH:mm:ss"
// Hence, `time-value`'s synced variable (`yourTimeValue` in this case) returns:
{
  HH: "14",
  mm: "30",
  ss: "15"
}
```

### Props API

Prop              | Type      | Required | Default Value
----------------- | --------- | -------- | -------------
format            | _String_  | no       | "HH:mm"
minute-interval   | _Number_  | no       | _undefined_
second-interval   | _Number_  | no       | _undefined_
time-value        | _Object_  | no       | _undefined_
hide-clear-button | _Boolean_ | no       | false

## Help Developing

This is the very first version of `vue-timepicker` and includes ES6 solution only. Please fork and help developing

```bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

## License

[MIT](http://opensource.org/licenses/MIT)