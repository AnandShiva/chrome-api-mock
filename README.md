# Welcome to Chrome API Mock

This Library is intended to Mock the Chrome global variable in your tests with sensible default values and utilities for setting the values returned by the chrome API's. 

**Advantages** 

 - Zero dependency npm module.  
 - Framework Agonistic 
 - All API mocks have default values and work out of the box. 
 - Ability to set your own implementation to API. 
 - Supports All Chrome API's; No need to mock each API's separately. 
 - Living module; All future API mocks will be added and supported. 

# Installing

run either:
**npm run chrome-api-mock --dev**
or
**yarn add chrome-api-mock --dev**

In tests you can do 

const  chromeMock = require('chrome-api-mock')
global.chrome = chromeMock.getChromeInstance();

## Jest Specific Implementation

If you are using jest for tests chrome-api-mock can give more flexibility and power
You can also add global chrome variable throughout the test so that you need not set *global.chrome* in individual tests. 

[Jest Docs - Setting Global Variable](https://jestjs.io/docs/en/configuration#globals-object) gives more information. 

When using jest.config.js to set the configurations, use this
``` 
// jest.config.js
const chromeMock = require(‘chrome-api-mock’)
globals: {
	chrome: chromeMock.getChromeInstance(),
},
```
Or if you are using package.json to store jest configuration, use below snippet example
``` 
// package.json
const chromeMock = require(‘chrome-api-mock’)
jest: {
	globals: {
		chrome: chromeMock.getChromeInstance(),
	}
}

```



## Add Custom return values to Chrome API's. 

The following functions allow us to set values which chrome API should return. 
By default all API mocks return empty object. 

- setCookie
``` 
// Usage test.js
const exampleModule = require('../src/example.js')
const chromeMock = require(‘chrome-api-mock’)
test('sample test file', ()=>{
	global.chrome = chromeMock.getChromeInstance();
	chromeMock.setStorage({key1:'value1'})
	chrome.storage.get('key1', function(value){
		assert(value,'value1') // test passes. 
	})
})
```
| Function | Usage  |
|--|--|
| getChromeInstance  | get's the structured Chrome Object which can be set global scope |
|setCookies|Accepts an Array of cookies which are returned by *chrome.cookies.get*|
|setStorage|Accepts an Object representing the storage object which are returned by *chrome.storage.get*|
|setRuntimeSendMessage|Accepts a function which replaces the chrome.runtime.sendMessage function in source code|
