
# NeoSocket Client - Javascript

NeoSocket Client is simple javascript library to manage your [NeoSocket(PHP)](https://github.com/mzohaibnaz/neosocket) connections on client side. but still this library can be used for client-side to any socket. :)

## Installation

  - Using NPM
 
```sh
$ npm install ns-jsclient
```
  - Vanilla JS File

> $ Download neosocket-client.js file and add on your project

## How to use
  - [Initializing](#create-object-of-class)
  - [Listening events](#read-data-from-server)
  -  - [Listen to all messages](#read-all-messages-with-raw-data)
  - [Sendign data](#send-data-to-server)
  - [Terminate Connection](#terminate-connection)
  - [Example](#example)

##### for npm you need to import library before using it
```js
//import for npm
import NeoSocket from "./neosocket-client";
```

##### create object of class
NeoSocket take url as a parameter.
default value of url param is: ws://localhost:6940/echo
```js
// create object of class 
// with default url of socket
let ns = new NeoSocket();
// with url
let ns = new NeoSocket("ws://localhost:444/test-socket");
```

#### Read data from server
###### # catch events from server
```js
// using ns.on method for catching events
// take 2 params 1st event time 2nd callback function
ns.on("event-type", (data) => {
    // do something with data
});
```

###### # onconnect and disconnect events with server
```js
// this event (connected) is called when connected is estanlished with server
ns.on("connected", () => {
    alert("you are successfully connected with server!")
});
// this event (disconnected) is called when connected is estanlished
ns.on("disconnected", () => alert("you are disconnected!"));
```

###### # read all messages with raw data
```js
// this event (nsraw) is called whenever there is data from server
// use this event for dealing other server-side library if you are not using neosocket(PHP) library
ns.on("nsraw", (data) => {
    
});
```

#### Send data to server
###### # use event() method before send method to select event type
```js
// send data to server with event-type `defualt`
ns.send("hello server");

//send data to server with specific event-type
ns.event("test").send("hello server on event-type test");
```

####  Terminate connection
```js
ns.dimiss();
```

# Example
on method returns current object of class so you can make chain of your code like example below.

> Note: that example below is for [NeoSocket(PHP)](#x) library which allow you to transfer data with event types. if you are using other server-side library use `nsraw` event-type to read messages.
```js
// create object
var  ns  =  new  NeoSocket();
// on successfully connected
ns.on("connected", () => {
	alert("you are successfully connected!")
}).on("message", (data) => {
	alert("data received from server! : "+  data);
	// send data to server with event type `bye`
	ns.event("bye").send("bye server!");
}).on("disconnected", () =>  alert("you are disconnected!"));
```
# License
[MIT](https://choosealicense.com/licenses/mit/)