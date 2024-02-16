![Status](https://img.shields.io/badge/Status-Experimental-yellow)

# Client Requests

An Omnis Studio remote object to perform client-side requests via fetch API

###  How to build

The library is stored in JSON format in this repository. Check out the repository and use Omnis Studio 11 or newer to `Create project library from JSON`.

### How to use

The `requests` remote object is everything you need from the library, you could copy this into your existing application library.

You can either use the callbacks details below, or inherit from `requests` and override the `$completed` and `$error` methods.

To start making requests, use the `$fetch(cURL[, cMethod='GET'])` method.


### Callbacks

`$setCallbackForm(cRemoteFormName, cMethodName)` instructs the object to callback the method passed in `cMethodName` on the remote form with the name passed in `cRemoteForm`.

Your callback method will receives two parameters: `callbackMethod(pData, pSuccessful)` where `pSuccessful` is **false** when the request caught an error, `pData` is either the result of a successful request, or the error.

Note: all instantiated remote forms are iterated to find the remote form with the name passed in `cRemoteForm`, therefore if your remote form has not been instantiated yet, you will miss the callback.

---

`$callbackinst(pInstance)` instructs the object to callback `$completed(pData)` or `$error(pError)` on the instances passed in `pInstance`.

---

`$completed(pData)` is the object's default callback for a successful. Override this method when inheriting in order to access your request's data.

---

`$error(pError)` is the object's default callback for a caught error. Override this method when inheriting in order to access the error.


### Callback example

```
# Client executed method

Do requests.$setCallbackForm('callbackSample_setCallbackForm','$callback')
Do requests.$fetch('https://api.ipify.org?format=json')
```

```
# Client executed method named $callback in remote form callbackSample_setCallbackForm

JavaScript:console.log(pData);
```
