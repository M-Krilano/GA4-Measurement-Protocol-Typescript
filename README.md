# Google Analytics GA4 Measurement Protocol Library
This library provides an interface for sending data to Google Analytics 4 properties using Measurement Protocol.

**NOTE** Google Analytics 4 is in Alpha as of the latest update

## Use

BSD 3-Clause license can be found in ./LICENSE

## Contact

analytics-help@adswerve.com

## Compatible with

- Node.js version 8+
- es2015

## Installation

```sh
npm install -s ga4-mp
```

## Setup

```js
ga4mp = require('ga4-mp');
let ga4 = ga4mp.createClient(apiSecret, measurementId, clientId);
```

The required credentials for sending events to GA4 are made up by the following:

|Credential|Description|
|---|---|
|measurement_id|The identifier for a Data Stream. Found in the Google Analytics UI under:  **Admin** > **Data Streams** > **choose your stream** > **Measurement ID**|
|api_secret|Generated throught the Google Analytics UI. To create a new secret, navigate in the Google Analytics UI to: **Admin** > **Data Streams** > **choose your stream** > **Measurement Protocol** > **Create**|
|client_id|[Get your Google API client ID](https://developers.google.com/identity/one-tap/web/guides/get-google-api-clientid)|


## Send Hits to GA4 Account

You can send events to GA4 as they happen or batch them to be sent at another time of your choosing.

### Send immediately

```js
ga4.send(<events>);
```

### Send later

```js
ga4.send(<events>, true); // Set postpone flag
ga4.flushBuffer();  // Send all postponed events
```

### Events passed to send()

```js
var events = [
  {
    name : 'add_to_cart',
    params : {
      currency : 'USD',
       items : ['Pokémon cards'],
       value : "4.99"
    }
  },
  {
    name : 'app_update',
    params : {
      previous_app_version : '4.6'
    }
  }
]
```

Events are expected to be passed to the send() function within an array and matching the object schema found in the [Google Analytics 4 documentation](https://developers.google.com/analytics/devguides/collection/protocol/ga4/sending-events?client_type=gtag#send_an_event).

## Additional Features

### Set and unset a constant parameter

```js
ga4.setConstantParam(key, value);  // Set a constant
ga4.unsetConstantParam(key); // Remove a constant
```

Set custom dimensions/metrics, country codes, etc. for all outgoing events.  You can unset them too.

### Output connection details

```js
ga4.readClientInfo();
```
