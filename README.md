<p align="center">
  <img src="../assets/banner.png" />
</p>
<p align=center>
  <img src="https://img.shields.io/badge/Made%20with-Javascript-%23f7df1e?style=for-the-badge&color=F1C40F" alt="fully in javascript"/>
  <img src="https://img.shields.io/github/stars/ReinaRPG?style=for-the-badge&color=3498DB"/>
  <a href="https://choosealicense.com/licenses/mit/">
  <a href="https://reinarpg.com">
    <img src="https://img.shields.io/badge/new-website-9B59B6?style=for-the-badge" alt="Chat"/>
  </a>
</p>
<h3 align=center>ReinaRPG is browser based voxel sandbox MMORPG</h3>
<br>

# net-browserify

`net` module for browserify, with a websocket server proxy.

# Guide
Just require this module or map this module to the `net` module with [Browserify](https://github.com/substack/node-browserify).
```
$ npm install net-browserify
```

You can set a custom proxy address if you want to:
```js
var net = require('net');

// Optionaly, set a custom proxy address
// (defaults to the current host & port)
net.setProxy({
	hostname: 'example.org',
	port: 42
});

// Use the net module like on a server
var socket = net.connect({
	host: 'google.com',
	port: 80
});

socket.on('connect', function () {
	console.log('Connected to google.com!');
});
```

### For the server

```js
var express = require('express');
var netApi = require('net-browserify');

// Create our app
var app = express();

app.use(netApi());

// Start the server
var server = app.listen(3000, function() {
	console.log('Server listening on port ' + server.address().port);
});
```

You can also specify some options:
```js
app.use(netApi({
	allowOrigin: '*', // Allow access from any origin
	to: [ // Restrict destination
		{ host: 'example.org', port: 42 }, // Restrict to example.org:42
		{ host: 'example.org' }, // Restrict to example.org, allow any port
		{ port: 42 }, // Restrict to port 42 only, allow any host
		{ host: 'bad.com', blacklist: true } // Blacklist bad.com
		// And so on...
	]
}));
```
