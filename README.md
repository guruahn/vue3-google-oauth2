# DEPRECATED - no longer actively maintained
You can use [this plugin vue3-google-login](https://github.com/yobaji/vue3-google-login/) instead to have support for the new Google Identity Services JavaScript library.

# vue3-google-oauth2
Handling Google sign-in and sign-out for Vue3 applications. 

Please refer to [here](https://github.com/guruahn/vue-google-oauth2) for Vue2 applications.


![npm bundle size](https://img.shields.io/bundlephobia/minzip/vue3-google-oauth2.svg)
![GitHub](https://img.shields.io/npm/l/vue3-google-oauth2)
![vue3-google-oauth2](https://img.shields.io/npm/dt/vue3-google-oauth2.svg)


[Front-end Demo](https://github.com/guruahn/vue3-google-oauth2-front-sample)

## Installation
### Installation with npm
```
npm install vue3-google-oauth2
```

### Installation with yarn
```
yarn add vue3-google-oauth2
```

## Initialization
```javascript
import { createApp } from 'vue'
import App from './App.vue'
import GAuth from 'vue3-google-oauth2'
const app = createApp(App)

const gAuthOptions = { clientId: 'YOUR_CLIENT_ID', scope: 'email', prompt: 'consent', fetch_basic_profile: false }
app.use(GAuth, gAuthOptions)
```


## Options
| Property     | Type     | Required        | Description     |
|--------------|----------|-----------------|-----------------|
| clientId     | String   | Required.       | The app's client ID, found and created in the Google Developers Console. |
| scope        | String   | Optional.       | Default value is `profile email`. [Full list of scopes](https://developers.google.com/identity/protocols/googlescopes). |
| prompt       | String   | Optional.       | This value using for [authCode.](https://developers.google.com/api-client-library/javascript/reference/referencedocs#gapiauth2offlineaccessoptions) The possible values are `select_account` or `consent`. Default value is `select_account`. To get refresh token from auth code, use `consent`.|
| fetch_basic_profile       | Boolean   | Optional.       | If set to true, `email profile openid` will [be automatically added as scope](https://developers.google.com/identity/sign-in/web/sign-in). Default value is `true`. |

## Methods
| Property     | Description        | Type     |
|--------------|--------------------|----------|
| instance   | return of [gapi.auth2.getAuthInstance()](https://developers.google.com/identity/sign-in/web/reference#gapiauth2authresponse)   | Object |
| signIn       | function for sign-in | Function  |
| getAuthCode  | function for getting authCode | Function  |
| signOut      | function for sign-out | Function  |

## Reactivity
> We support **reactivity** by Provide/Injection. Refer to [sample project](https://github.com/guruahn/vue3-google-oauth2-front-sample).

| Property     | Description        | Type     |
|--------------|--------------------|----------|
| Vue3GoogleOauth.isInit   | it will return reactivity object value({isInit, isAuthorized})  | Object |
| Vue3GoogleOauth.isAuthorized   | it will return reactivity object value({isInit, isAuthorized})  | Object |

## Usages
Refer to [sample project](https://github.com/guruahn/vue3-google-oauth2-front-sample).


## Extra - Directly get `access_token` and `refresh_token` on Server-side
To get `access_token` and `refresh_token` in server side, the data for `redirect_uri` should be `postmessage`. `postmessage` is magic value for `redirect_uri` to get credentials without actual redirect uri.

### Curl
```
curl -d "client_id=YOUR_CLIENT_ID&\
  client_secret=YOUR_CLIENT_SECRET&\
  redirect_uri=postmessage&\
  grant_type=authorization_code&\
  code=YOUR_AUTH_CODE" https://accounts.google.com/o/oauth2/token
```

### Sample Code
- [Golang Sample Code](https://github.com/guruahn/vue-google-oauth2/blob/master/backend-samples/golang/main.go)
- [Python Sample Code](https://github.com/guruahn/vue-google-oauth2/blob/master/backend-samples/python/main.py)
- [Front Sample Code](https://github.com/guruahn/vue3-google-oauth2-front-sample)

## Additional Help
- [sample login page HTML file](https://github.com/guruahn/vue-google-oauth2/blob/master/sample.html).
- [Google API Client Libraries : Methods and Classes](https://developers.google.com/api-client-library/javascript/reference/referencedocs)
- If you are curious of how the entire Google sign-in flow works, please refer to the diagram below
![Google Sign-in Flow](https://developers.google.com/identity/sign-in/web/server_side_code_flow.png)


## FAQ
### The failure of initialization happens
You can check the brower console to check errors which occur during initialization.
The most of errors are from inproper setting of google oauth2 credentials setting in Google Developer Console.
After changing the settings, you have to do hard refresh to clear your caches.

