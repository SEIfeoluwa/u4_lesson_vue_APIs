# Vue With Apis

![](https://miro.medium.com/max/700/1*P3ODlZMsFN3uCmnTY3smaA.png)

## Getting Started

- Fork and clone
- `npm install`
- Create a `.env` in the root of this project

## Overview

In this lesson, we'll learn how to interact with RESTful API's utilizing VueJS. We'll be utilizing the Open Weather Map api to build a small weather application. Like most other frameworks and libraries, Vue has a component lifecycle that allows us to control what happens when a component is rendered, updated, and removed from the DOM tree. We'll utilize these component lifecycle methods to trigger a request to retrieve weather data. We'll also be utilizing the browsers native Geolocation API to retrieve a users location in order to send our API requests.

## Vue Component Lifecycle Methods

VueJS provides us with a few component lifecycle methods also known as `hooks`:

- mounted
- created
- updated

and more...

We'll include a full list with each hooks description in the [Resources](#Resources) section down below.

Each method has it's own responsibility in a components lifecycle. Today we'll be using `mounted` to trigger our API calls.

### Mounted

`mounted` is a hook that is triggered when a component get's loaded onto the DOM tree. This is one of the hooks that runs right when our component loads, which makes it a great candidate to trigger an API call.

## Scaffolding Our Project

Let's start by creating a few pieces of state in our `App.vue`. We'll create:

- `dailyWeather: []`,
- `currentWeather: null`

Next we'll set up a method called `getCurrentWeather` that accepts a parameter of `coords`. This method should be `async`

```js
methods :{
    async getCurrentWeather(coords){}
}
```

Now we'll import `axios` at the top of our `script` section and create a variable to access our api key:

```js
import axios from 'axios'
const API_KEY = process.env.VUE_APP_WEATHER_KEY
```

Inside of our `getCurrentWeather` method, we'll set up a `GET` request to the following endpoint:

`https://api.openweathermap.org/data/2.5/onecall?lat=${coords.latitude}&lon=${coords.longitude}&units=imperial&appid=${API_KEY}`

**Note: Make sure to utilize ` when inputting this url**

We'll plug in a few query parameters into this url using the template literal syntax:

```js
const res = await axios.get(
  `https://api.openweathermap.org/data/2.5/onecall?lat=${coords.latitude}&lon=${coords.longitude}&units=imperial&appid=${API_KEY}`
)
```

Finally we'll set the `current` property from the response to the `currentWeather` state:

```js
this.currentWeather = res.data.current
```

## Resources

- [Native Browser Geolocation Api](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API/Using_the_Geolocation_API)
- [Openweather Api](https://openweathermap.org/api)
- [Symbol HexCodes](https://www.toptal.com/designers/htmlarrows/math/degree-sign/)
- [Vue Lifecycle Hooks](https://v3.vuejs.org/api/options-lifecycle-hooks.html)
