# Functions

## __initialize()__

### Overview

Initialize the Twilio Client SDK.

### Syntax

	twilio.initialize()

## __shutdown()__

### Overview

Shuts down the Twilio Client SDK.

This will terminate all connections, release all Device objects, and release any resources used by the SDK.

### Syntax

	twilio.shutdown()

## __isInitialized()__

### Overview

Determines if the Twilio Client SDK has been initialized or not. Returns `true` or `false`

If you expect your application to run in the background when the user has switched to other applications, you will want to check the return value of this method on startup. The Android OS may have killed your application due to memory pressure, but the SDK may still be running in the background.

### Syntax

	twilio.isInitialized()

## __createDevice()__

### Overview

Create and initialize a new Device object.

If the incoming capabilities are defined, then the device will automatically begin listening for incoming connections.

### Syntax

	twilio.createDevice(capabilityToken)

#### capabilityToken (required)
_[String](https://docs.coronalabs.com/api/type/String.html)._ A signed JSON Web Token that defines the features available to the Device. These may be created using the Twilio Helper Libraries available [here](http://www.twilio).com. The capabilities are used to begin listening for incoming connections and provide the default parameters used for establishing outgoing connections. Please visit [Capability Tokens](http://www.twilio.com/docs/client/capability-tokens) for more information.

## __release()__

### Overview

Shuts down and releases the Device. This will terminate all connections and release resources immediately.

### Syntax

	twilio.release()

## __listen()__

### Overview

Start listening for incoming connections.

The Device will automatically listen for incoming connections on calls to twilio.createDevice() or twilio.updateCapabilityToken() if the token allows.

This method only needs to be called if twilio.unlisten() was previously called.

### Syntax

	twilio.listen()

## __unlisten()__

### Overview

Stop listening for incoming connections.

This could be used for a "silence" mode on the your Android application, for instance.

This method will do nothing if the Device is currently not listening, either because of a previous call to twilio.unlisten() or because the Device has not been granted the incoming capability.

### Syntax

	twilio.unlisten()

## __connect()__

### Overview

Creates a new connection to the Twilio application specified in the capability token of the Device.

Parameters are passed to the application unmodified.

### Syntax

	twilio.connect(params)

#### params (optional)
_[Table](https://docs.coronalabs.com/api/type/Table.html)._ An optional table containing parameters for the outgoing connection that get passed to your Twilio Application. These parameters are merged with any parameters supplied in the Capability Token. If there are any key collisions with the two Maps, the value(s) from the Capability Map will take precedence.

## __accept()__

### Overview

Accepts an incoming connection request.

When an incoming connection is received, calling this method will accept the incoming connection.

### Syntax

	twilio.accept()

## __ignore()__

### Overview

Ignores an incoming connection request.

The caller will receive no notification that the call was ignored.

When an incoming connection is received, calling ignore will close the incoming connection request and the connection may not be accepted.

### Syntax

	twilio.ignore()

## __reject()__

### Overview

Rejects an incoming connection request.

The caller may receive a notification that the call was rejected.

When an incoming connection is received, notifying the caller that the call was rejected.

### Syntax

	twilio.reject()

## __disconnect()__

### Overview

Disconnect the connection.

### Syntax

	twilio.disconnect()

## __disconnectAll()__

### Overview

Disconnects all current connections associated with the Device.

This a convenience routine that disconnects all current incoming and outgoing connections, including pending incoming connections.

### Syntax

	twilio.disconnectAll()

## __sendDigits()__

### Overview

Send a string of digits over the connection.

### Syntax

	twilio.sendDigits(digits)

#### digits (required)
_[String](https://docs.coronalabs.com/api/type/String.html)._ a String of one or more valid digits and optional `'w'` chars. Valid digits are `'0'` - `'9'`, `'*'`, `'#'`, and `'w'`. Each `'w'` will cause a 500 ms pause between digits sent. If any invalid character is present, no digits will be sent.

## __getCapabilityToken()__

### Overview

Retrieves the capability token originally passed to twilio.createDevice().

### Syntax

	twilio.getCapabilityToken()

## __updateCapabilityToken()__

### Overview

Updates the capabilities of the Device.

There may be circumstances when the defined capabilities have expired or need to change. For example, the Device may enter the State because the capabilities have expired. In these cases, the capabilities will need to be updated. If the device is currently listening for incoming connections, it will restart the listening process (if permitted) using these updated capabilities.

Existing connections are not affected by updating the capability token.

### Syntax

	twilio.updateCapabilityToken(capabilityToken)

#### capabilityToken (required)
_[String](https://docs.coronalabs.com/api/type/String.html)._ The new capability token string.

## __getCapabilities()__

### Overview

Current capabilities of the Device. Returns _[table](https://docs.coronalabs.com/api/type/Table.html)_

### Syntax

	twilio.getCapabilities()

### _Properties_

#### INCOMING

_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ Indicates whether the device can receive incoming calls.

#### OUTGOING

_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ Indicates whether the device can make outgoing calls.

#### EXPIRATION

_[String](https://docs.coronalabs.com/api/type/String.html)._ Represents the time the device's capability token expires (number of seconds relative to the UNIX epoch).

#### ACCOUNT_SID

_[String](https://docs.coronalabs.com/api/type/String.html)._ Represents the account SID.

#### APPLICATION_SID

_[String](https://docs.coronalabs.com/api/type/String.html)._ Represents the application SID used when making an outgoing call. Only present if OUTGOING is also present with a true value.

#### APPLICATION_PARAMETERS

_[Table](https://docs.coronalabs.com/api/type/Table.html)._ Parameters that are sent to the Twilio Application with each outgoing connection.

#### CLIENT_NAME

_[String](https://docs.coronalabs.com/api/type/String.html)._ Represents the client name that should be used for incoming calls.

## __getState()__

### Overview

Retrieves the current state of the device. Returns a _[string](https://docs.coronalabs.com/api/type/String.html)_. Possible values are `OFFLINE`, `READY`, and `BUSY`.

### Syntax

	twilio.getState()

## __setIncomingSoundEnabled()__

### Overview

Set whether the default Twilio sound should be played for an incoming connection.

By default, twilio.isIncomingSoundEnabled() is `true`.

### Syntax

	twilio.setIncomingSoundEnabled(bool)

#### bool (required)
_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ `true` to enable, `false` to disable

## __isIncomingSoundEnabled()__

### Overview

Return whether the default Twilio sound should be played for an incoming connection. Returns a _[boolean](https://docs.coronalabs.com/api/type/Boolean.html)_.

The default value is `true`.

### Syntax

	twilio.isIncomingSoundEnabled()

## __setOutgoingSoundEnabled()__

### Overview

Set whether the default Twilio sound should be played for an outgoing connection.

By default, twilio.isIncomingSoundEnabled() is `true`.

### Syntax

	twilio.setOutgoingSoundEnabled(bool)

#### bool (required)
_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ `true` to enable, `false` to disable

## __isOutgoingSoundEnabled()__

### Overview

Return whether the default Twilio sound should be played for an outgoing connection. Returns a _[boolean](https://docs.coronalabs.com/api/type/Boolean.html)_.

The default value is `true`.

### Syntax

	twilio.isOutgoingSoundEnabled()

## __setDisconnectSoundEnabled()__

### Overview

Set whether the default Twilio sound should be played when a connection is disconnected either normally or due to an error.

The disconnected sound will not be played if the connection is ignored or rejected.

By default, `twilio.isDisconnectSoundEnabled()` is `true`.

### Syntax

	twilio.setDisconnectSoundEnabled(bool)

#### bool (required)
_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ `true` to enable, `false` to disable

## __isDisconnectSoundEnabled()__

### Overview

Return whether the default Twilio sound should be played when a connection is disconnected either normally or due to an error. Returns a _[boolean](https://docs.coronalabs.com/api/type/Boolean.html)_.

The disconnected sound will not be played if the connection is ignored or rejected.

The default value is true.

### Syntax

	twilio.isDisconnectSoundEnabled()

## __getConnectionParameters()__

### Overview

Retrieves the set of application parameters associated with this connection. Returns a _[table](https://docs.coronalabs.com/api/type/Table.html)_.

Incoming connection parameters are defined by set of values described by the constants listed below.

Outgoing connection parameters are defined by the union of optional application parameters specified in the Capability Token and any additional parameters specified when the twilio.connect() method is called.

### Syntax

	twilio.getConnectionParameters()

### _Properties_

#### From

_[String](https://docs.coronalabs.com/api/type/String.html)._ Representa the calling party. If the caller is a telephone, it will be in the E.164 format. If the caller is another Twilio Client, it will be in a URI format "client:name".

#### To

_[String](https://docs.coronalabs.com/api/type/String.html)._ Represents the client name of the called party. This is in a URI format "client:name".

#### AccountSID

_[String](https://docs.coronalabs.com/api/type/String.html)._ Represents the account id making the incoming call.

#### APIVersion

_[String](https://docs.coronalabs.com/api/type/String.html)._ Represents the version of the Twilio API used in the server application.

#### CallSID

_[String](https://docs.coronalabs.com/api/type/String.html)._ Represents a unique identifier for the incoming call.

## __getConnectionState()__

### Overview

Retrieves the current state of the connection. Returns a _[string](https://docs.coronalabs.com/api/type/String.html)_. Possible values are `PENDING`, `CONNECTING`, `CONNECTED`, and `DISCONNECTED`.

### Syntax

	twilio.getConnectionState()

## __setMuted()__

### Overview

Mutes or unmutes the microphone's audio for the connection.

### Syntax

	twilio.setMuted(bool)

#### bool (required)
_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ `true` to mute, `false` to unmute

## __isMuted()__

### Overview

Reports whether the microphone's audio for the connection is muted. Returns a _[boolean](https://docs.coronalabs.com/api/type/Boolean.html)_.

### Syntax

	twilio.isMuted()

## __setReceivePresenceEvents()__

### Overview

Sets whether or not the application wants to receive presence events.

Since bandwidth and battery life can both be precious resources on a mobile device, you may not want to incur the extra overhead of receiving and processing presence notifications.

### Syntax

	twilio.setReceivePresenceEvents(bool)

#### bool (required)
_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ `true` to enable, `false` to disable

