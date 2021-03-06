ng-ovh
======

Angular service for the [OVH](https://api.ovh.com) API.

  - Simple to use
  - Well documented
  - Only 1.9KB minified and gzipped!

The OVH API Console is available [here](https://api.ovh.com/console).


Installation
------------

You can download it with Bower:
```bash
$ bower install ng-ovh --save
```
And include the script in your html:
```html
<script src="components/ng-ovh/ng-ovh.min.js"></script>
```


Configuration
-------------

Simply add the dependency in your Angular app, like this:

```javascript
var myApp = angular.module('myApp', [
    'ngOvh'    // Require the ngOvh module here
]);
```

After that, you can configure it via the OvhProvider:

```javascript
myApp.config(function (OvhProvider) {

    // Set the Application Key (AK):
    OvhProvider.setAppKey('YOUR_APPLICATION_KEY');

    // Set the Application Secret (AS):
    OvhProvider.setAppSecret('YOUR_APPLICATION_SECRET');

    // [... other options]

});
```

#### Options

* **setAppKey**("AK") : Set the Application Key (AK).
* **setAppSecret**("AS") : Set the Application Secret (AS).
* setConsumerKey("CK") : Set the Consumer Key (CK).
* setBaseUrl("URL") : Set the API base URL.
* setAccessRules([{ ... }]) : Set the access rules.

The Application Key (AK) and the Application Secret (AS) is mandatory.

#### Get an Application Key (AK) and an Application Secret (AS)

In order to use the API, you need to create a third party application in OVH.
Go to [this link](https://eu.api.ovh.com/createApp/), and follow the steps. It will give you an AK and an AS to use for your application.

You can find more informations [here](https://api.ovh.com/g934.first_step_with_api).


Usage
-----

All functions (except 'isLogged') returns a `promise` (with success and error). You can catch it like the angular way, e.g.:

```javascript
Ovh.get('/me').then(function (infos) {
    // Success!
    // The param contains all the datas.
}, function (error) {
    // Error!
    // The param contains the traditional angular error.
});
```

#### Functions

* **login([urlToRedirect])**
```javascript
Ovh.login('http://www.example.com/home');
```
Log the user (request a new credential).
It will redirect the user to the OVH API login page.
When logged, user will be redirected to the given URL (or current location if omitted).

The token (the "Consumer Key" ("CK")) will be stored into the _localStorage_.

* **logout()**
```javascript
Ovh.logout();
```
Log out the user (expire current credential).

* **get(url, [config])**
* **post(url, [config])**
* **put(url, [config])**
* **delete(url, [config])** (aliases: **del**, **remove**)
```javascript
Ovh.get('/me');
Ovh.post('/domain/zone/{zoneName}/record', {
    params : {
        zoneName  : 'example.com'    // 'zoneName' will be automatically replaced in the url!
    },
    data : {
        fieldType : 'A',
        target    : '192.168.1.1'
    }
});
Ovh.put('/me', {
    data : {
        firstname : 'Bobobo-bo',
        name      : 'Bo-bobo'
    }
});
Ovh.delete('/me/sshKey/{keyName}', {
    params : {
        keyName : 'mypublickey'    // 'keyName' will be automatically replaced in the url!
    }
});
```
The param `config` is the same than Angular $http (see doc [here](https://docs.angularjs.org/api/ng/service/$http#usage)).

Note that the `resolve` promise returns directly the datas.

* **getSchema(schemaPath)**
```javascript
Ovh.getSchema('/me');
```
Get specific schema from API (here "/me").

* **getModels(schemaPath, [modelsName])**
```javascript
Ovh.getModels('/me', 'nichandle.CountryEnum');
```
Get all or a specific Models from API (here "/me", "nichandle.CountryEnum"). If second param is omitted, it returns all the Models.

* **isLogged()**
```javascript
Ovh.isLogged();
```
Return `true` if user is connected.



Examples
--------

You can find examples in the "examples" folder.


License
-------

MIT


Note
----

This library is not maintained by OVH.

