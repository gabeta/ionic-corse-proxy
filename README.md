# ionic-corse-proxy

If you are two part to your project:

* The Api Server hosted at `http://localhost:8080`
* The Ionic web server hosted at `http://localhost:8100`

If you run **Ionic serve** on your navigator. You will come across this error:

`XMLHttpRequest cannot load http://localhost:8080/api/. No 'Access-Control-Allow-Origin' header is present on the requested resource. Origin 'http://localhost:8100' is therefore not allowed access.`

There are this error because by default browers do not accept cross domain.
This error is not valid for your mobile.

For resolve this error you must create proxy. go to `ionic.project`

