# homebridge-fritz
[![NPM Version](https://img.shields.io/npm/v/homebridge-fritz.svg)](https://www.npmjs.com/package/homebridge-fritz)
[![Build status](https://travis-ci.org/andig/homebridge-fritz.svg?branch=master)](https://travis-ci.org/andig/homebridge-fritz)
[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=HGD5E9L28HQHC)


Homebridge platform plugin for FRITZ!Box.

This plugin exposes:

  - Wlan guest access switch
  - Fritz!DECT outlets (100, 200, 210)
  - Fritz!Powerline outlets (510, 540)
  - Comet!DECT thermostats


## Installation

Follow the homebridge installation instructions at [homebridge](https://www.npmjs.com/package/homebridge).

Install this plugin globally:

```
npm install -g homebridge-fritz
```

Add platform to `config.json`, for configuration see below.


## Configuration

```
{
  "platforms": [
    {
      "platform": "Fritz!Box",
      "name": "My FritzBox",
      "username": "<username>",
      "password": "<password>",
      "url": "http://fritz.box",
      "interval": 60,
      "options": {
        "strictSSL": false
      }
    }
  ]
}

```

The `url` and `interval` settings are optional:

  - `url`: Fritz!Box address
  - `interval`: polling interval for updating accessories if state was changed outside homebringe

To enable debugging run homebridge with `-D` option:

    homebridge -D


## Common Issues / Frequently Asked Questions

  1. homebridge-fritz can't login to the FritzBox
  
    Some users have reported that logging into the FritzBox internally via `https` fails. This seems to be caused by the FritzApp *occupying* the same port.
    In this case you can connect internally via `http` or use the external IP.

    `Fritz!Box platform login failed` messages can be caused by invalid login data or wrong url.

    Log messages if the form of:

        { error: { [Error: self signed certificate] code: 'DEPTH_ZERO_SELF_SIGNED_CERT' }

    indicate that there are SSL security problems- most likely due to self-signed certificates. Use the `"strictSSL": false` option to disable the respective check.

  
  2. homebridge-fritz is not able to update my thermostat
  
    Current FritzBox firmwares seem to ignore API updates when the thermostat has been key-locked. 
    No workaround available- please contact AVM to change this behaviour or don't use the locking mechanism.


  3. homebridge-fritz can login but not update thermostat battery charge

    Battery charge is not an API function. That means that the user must have access to FritzBox administration, not only to the SmartHome API in order to use this functionality. 
    Update your Fritz!Box user accordingly. 


## Acknowledgements

  - Original non-working fritz accessory https://github.com/tommasomarchionni/homebridge-FRITZBox
  - Platform implementation inspired by https://github.com/rudders/homebridge-platform-wemo.
