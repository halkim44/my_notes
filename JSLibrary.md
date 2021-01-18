# Javascript Libraries Notes

## Axios

a client HTTP API based on the XMLHttpRequest interface provided by browsers.

### Advantages over native Fetch API

- request and response interception
- streamlined error handling
- protection against XSRF
- support for upload progress
- response timeout
- the ability to cancel request
- support for older browsers
- automatic JSON data transformation

```js

axios({
  method: 'post',
  url: '/login',
  data: {
    firstName: 'Finn',
    lastName: 'Williams'
  }
});

// or the shorthands methods

axios.request(config)
axios.get(url[, config])
axios.delete(url[, config])
axios.head(url[, config])
axios.options(url[, config])
axios.post(url[, data[, config]])
axios.put(url[, data[, config]])
axios.patch(url[, data[, config]])
```

### Handling the response

```js
axios
  .post("/login", {
    firstName: "Finn",
    lastName: "Williams",
  })
  .then(
    (response) => {
      // these are all the value available in response
      console.log(response.data);
      console.log(response.status);
      console.log(response.statusText);
      console.log(response.headers);
      console.log(response.config);
    },
    (error) => {
      console.log(error);
    }
  ); // the first will be called if success, second if fail
```

### making simultaneous request

able to make multiple requests in parallel by passing an array of arguments to the `axios.all()`. this will returns a single Promise object that resolves only when all arguments passed as an array have resolved.

if any of the value rejects then the promise will immediately reject with the reason of the first promise that rejects.

`axios.spread()` same as `.all()` but used to unpack value from the response array.

### Sending custom headers

pass an object at the last arguments.

### Transform request and response

Axios automatically converts requests and responses to JSON. But it also allows you to override the default behavior and define a different transformation mechanism using `transformRequest` or `transformResponse`.

### Intercepting request and responses

with Http interception you can examine and change HTTP requests from your program to the server(useful for logging or authentication).

interceptors helps with cases where global config or custom instances might be too generic. Interceptors have the ability to change any object properties on the fly.

```js
// Add a request interceptor
axios.interceptors.request.use(function (config) {
  // Do something before request is sent, like we're inserting a timeout for only requests with a particular baseURL
  if (config.baseURL === 'https://axios-app.firebaseio.com/users.json') {
    config.timeout = 4000
  } else {
    return config
  }
  console.log (config)
    return config;
  }, function (error) {
  // Do something with request error
  return Promise.reject(error);
});

// Add a response interceptor
axios.interceptors.response.use(function (response) {
  // Do something with response data like console.log, change header, or as we did here just added a conditional behaviour, to change the route or pop up an alert box, based on the reponse status
  if (response.status === 200 || response.status 201) {
    router.replace('homepage') }
  else {
    alert('Unusual behaviour')
  }
  console.log(response)
  return response;
}, function (error) {
  // Do something with response error
  return Promise.reject(error);
});
```

### Client-side support for protection against XSRF

**Cross-site request forgery(XSRF)** ― is a method of attacking a web-hosted app in which the attacker disguises himself as a legal and trusted user to influence the interaction between the app and the user's browser.

axios is design to protect against XSRF by allowing you to embed additional authentication data when making requests.

```js
const options = {
  method: "post",
  url: "/login",
  xsrfCookieName: "XSRF-TOKEN",
  xsrfHeaderName: "X-XSRF-TOKEN",
};

// send the request
axios(options);
```

### Monitoring Post request progress

axios able to monitor request progress(especially when downloading or upload large file). we can make progress bar out of this using the Axios Progress bar.

### Canceling a request

using a cancel token, we can cancel a request. It was added to Axios in v1.5 and is based on the cancelable promises proposal.

### Global config

handles all application request using a standard configuration that is set through a default object that ships with axios.

this object contains

- **baseURL**
- **headers**
- **timeout** ― the point at which the request is aborted(milliseconds)
- **withCredentials** ― indicate whether or not cross-site Access-Control request should be made using credentials.
- **responseType** ― the type of data the server will return (there are many options beside `json`)
- **responseEncoding**
- **xsrfCookieName** ― the name of the cookie to use as a value for XSRF token.
- **xsrfHeaderName** ― the name of the HTTP header that carries the XSRF token value.
- **maxContentLength** ― max size of HTTP response content in bytes allowed
- **maxBodyLength** ― max size of the HTTP request content in bytes allowed

### Creating instances

is similar to a global config but scoped to specific components.
