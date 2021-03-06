[![Build Status](https://secure.travis-ci.org/planetk/homebridge-netatmo.png?branch=master)](http://travis-ci.org/planetk/homebridge-netatmo)
Is this plugin useful for you? Please buy me a beer ...
[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=7ZGEPWHG5UH6S)

# homebridge-netatmo

This is a plugin for homebridge. It's a working implementation for several netatmo devices:

* **netatmo weather station** fully supported
* **netatmo thermostat** base functionality supported
* **netatmo welcome** currently under development

# Installation

1. Install homebridge using: npm install -g homebridge
2. Install this plugin using: npm install -g homebridge-netatmo
3. Update your configuration file. See sample-config.json in this repository for a sample. 

# Configuration

Configuration sample:

```
"platforms": [
        {
            "platform": "netatmo",
            "name": "netatmo platform",
            "ttl": 5,
            "auth": {
    	        "client_id": "XXXXX Create at https://dev.netatmo.com/",
                "client_secret": "XXXXX Create at https://dev.netatmo.com/",
                "username": "your netatmo username",
                "password": "your netatmo password"
            }
        }
    ],

```

To retrieve client id and secret please follow following guide:

1. Register at http://dev.netatmo.com as a developer
2. After successful registration create your own app by using the menu entry "CREATE AN APP"
3. On the following page, enter a name for your app. Any name can be chosen. All other fields of the form (like callback url, etc.) can be left blank.
4. After successfully submitting the form the overview page of your app should show client id and secret.


# Advanced Configuration

There are some optional configuration options in the netatmo section of the config which provide finer control about what device and services to use to create accessories.

## Control Accessories by device type

<pre>
            "deviceTypes": [
              <b>"weatherstation"</b>,
              <b>"thermostat"</b>,
              "welcome"
            ]
</pre>

This allows you to include/exclude devices of a certain type in your accessories.
The device types marked **bold** are the **default types**, if this config section is left out.

Please note, that welcome support is by default switched of, since it is not fully implemented yet.

##  Control Accessories by device ID

Not yet implemented

##  Control Services

TBD (Needs description here)


# Development

Following information is not relevant for users who just want to access netatmo via homekit.
It is intented for software developers who want to modify / enhance the functionality of the software.

## Terms

<dl>
 <dt>Device</dt>
 <dd>A device in this context is a netatmo hadware device.</dd>

 <dt>Device Type</dt>
 <dd>Describes the type of the netatmo device i.e. weatherstation, thermostat or welcome.</dd>


 <dt>Module</dt>
 <dd>Some devices contain several modules (e.g. weatherstation: main module, rain gauge, outside module, wind gauge). A device or module results in an accessory</dd>
 
</dl>

## Concepts

New deviceTypes should be put into the */devices* folder. It might be helpful to use the existing deviceTypess as template and to inherit the NetatmoDevice. Each device provides one or more accessories which provide one or more services.

Services are defined inside the */services* folder. The naming convention is, that a service source code file starts with the device name.

The default set of devices and services that are used is the one which resulted from earlier versions.

Please see Chapter #Advanced Configuration on details about how to add on device or service.

## Mock API & Testing

New features should be developed with a test scenario. Tests are executed via travis-ci.

For debugging and test purposes the software contains a support for a mock netatmo api.

The mock-api is activate by putting a

    mockapi: "name"

into the netatmo section of the config file.

When activated there will be no calls to the netatmo API. Instead raw json data is read from file located in the */mockapi_calls* folder.

The file name is *[apimethod]-[name].json* where
 
* *[apimethod]* is the name of the netatmo method to be called (e.g. getstationsdata )
* *[name]* is the name given in the config file (e.g. wind)
 
If this file is not found a *[apimethod]-default.json* file is read.
If this is not found as well, empty data is returned.

# TODO / Next Features
Following things are to be developed next.

* support for netatmo welcome (motion deteciton)
* review thermostat implementation
* complete tests
* add optional eve services including history data
* recheck temperature units
* support for min/max temperature
* add Radio Link Quality characteristic
* I18N for service and accessory names (config)
* add SoftwareRevision characteristic -> plugin version
* check logging (remove console.log)
* remove refresh log / add log for acc
* log callbacks with error != null
* Review all //TODO comments from sources
* document extended config (switch on/off devices/services)

----

Is this plugin useful for you? Please buy me a beer ...
[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=7ZGEPWHG5UH6S)


