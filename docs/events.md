# Events

## __onTwilioInitialization__

Called after [twilio.initialize()](#initialize) has resolved.

### _Properties_

#### __event.name__

_[String](https://docs.coronalabs.com/api/type/String.html)._ "twilioEvent"

#### __event.type__

_[String](https://docs.coronalabs.com/api/type/String.html)._ "onTwilioInitialization"

#### __event.isError__

_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ Value indicating whether an error occurred.

#### __event.error__

_[String](https://docs.coronalabs.com/api/type/String.html)._ If event.isError is `true`, this is a string value stating the reason.

## __onCreateDeviceError__

Called if there is an error after [twilio.createDevice()](#createDevice) is called.

### _Properties_

#### __event.name__

_[String](https://docs.coronalabs.com/api/type/String.html)._ "twilioEvent"

#### __event.type__

_[String](https://docs.coronalabs.com/api/type/String.html)._ "onCreateDeviceError"

#### __event.isError__

_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ Value indicating whether an error occurred.

#### __event.error__

_[String](https://docs.coronalabs.com/api/type/String.html)._ If event.isError is `true`, this is a string value stating the reason.

## __onStartListening__

Called when the Device has started listening for incoming connections.

### _Properties_

#### __event.name__

_[String](https://docs.coronalabs.com/api/type/String.html)._ "twilioEvent"

#### __event.type__

_[String](https://docs.coronalabs.com/api/type/String.html)._ "onStartListening"

## __onStopListening__

Called when the Device has stopped listening for incoming connections.

### _Properties_

#### __event.name__

_[String](https://docs.coronalabs.com/api/type/String.html)._ "twilioEvent"

#### __event.type__

_[String](https://docs.coronalabs.com/api/type/String.html)._ "onStopListening"

#### __event.isError__

_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ Value indicating whether an error occurred.

#### __event.error__

_[String](https://docs.coronalabs.com/api/type/String.html)._ If event.isError is `true`, this is a string value stating the reason.

#### __event.errorCode__

_[Number](https://docs.coronalabs.com/api/type/String.html)._ If event.isError is `true`, this is the error code that pinpoints the reason. For a list of error codes and their meanings, see [Twilio Errors](http://www.twilio.com/docs/client/errors).

## __onPresenceChanged__

Called when the presence status for one or more other clients has changed.

When the device is ready, it is invoked as clients become available or unavailable.

A client is considered available even if another call is in progress.

When your client disconnects the onStopListening event will be invoked, and when the device reconnects this method will be called again for every available online client.

### _Properties_

#### __event.name__

_[String](https://docs.coronalabs.com/api/type/String.html)._ "twilioEvent"

#### __event.type__

_[String](https://docs.coronalabs.com/api/type/String.html)._ "onPresenceChanged"

#### __event.clientName__

_[String](https://docs.coronalabs.com/api/type/String.html)._ The client name for which the event applies.

#### __event.isAvailable__

_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ Whether or not the client specified by name is currently connected to Twilio services for the account.

## __onConnecting__

Called for a newly-created Connection when it is connecting to your Twilio application.

When this occurs, Connection is in the `CONNECTING` state.

### _Properties_

#### __event.name__

_[String](https://docs.coronalabs.com/api/type/String.html)._ "twilioEvent"

#### __event.type__

_[String](https://docs.coronalabs.com/api/type/String.html)._ "onConnecting"

## __onConnected__

Called after the Connection has successfully connected to your Twilio application.

Note that this does not necessarily mean your application has executed successfully; it only indicates that the connection has been established.

When this occurs the Connection will be in the `CONNECTED` state.

### _Properties_

#### __event.name__

_[String](https://docs.coronalabs.com/api/type/String.html)._ "twilioEvent"

#### __event.type__

_[String](https://docs.coronalabs.com/api/type/String.html)._ "onConnected"

## __onDisconnected__

Called after the Connection has been disconnected, ignored, or rejected by either party or when an error occurs.

After this callback has been called, it is safe to assume that the connection is no longer connected.

When this occurs the Connection will be in the `DISCONNECTED` state.

### _Properties_

#### __event.name__

_[String](https://docs.coronalabs.com/api/type/String.html)._ "twilioEvent"

#### __event.type__

_[String](https://docs.coronalabs.com/api/type/String.html)._ "Properties"

#### __event.isError__

_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ Value indicating whether an error occurred.

#### __event.error__

_[String](https://docs.coronalabs.com/api/type/String.html)._ If event.isError is `true`, this is a string value stating the reason.

#### __event.errorCode__

_[Number](https://docs.coronalabs.com/api/type/String.html)._ If event.isError is `true`, this is the error code that pinpoints the reason. For a list of error codes and their meanings, see [Twilio Errors](http://www.twilio.com/docs/client/errors).

## __onIncomingConnection__

### _Properties_

#### __event.name__

_[String](https://docs.coronalabs.com/api/type/String.html)._ "twilioEvent"

#### __event.type__

_[String](https://docs.coronalabs.com/api/type/String.html)._ "onIncomingConnection"

#### __event.params__

_[Table](https://docs.coronalabs.com/api/type/Table.html)._ Table indicating the connection parameters of an incoming connection.

