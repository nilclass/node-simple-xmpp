Node Simple XMPP
================
Simple High Level NodeJS XMPP Library

Dependencies
------------
	sudo apt-get install libexpat1 libexpat1-dev libicu-dev

Install
-------
	npm install simple-xmpp

Example
-------
	var xmpp = require('simple-xmpp');

	xmpp.on('online', function() {
		console.log('Yes, I\'m connected!');
	});

	xmpp.on('chat', function(from, message) {
		xmpp.send(from, 'echo: ' + message);
	});

	xmpp.on('error', function(err) {
		console.error(err);
	});

	xmpp.on('subscribe', function(from) {
	if (from === 'a.friend@gmail.com') {
		xmpp.acceptSubscription(from);
		}
	});

	xmpp.connect({
	    jid         : username@gmail.com,
	    password    : password,
	    host        : 'talk.google.com',
	    port        : 5222
	});

	xmpp.subscribe('your.friend@gmail.com');
	// check for incoming subscription requests
	xmpp.getRoster();


Documentation
-------------

### Events

#### Online
Event emitted when successfully connected

	xmpp.on('online', function() {
		console.log('Yes, I\'m online');
	});

#### Chat
Event emitted when somebody sends a chat message to you

	xmpp.on('chat', function(from, message) {
		console.log('%s says %s', from, message);
	});

#### Buddy
Event emitted when state of the buddy on your chat list changes

	/**
		@param jid - is the id of buddy (eg:- hello@gmail.com)
		@param state - state of the buddy. value will be one of the following constant can be access via require('simple-xmpp').STATUS
			AWAY - Buddy goes away
		    DND - Buddy set its status as "Do Not Disturb" or  "Busy",
		    ONLINE - Buddy comes online or available to chat
		    OFFLINE - Buddy goes offline
	*/
	xmpp.on('buddy', function(jid, state) {
		console.log('%s is in %s state', jid, state);
	});
	
#### Buddy capabilities
Event emitted when a buddy's client capabilities are retrieved. Capabilities specify which additional
features supported by the buddy's XMPP client (such as audio and video chat). See 
[XEP-0115: Entity Capabilities](http://xmpp.org/extensions/xep-0115.html) for more information.

	xmpp.on('buddyCapabilities', function(jid, data) {
		// data contains clientName and features
		console.log(data.features);
	});

#### Stanza
access core stanza element when such received
Fires for every incoming stanza

	/**
		@param stanza - the core object
		xmpp.on('stanza', function(stanza) {
			console.log(stanza);
		});
	*/

### Methods

#### Send
Send Chat Messages

	/**
		@param to - Address to send (eg:- abc@gmail.com)
		@param message - message to be sent
	*/

	xmpp.send(to, message);

Send Friend requests

	/**
		@param to - Address to send (eg:- your.friend@gmail.com)
	*/
	xmpp.subscribe(to);

Accept Friend requests

	/**
		@param from - Address to accept (eg:- your.friend@gmail.com)
	*/
	xmpp.acceptSubscription(from);

Unsubscribe Friend

	/**
		@param to - Address to unsubscribe (eg:- no.longer.friend@gmail.com)
	*/
	xmpp.unsubscribe(to);

Accept unsubscription requests

	/**
		@param from - Address to accept (eg:- no.longer.friend@gmail.com)
	*/
	xmpp.acceptUnsubscription(from);

#### Probe
Probe the state of the buddy

	/**
		@param jid - Buddy's id (eg:- abc@gmail.com)
		@param state -  State of the buddy.  value will be one of the following constant can be access via require('simple-xmpp').STATUS
			AWAY - Buddy goes away
			DND - Buddy set its status as "Do Not Disturb" or  "Busy",
			ONLINE - Buddy comes online or available to chat
			OFFLINE - Buddy goes offline
	*/

	xmpp.probe(jid, function(state) {

	})

### Fields
Fields provided Additional Core functionalies

#### xmpp.conn
The underline connection object

	var xmpp = simpleXMPP.connect({});
	xmpp.conn; // the connection object

#### xmpp.Element
Underline XMPP Element class

	var xmpp = simpleXMPP.connect({});
	xmpp.Element; // the connection objec


### Guides

