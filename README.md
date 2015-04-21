#  [![NPM version][npm-image]][npm-url] [![Build Status][travis-image]][travis-url] [![Dependency Status][daviddm-image]][daviddm-url]

> Small wrapper on top of Cross Origin postMessage

## Install

### Bower
```sh
$ bower install --save hermes-messenger
```

### Browserify
```sh
$ npm install --save hermes-messenger
```

## Docs

This exports or adds to `window.HermesMessenger` a constructor to create a new instance.

### Constructor
```js
var Hermes = require('hermes-messenger');
new Hermes(frame, origin);
```

* `frame` is the Iframe or Frame Node Element (e.g. `document.querySelector('iframe')`)
* `origin` is the url (with protocol) of the frame (e.g. `https://gojobhero.com`) or `*` for any origin

Look at [MDN postMessage](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage) for more info.


### Send
Send a messsage to the frame
```
hermes.send(data);
```

If you want to recieve a response pass a Node style callback with data.
```
hermes.send({ msg: 'Yay rainbows!', callback: function(err, resp) { } });
```


### Receive
Listen on the message event.

The function takes the `data` that was received and a `callback` if the sender wants a reply.

```
hermes.on('message', function(data) { });
```

You can check if you need to reply back this message by checking if a 2nd argument is passed, the callback.
```
hermes.on('message', function(data, callback) {
  if (callback) {
    cb('some err');
  }
});
```

## Usage

```js
var Hermes = require('hermes-messenger'); // If using Browserify
var Hermes = window.HermesMessenger;      // Also exports onto window

var hermes = new Hermes(document.querySelector('iframe'), '*');

// Send a message to an iframe
hermes.send({ message: 'Testing Rainbows!' });

// Send a message and wait for a response
hermes.send({
  message: 'How many rainbows?!',
  callback: function(err, data) {
  }
});

// Listen for messages
hermes.on('message', function(data) {
  
});

// Listen for messages and respond
hermes.on('message', function(data, cb) {
  var err = false;

  if (cb) {
    if (err) {
      cb('Error getting data'); // Send error
    } else {
      cb(null, 'All of the rainbows');
    }
  }
});
```

## Browser Compatibility

[Cross-document message](http://caniuse.com/#feat=x-doc-messaging)

For all versions of IE, the window must be either a Frame or Iframe. Popups won't work.

## Building

```sh
# creates browser files
$ gulp
```

## License

MIT © [JobHero](gojobhero.com)


[npm-image]: https://badge.fury.io/js/hermes-messenger.svg
[npm-url]: https://npmjs.org/package/hermes-messenger
[travis-image]: https://travis-ci.org/jobhero/hermes-messenger.svg?branch=master
[travis-url]: https://travis-ci.org/jobhero/hermes-messenger
[daviddm-image]: https://david-dm.org/jobhero/hermes-messenger.svg?theme=shields.io
[daviddm-url]: https://david-dm.org/jobhero/hermes-messenger