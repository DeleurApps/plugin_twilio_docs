# twilio: Plugin API Docs

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [Library](http://docs.coronalabs.com/api/type/Library.html)
| __Corona Store__     | [twilio](http://store.coronalabs.com/plugin/twilio)
| __Sample Code__      | [View Sample on GitHub](https://github.com/DeleurApps/plugin_twilio_sample)
| __Platforms__        | Android

## Overview

The twilio plugin can be used in your [Corona](https://coronalabs.com/products/corona-sdk/) project. This enables you do integrate the [Twilio Client](https://www.twilio.com/docs/api/client) into your application. Twilio Client extends the power of Twilio beyond the traditional telephone network. With Twilio Client you are no longer restricted to building Twilio applications that rely on interacting with traditional telephones.

You setup your device and establish a connection to Twilio. Audio from your device's microphone is sent to Twilio, and Twilio plays audio through your device's speakers, like on a normal phone call. But with Twilio Client, your device need not be a phone.

When you initiate a connection using Twilio Client, you're not connecting to another phone directly. Rather, you're connecting to Twilio and instructing Twilio to fetch TwiML from your server to handle the connection. This is analogous to the way Twilio handles incoming calls from a real phone.

## Getting Started

Because Twilio Client connections aren't made to a specific phone number, Twilio relies on a [Twilio Application](https://www.twilio.com/docs/api/rest/applications) within your account to determine how to interact with your server. A Twilio Application is just a convenient way to store a set of URLs, like the VoiceUrl and SmsUrl on a phone number, but without locking them to a specific phone number. This makes Twilio Applications perfect for handling connections from Twilio Client (which is actually why we created them in the first place).

So when your device initiates a Twilio Client connection to Twilio, a request is made to the VoiceUrl property of an Application within your account. You specify the Application you're connecting to with a [Capability Token](https://www.twilio.com/docs/client/capability-tokens). Twilio uses the TwiML response from its request to that Application's VoiceUrl to direct what happens with the Client connection.

To get started you will need your Twilio Account SID and Auth Token. You can find these in your [Account Dashboard](https://www.twilio.com/user/account/). If you don't have an account, you can sign up for a free [trial account](https://www.twilio.com/try-twilio). You will also need to set up a server that serves your TwiML application. You can find a sample server in this [guide](https://www.twilio.com/docs/quickstart/php/ios-client/setup)


### Corona Store Activation

In order to use this plugin, you must activate the plugin at the [Corona Store](http://store.coronalabs.com/plugin/PLUGIN_NAME).


### SDK

When you build using the Corona Simulator, the server automatically takes care of integrating the plugin into your project.

All you need to do is add an entry into a `plugins` table of your `build.settings`. The following is an example of a minimal `build.settings` file:

``````
settings =
{
	plugins =
	{
		-- key is the name passed to Lua's 'require()'
		["plugin.twilio"] =
		{
			-- required
			publisherId = "com.deleurapps",
		},
	},
}
``````

### Android

Before calling [twilio.initialize()](#initialize), you must request the `android.permission.RECORD_AUDIO` permission for android. To do so,call the following function:

```lua
native.showPopup( "requestAppPermission", {appPermission = "android.permission.RECORD_AUDIO", urgency = "Critical", } )
```

## Syntax

	local twilio = require "plugin.twilio"

## Functions Overview

[initialize()](#initialize)

[shutdown()](#shutdown)

[isInitialized()](#isinitialized)

[createDevice()](#createdevice)

[release()](#release)

[listen()](#listen)

[unlisten()](#unlisten)

[connect()](#connect)

[accept()](#accept)

[ignore()](#ignore)

[reject()](#reject)

[disconnect()](#disconnect)

[disconnectAll()](#disconnectall)

[sendDigits()](#senddigits)

[getCapabilityToken()](#getcapabilitytoken)

[updateCapabilityToken()](#updatecapabilitytoken)

[getCapabilities()](#getcapabilities)

[getState()](#getstate)

[setIncomingSoundEnabled()](#setincomingsoundenabled)

[isIncomingSoundEnabled()](#isincomingsoundenabled)

[setOutgoingSoundEnabled()](#setoutgoingsoundenabled)

[isOutgoingSoundEnabled()](#isoutgoingsoundenabled)

[setDisconnectSoundEnabled()](#setdisconnectsoundenabled)

[isDisconnectSoundEnabled()](#isdisconnectsoundenabled)

[getConnectionParameters()](#getconnectionrarameters)

[getConnectionState()](#getconnectionstate)

[setMuted()](#setmuted)

[isMuted()](#ismuted)

[setReceivePresenceEvents()](#setreceivepresenceevents)

## Events Overview

[onTwilioInitialization](#ontwilioinitialization)

[onCreateDeviceError](#oncreatedeviceerror)

[onStartListening](#onstartlistening)

[onStopListening](#onstoplistening)

[onPresenceChanged](#onpresencechanged)

[onConnecting](#onconnecting)

[onConnected](#onconnected)

[onDisconnected](#ondisconnected)

[onIncomingConnection](#onincomingconnection)

## Project Configuration

### Corona Store Activation

In order to use this plugin, you must activate the plugin at the [Corona Store](http://store.coronalabs.com/plugin/twilio).

### SDK

When you build using the Corona Simulator, the server automatically takes care of integrating the plugin into your project.

All you need to do is add an entry into a `plugins` table of your `build.settings`. The following is an example of a minimal `build.settings` file:

``````
settings =
{
	plugins =
	{
		-- key is the name passed to Lua's 'require()'
		["plugin.twilio"] =
		{
			-- required
			publisherId = "com.deleurapps",
		},
	},
}
``````

## Functions

#### initialize()

##### Overview

Initialize the Twilio Client SDK.

##### Syntax

	twilio.initialize()

#### shutdown()

##### Overview

Shuts down the Twilio Client SDK.

This will terminate all connections, release all Device objects, and release any resources used by the SDK.

##### Syntax

	twilio.shutdown()

#### isInitialized()

##### Overview

Determines if the Twilio Client SDK has been initialized or not. Returns `true` or `false`

If you expect your application to run in the background when the user has switched to other applications, you will want to check the return value of this method on startup. The Android OS may have killed your application due to memory pressure, but the SDK may still be running in the background.

##### Syntax

	twilio.isInitialized()

#### createDevice()

##### Overview

Create and initialize a new Device object.

If the incoming capabilities are defined, then the device will automatically begin listening for incoming connections.

##### Syntax

	twilio.createDevice(capabilityToken)

###### capabilityToken (required)
_[String](https://docs.coronalabs.com/api/type/String.html)._ A signed JSON Web Token that defines the features available to the Device. These may be created using the Twilio Helper Libraries available at http://www.twilio.com. The capabilities are used to begin listening for incoming connections and provide the default parameters used for establishing outgoing connections. Please visit [Capability Tokens](http://www.twilio.com/docs/client/capability-tokens) for more information.

#### release()

##### Overview

Shuts down and releases the Device. This will terminate all connections and release resources immediately.

##### Syntax

	twilio.release()

#### listen()

##### Overview

Start listening for incoming connections.

The Device will automatically listen for incoming connections on calls to twilio.createDevice() or twilio.updateCapabilityToken() if the token allows.

This method only needs to be called if twilio.unlisten() was previously called.

##### Syntax

	twilio.listen()

#### unlisten()

##### Overview

Stop listening for incoming connections.

This could be used for a "silence" mode on the your Android application, for instance.

This method will do nothing if the Device is currently not listening, either because of a previous call to twilio.unlisten() or because the Device has not been granted the incoming capability.

##### Syntax

	twilio.unlisten()

#### connect()

##### Overview

Creates a new connection to the Twilio application specified in the capability token of the Device.

Parameters are passed to the application unmodified.

##### Syntax

	twilio.connect(params)

###### params (optional)
_[Table](https://docs.coronalabs.com/api/type/Table.html)._ An optional table containing parameters for the outgoing connection that get passed to your Twilio Application. These parameters are merged with any parameters supplied in the Capability Token. If there are any key collisions with the two Maps, the value(s) from the Capability Map will take precedence.

#### accept()

##### Overview

Accepts an incoming connection request.

When an incoming connection is received, calling this method will accept the incoming connection.

##### Syntax

	twilio.accept()

#### ignore()

##### Overview

Ignores an incoming connection request.

The caller will receive no notification that the call was ignored.

When an incoming connection is received, calling ignore will close the incoming connection request and the connection may not be accepted.

##### Syntax

	twilio.ignore()

#### reject()

##### Overview

Rejects an incoming connection request.

The caller may receive a notification that the call was rejected.

When an incoming connection is received, notifying the caller that the call was rejected.

##### Syntax

	twilio.reject()

#### disconnect()

##### Overview

Disconnect the connection.

##### Syntax

	twilio.disconnect()

#### disconnectAll()

##### Overview

Disconnects all current connections associated with the Device.

This a convenience routine that disconnects all current incoming and outgoing connections, including pending incoming connections.

##### Syntax

	twilio.disconnectAll()

#### sendDigits()

##### Overview

Send a string of digits over the connection.

##### Syntax

	twilio.sendDigits(digits)

###### digits (required)
_[String](https://docs.coronalabs.com/api/type/String.html)._ a String of one or more valid digits and optional 'w' chars. Valid digits are '0' - '9', '*', '#', and 'w'. Each 'w' will cause a 500 ms pause between digits sent. If any invalid character is present, no digits will be sent.

#### getCapabilityToken()

##### Overview

Retrieves the capability token originally passed to twilio.createDevice().

##### Syntax

	twilio.getCapabilityToken()

#### updateCapabilityToken()

##### Overview

Updates the capabilities of the Device.

There may be circumstances when the defined capabilities have expired or need to change. For example, the Device may enter the State because the capabilities have expired. In these cases, the capabilities will need to be updated. If the device is currently listening for incoming connections, it will restart the listening process (if permitted) using these updated capabilities.

Existing connections are not affected by updating the capability token.

##### Syntax

	twilio.updateCapabilityToken(capabilityToken)

###### capabilityToken (required)
_[String](https://docs.coronalabs.com/api/type/String.html)._ The new capability token string.

#### getCapabilities()

##### Overview

Current capabilities of the Device. Returns _[table](https://docs.coronalabs.com/api/type/Table.html)_

##### Syntax

	twilio.getCapabilities()

##### Properties

###### INCOMING

_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ Indicates whether the device can receive incoming calls.

###### OUTGOING

_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ Indicates whether the device can make outgoing calls.

###### EXPIRATION

_[String](https://docs.coronalabs.com/api/type/String.html)._ Represents the time the device's capability token expires (number of seconds relative to the UNIX epoch).

###### ACCOUNT_SID

_[String](https://docs.coronalabs.com/api/type/String.html)._ Represents the account SID.

###### APPLICATION_SID

_[String](https://docs.coronalabs.com/api/type/String.html)._ Represents the application SID used when making an outgoing call. Only present if OUTGOING is also present with a true value.

###### APPLICATION_PARAMETERS

_[Table](https://docs.coronalabs.com/api/type/Table.html)._ Parameters that are sent to the Twilio Application with each outgoing connection.

###### CLIENT_NAME

_[String](https://docs.coronalabs.com/api/type/String.html)._ Represents the client name that should be used for incoming calls.

#### getState()

##### Overview

Retrieves the current state of the device. Returns a _[string](https://docs.coronalabs.com/api/type/String.html)_. Possible values are `OFFLINE`, `READY`, and `BUSY`.

##### Syntax

	twilio.getState()

#### setIncomingSoundEnabled()

##### Overview

Set whether the default Twilio sound should be played for an incoming connection.

By default, twilio.isIncomingSoundEnabled() is `true`.

##### Syntax

	twilio.setIncomingSoundEnabled(bool)

###### bool (required)
_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ `true` to enable, `false` to disable

#### isIncomingSoundEnabled()

##### Overview

Return whether the default Twilio sound should be played for an incoming connection. Returns a _[boolean](https://docs.coronalabs.com/api/type/Boolean.html)_.

The default value is `true`.

##### Syntax

	twilio.isIncomingSoundEnabled()

#### setOutgoingSoundEnabled()

##### Overview

Set whether the default Twilio sound should be played for an outgoing connection.

By default, twilio.isIncomingSoundEnabled() is `true`.

##### Syntax

	twilio.setOutgoingSoundEnabled(bool)

###### bool (required)
_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ `true` to enable, `false` to disable

#### isOutgoingSoundEnabled()

##### Overview

Return whether the default Twilio sound should be played for an outgoing connection. Returns a _[boolean](https://docs.coronalabs.com/api/type/Boolean.html)_.

The default value is `true`.

##### Syntax

	twilio.isOutgoingSoundEnabled()

#### setDisconnectSoundEnabled()

##### Overview

Set whether the default Twilio sound should be played when a connection is disconnected either normally or due to an error.

The disconnected sound will not be played if the connection is ignored or rejected.

By default, `twilio.isDisconnectSoundEnabled()` is `true`.

##### Syntax

	twilio.setDisconnectSoundEnabled(bool)

###### bool (required)
_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ `true` to enable, `false` to disable

#### isDisconnectSoundEnabled()

##### Overview

Return whether the default Twilio sound should be played when a connection is disconnected either normally or due to an error. Returns a _[boolean](https://docs.coronalabs.com/api/type/Boolean.html)_.

The disconnected sound will not be played if the connection is ignored or rejected.

The default value is true.

##### Syntax

	twilio.isDisconnectSoundEnabled()

#### getConnectionParameters()

##### Overview

Retrieves the set of application parameters associated with this connection. Returns a _[table](https://docs.coronalabs.com/api/type/Table.html)_.

Incoming connection parameters are defined by set of values described by the constants listed below.

Outgoing connection parameters are defined by the union of optional application parameters specified in the Capability Token and any additional parameters specified when the twilio.connect() method is called.

##### Syntax

	twilio.getConnectionParameters()

##### Properties

###### From

_[String](https://docs.coronalabs.com/api/type/String.html)._ Representa the calling party. If the caller is a telephone, it will be in the E.164 format. If the caller is another Twilio Client, it will be in a URI format "client:name".

###### To

_[String](https://docs.coronalabs.com/api/type/String.html)._ Represents the client name of the called party. This is in a URI format "client:name".

###### AccountSID

_[String](https://docs.coronalabs.com/api/type/String.html)._ Represents the account id making the incoming call.

###### APIVersion

_[String](https://docs.coronalabs.com/api/type/String.html)._ Represents the version of the Twilio API used in the server application.

###### CallSID

_[String](https://docs.coronalabs.com/api/type/String.html)._ Represents a unique identifier for the incoming call.

#### getConnectionState()

##### Overview

Retrieves the current state of the connection. Returns a _[string](https://docs.coronalabs.com/api/type/String.html)_. Possible values are `PENDING`, `CONNECTING`, `CONNECTED`, and `DISCONNECTED`.

##### Syntax

	twilio.getConnectionState()

#### setMuted()

##### Overview

Mutes or unmutes the microphone's audio for the connection.

##### Syntax

	twilio.setMuted(bool)

###### bool (required)
_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ `true` to mute, `false` to unmute

#### isMuted()

##### Overview

Reports whether the microphone's audio for the connection is muted. Returns a _[boolean](https://docs.coronalabs.com/api/type/Boolean.html)_.

##### Syntax

	twilio.isMuted()

#### setReceivePresenceEvents()

##### Overview

Sets whether or not the application wants to receive presence events.

Since bandwidth and battery life can both be precious resources on a mobile device, you may not want to incur the extra overhead of receiving and processing presence notifications.

##### Syntax

	twilio.setReceivePresenceEvents(bool)

###### bool (required)
_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ `true` to enable, `false` to disable

## Events

#### onTwilioInitialization

Called after [twilio.initialize()](#initialize) has resolved.

##### Properties

###### event.name

_[String](https://docs.coronalabs.com/api/type/String.html)._ "twilioEvent"

###### event.type

_[String](https://docs.coronalabs.com/api/type/String.html)._ "onTwilioInitialization"

###### event.isError

_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ Value indicating whether an error occurred.

###### event.error

_[String](https://docs.coronalabs.com/api/type/String.html)._ If event.isError is `true`, this is a string value stating the reason.

#### onCreateDeviceError

Called if there is an error after [twilio.createDevice()](#createDevice) is called.

##### Properties

###### event.name

_[String](https://docs.coronalabs.com/api/type/String.html)._ "twilioEvent"

###### event.type

_[String](https://docs.coronalabs.com/api/type/String.html)._ "onCreateDeviceError"

###### event.isError

_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ Value indicating whether an error occurred.

###### event.error

_[String](https://docs.coronalabs.com/api/type/String.html)._ If event.isError is `true`, this is a string value stating the reason.

#### onStartListening

Called when the Device has started listening for incoming connections.

##### Properties

###### event.name

_[String](https://docs.coronalabs.com/api/type/String.html)._ "twilioEvent"

###### event.type

_[String](https://docs.coronalabs.com/api/type/String.html)._ "onStartListening"

#### onStopListening

Called when the Device has stopped listening for incoming connections.

##### Properties

###### event.name

_[String](https://docs.coronalabs.com/api/type/String.html)._ "twilioEvent"

###### event.type

_[String](https://docs.coronalabs.com/api/type/String.html)._ "onStopListening"

###### event.isError

_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ Value indicating whether an error occurred.

###### event.error

_[String](https://docs.coronalabs.com/api/type/String.html)._ If event.isError is `true`, this is a string value stating the reason.

###### event.errorCode

_[Number](https://docs.coronalabs.com/api/type/String.html)._ If event.isError is `true`, this is the error code that pinpoints the reason. For a list of error codes and their meanings, see http://www.twilio.com/docs/client/errors.

#### onPresenceChanged

Called when the presence status for one or more other clients has changed.

When the device is ready, it is invoked as clients become available or unavailable.

A client is considered available even if another call is in progress.

When your client disconnects the onStopListening event will be invoked, and when the device reconnects this method will be called again for every available online client.

##### Properties

###### event.name

_[String](https://docs.coronalabs.com/api/type/String.html)._ "twilioEvent"

###### event.type

_[String](https://docs.coronalabs.com/api/type/String.html)._ "onPresenceChanged"

###### event.clientName

_[String](https://docs.coronalabs.com/api/type/String.html)._ The client name for which the event applies.

###### event.isAvailable

_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ Whether or not the client specified by name is currently connected to Twilio services for the account.

#### onConnecting

Called for a newly-created Connection when it is connecting to your Twilio application.

When this occurs, Connection is in the `CONNECTING` state.

##### Properties

###### event.name

_[String](https://docs.coronalabs.com/api/type/String.html)._ "twilioEvent"

###### event.type

_[String](https://docs.coronalabs.com/api/type/String.html)._ "onConnecting"

#### onConnected

Called after the Connection has successfully connected to your Twilio application.

Note that this does not necessarily mean your application has executed successfully; it only indicates that the connection has been established.

When this occurs the Connection will be in the `CONNECTED` state.

##### Properties

###### event.name

_[String](https://docs.coronalabs.com/api/type/String.html)._ "twilioEvent"

###### event.type

_[String](https://docs.coronalabs.com/api/type/String.html)._ "onConnected"

#### onDisconnected

Called after the Connection has been disconnected, ignored, or rejected by either party or when an error occurs.

After this callback has been called, it is safe to assume that the connection is no longer connected.

When this occurs the Connection will be in the `DISCONNECTED` state.

##### Properties

###### event.name

_[String](https://docs.coronalabs.com/api/type/String.html)._ "twilioEvent"

###### event.type

_[String](https://docs.coronalabs.com/api/type/String.html)._ "Properties"

###### event.isError

_[Boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ Value indicating whether an error occurred.

###### event.error

_[String](https://docs.coronalabs.com/api/type/String.html)._ If event.isError is `true`, this is a string value stating the reason.

###### event.errorCode

_[Number](https://docs.coronalabs.com/api/type/String.html)._ If event.isError is `true`, this is the error code that pinpoints the reason. For a list of error codes and their meanings, see http://www.twilio.com/docs/client/errors.

#### onIncomingConnection

##### Properties

###### event.name

_[String](https://docs.coronalabs.com/api/type/String.html)._ "twilioEvent"

###### event.type

_[String](https://docs.coronalabs.com/api/type/String.html)._ "onIncomingConnection"

###### event.params

_[Table](https://docs.coronalabs.com/api/type/Table.html)._ Table indicating the connection parameters of an incoming connection.

## Support

More support is available from the Deleur Apps team:

* [E-mail](mailto://deleurapps@gmail.com)
* [Corona Forums](https://forums.coronalabs.com/forum/654-corona-store-plugins/)

## Thanks

* Plugin sponsored by [Spring Morning Software](http://springmorning.nl)

