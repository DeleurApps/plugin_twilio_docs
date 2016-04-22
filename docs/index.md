# Welcome

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

## Getting Started

Because Twilio Client connections aren't made to a specific phone number, Twilio relies on a [Twilio Application](https://www.twilio.com/docs/api/rest/applications) within your account to determine how to interact with your server. A Twilio Application is just a convenient way to store a set of URLs, like the VoiceUrl and SmsUrl on a phone number, but without locking them to a specific phone number. This makes Twilio Applications perfect for handling connections from Twilio Client (which is actually why we created them in the first place).

So when your device initiates a Twilio Client connection to Twilio, a request is made to the VoiceUrl property of an Application within your account. You specify the Application you're connecting to with a [Capability Token](https://www.twilio.com/docs/client/capability-tokens). Twilio uses the TwiML response from its request to that Application's VoiceUrl to direct what happens with the Client connection.

To get started you will need your Twilio Account SID and Auth Token. You can find these in your [Account Dashboard](https://www.twilio.com/user/account/). If you don't have an account, you can sign up for a free [trial account](https://www.twilio.com/try-twilio). You will also need to set up a server that serves your TwiML application. You can find a sample server in this [guide](https://www.twilio.com/docs/quickstart/php/android-client/setup)

### Syntax

```lua
local twilio = require "plugin.twilio"
```

### Event Listener

To receive events created by the twilio plugin, you have to create a runtime event listener:

```lua
local function twilioListener(event)
	print(event.type)
end

Runtime:addEventListener("twilioEvent", twilioListener)
```

### Creating a device

To create a twilio device that will send/receive calls, you must initialize the SDK, fetch the [Capability Token](https://www.twilio.com/docs/client/capability-tokens) and create a device.

```lua
local function networkListener( event )
    if ( event.isError ) then
        print( "Network error: ", event.response )
    else
        local capabilityToken = event.response
        twilio.createDevice(capabilityToken)
    end
end

twilio.initialize()
network.request( "TOKEN_SERVICE_URL", "GET", networkListener )
```

### Making Outgoing Calls

After successfully creating a device, you can start making outgoing calls. To do so add the following function call, where `params` is a table you want passed to your TwiML Application. Check out [this guide](https://www.twilio.com/docs/quickstart/php/android-client/twilio-application) to see how a TwiML Application works.

```lua
local contact = "CONTACT_NUMBER"
local params = {To = contact}
twilio.connect(params)
```

### Receiving Incoming Calls

To listen for incoming calls and accept/ignore/reject them, add the following code to your `twilioListener`:

```lua
local function twilioListener(event)
	print(event.type)
	if event.type == "onIncomingConnection" then
		twilio.accept()
		-- twilio.ignore()
		-- twilio.reject()
	end
end

Runtime:addEventListener("twilioEvent", twilioListener)
```
