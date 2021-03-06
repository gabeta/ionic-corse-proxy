# ionic-corse-proxy

If you are two part to your project:

* The Api Server hosted at `http://localhost:8080`
* The Ionic web server hosted at `http://localhost:8100`

If you run **Ionic serve** on your navigator. You will come across this error:

`XMLHttpRequest cannot load http://localhost:8080/api/. No 'Access-Control-Allow-Origin' header is present on the requested resource. Origin 'http://localhost:8100' is therefore not allowed access.`

There are this error because by default browers do not accept cross domain.
This error is not valid for your mobile.

### Create a proxy ###

For resolve this error you must create proxy. go to `ionic.project` and add this code :

```javascript
 "proxies": [
    {
      "path": "/api",
      "proxyUrl": "http://localhost:8080/api"
    }
  ]
```

Example `ionic.project`:

```javascript
{
  "name": "proxy-example",
  "app_id": "",
  "proxies": [
	  {
	     "path": "/api",
	     "proxyUrl": "http://localhost:8080/api"
      }
  ]
}
```

Now you must use `http://localhost:8100/api` in your project for call your backend API `http://localhost:8080/api`


### Angular Constant ###

If you want to use angular constant API_URL.

```javascript
angular.module('starter', ['ionic'])
.constant(
	'API_URL' : 'http://localhost:8100/api'
  )
```
Once this is done, you can use the constant anywhere in your app, by including

Example with factory :

```javascript
angular.module('starter', ['ionic'])

.factory('Api', function($http, API_URL) {

  return {
  
    getApiData: function() {
    	return $http.get(API_URL + '/post')
      			.then(function(data) {
        			return data;
      			});
    };

  };

})

```

### Automating URL with gulp ###

You must add two task on your `gulpfile`

* change_url : run this task for change `http://localhost:8080/api` to `http://localhost:8100/api` 
* rollback_url : run this task for remove `http://localhost:8100/api` to `http://localhost:8080/api`

Firstly, your must install node module `replace` => `npm install --save replace`

```javascript

// ReplaceFiles is the js containing your API_URL. I use app.js for this example

var replace = require('replace');
var replaceFiles = ['./www/js/app.js']; 

gulp.task('change_url', function() {
  return replace({
    regex: "http://localhost:8080/api",
    replacement: "http://localhost:8100/api",
    paths: replaceFiles,
    recursive: false,
    silent: false,
  });
})

gulp.task('rollback_url', function() {
  return replace({
    regex: "http://localhost:8100/api",
    replacement: "http://localhost:8080/api",
    paths: replaceFiles,
    recursive: false,
    silent: false,
  });
})

```

#Enjoy !!!!#