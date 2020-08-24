# ESPAsync_WiFiManager

[![arduino-library-badge](https://www.ardu-badge.com/badge/ESPAsync_WiFiManager.svg?)](https://www.ardu-badge.com/ESPAsync_WiFiManager)
[![GitHub release](https://img.shields.io/github/release/khoih-prog/ESPAsync_WiFiManager.svg)](https://github.com/khoih-prog/ESPAsync_WiFiManager/releases)
[![GitHub](https://img.shields.io/github/license/mashape/apistatus.svg)](https://github.com/khoih-prog/ESPAsync_WiFiManager/blob/master/LICENSE)
[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](#Contributing)
[![GitHub issues](https://img.shields.io/github/issues/khoih-prog/ESPAsync_WiFiManager.svg)](http://github.com/khoih-prog/ESPAsync_WiFiManager/issues)

---
---

### Why do we need this Async [ESPAsync_WiFiManager library](https://github.com/khoih-prog/ESPAsync_WiFiManager)

- Using asynchronous network means that you can handle **more than one connection at the same time**
- You are called once the request is ready and parsed
- When you send the response, you are **immediately ready** to handle other connections while the server is taking care of sending the response in the background
- **Speed is OMG**
- **Easy to use API, HTTP Basic and Digest MD5 Authentication (default), ChunkedResponse**
- Easily extendible to handle **any type of content**
- Supports Continue 100
- Async WebSocket plugin offering different locations without extra servers or ports
- Async EventSource (Server-Sent Events) plugin to send events to the browser
- URL Rewrite plugin for conditional and permanent url rewrites
- ServeStatic plugin that supports cache, Last-Modified, default index and more
- Simple template processing engine to handle templates

To appreciate the power of the [ESPAsyncWebServer](https://github.com/me-no-dev/ESPAsyncWebServer) and underlying Async libraries, please compare the more efficient [Async_ESP32_FSWebServer example](examples/Async_ESP32_FSWebServer) example with the complicated twin [ESP32_FSWebServer](https://github.com/khoih-prog/ESP_WiFiManager/tree/master/examples/ESP32_FSWebServer).

---

### Releases 1.0.11

1. Initial coding to use ESPAsyncWebServer instead of (ESP8266)WebServer.
2. Add more features and error checking to many examples.
3. Add example [Async_ConfigOnDRD_FS_MQTT_Ptr](examples/Async_ConfigOnDRD_FS_MQTT_Ptr)
4. Bump up to v1.0.11 to sync with ESP_WiFiManager v1.0.11.

---
---

This library is based on, modified, bug-fixed and improved from:

1. [`Tzapu's WiFiManager`](https://github.com/tzapu/WiFiManager)
2. [`Ken Taylor's WiFiManager`](https://github.com/kentaylor/WiFiManager)
3. [`Alan Steremberg's ESPAsyncWiFiManager`](https://github.com/alanswx/ESPAsyncWiFiManager)
4. [`Khoi Hoang's ESP_WiFiManager`](https://github.com/khoih-prog/ESP_WiFiManager)

to use the better **asynchronous** [ESPAsyncWebServer](https://github.com/me-no-dev/ESPAsyncWebServer) instead of (ESP8266)WebServer.

This is an `ESP32 / ESP8266` WiFi Connection Manager with fallback Web ConfigPortal. This Library is used for configuring ESP32, ESP8266 modules' (WiFi / Dynamic) Credentials at runtime. You can also specify static DNS servers, personalized HostName, fixed or random AP channel. Now with CORS feature.

Thanks to this [ESPAsync_WiFiManager library](https://github.com/khoih-prog/ESPAsync_WiFiManager) is based on and sync'ed with [`ESP_WiFiManager`](https://github.com/khoih-prog/ESP_WiFiManager), all the features currently supported by [`ESP_WiFiManager`](https://github.com/khoih-prog/ESP_WiFiManager) will be available. Please have a look at [`ESP_WiFiManager`](https://github.com/khoih-prog/ESP_WiFiManager) for those too-many-to-list features.

---

## Prerequisite

 1. [`Arduino IDE 1.8.12+` for Arduino](https://www.arduino.cc/en/Main/Software)
 2. [`ESP8266 Core 2.7.3+`](https://github.com/esp8266/Arduino) for ESP8266-based boards.
 3. [`ESP32 Core 1.0.4+`](https://github.com/espressif/arduino-esp32) for ESP32-based boards
 4. [`ESPAsyncWebServer v1.2.3+`](https://github.com/me-no-dev/ESPAsyncWebServer)
 5. [`ESPAsyncTCP v1.2.2+`](https://github.com/me-no-dev/ESPAsyncTCP) for ESP8266
 6. [`AsyncTCP v1.1.1+`](https://github.com/me-no-dev/AsyncTCP) for ESP32
 
---

## Installation

### Use Arduino Library Manager
The best and easiest way is to use `Arduino Library Manager`. Search for `ESPAsync_WiFiManager`, then select / install the latest version. You can also use this link [![arduino-library-badge](https://www.ardu-badge.com/badge/ESPAsync_WiFiManager.svg?)](https://www.ardu-badge.com/ESPAsync_WiFiManager) for more detailed instructions.

### Manual Install

1. Navigate to [ESPAsync_WiFiManager](https://github.com/khoih-prog/ESPAsync_WiFiManager) page.
2. Download the latest release `ESPAsync_WiFiManager-master.zip`.
3. Extract the zip file to `ESPAsync_WiFiManager-master` directory 
4. Copy the whole `ESPAsync_WiFiManager-master` folder to Arduino libraries' directory such as `~/Arduino/libraries/`.

### VS Code & PlatformIO:
1. Install [VS Code](https://code.visualstudio.com/)
2. Install [PlatformIO](https://platformio.org/platformio-ide)
3. Install **ESPAsync_WiFiManager** library by using [Library Manager](https://docs.platformio.org/en/latest/librarymanager/). Search for ***ESPAsync_WiFiManager*** in [Platform.io Author's Libraries](https://platformio.org/lib/search?query=author:%22Khoi%20Hoang%22)
4. Use included [platformio.ini](examples/platformio/platformio.ini) file from examples to ensure that all dependent libraries will installed automatically.

---

## How It Works

- The [Async_ConfigOnSwitch](examples/Async_ConfigOnSwitch) example shows how it works and should be used as the basis for a sketch that uses this library.
- The concept of [Async_ConfigOnSwitch](examples/Async_ConfigOnSwitch) is that a new `ESP32 / ESP8266` will start a WiFi ConfigPortal when powered up and save the configuration data in non volatile memory. Thereafter, the ConfigPortal will only be started again if a button is pushed on the `ESP32 / ESP8266` module.
- Using any WiFi enabled device with a browser (computer, phone, tablet) connect to the newly created Access Point (AP) using configurable SSID and Password (specified in sketch)

```cpp
// SSID and PW for Config Portal
String ssid = "ESP_" + String(ESP_getChipId(), HEX);
const char* password = "your_password";
``` 
then connect WebBrowser to configurable ConfigPortal IP address, default is 192.168.4.1

- Choose one of the access points scanned, enter password, click ***Save***.
- ESP will restart, then try to connect to the WiFi netwotk using STA-only mode, ***without running the ConfigPortal WebServer and WiFi AP***. See [Accessing manager after connection](https://github.com/khoih-prog/ESP_WiFiManager/issues/15).

---
---

### HOWTO Basic configurations

#### 1. Using default for every configurable parameter

- Include in your sketch
```cpp
#ifdef ESP32
  #include <esp_wifi.h>
  #include <WiFi.h>
  #include <WiFiClient.h>

  #define ESP_getChipId()   ((uint32_t)ESP.getEfuseMac())

  #define LED_ON      HIGH
  #define LED_OFF     LOW
#else
  #include <ESP8266WiFi.h>          //https://github.com/esp8266/Arduino
  //needed for library
  #include <DNSServer.h>

  #define ESP_getChipId()   (ESP.getChipId())

  #define LED_ON      LOW
  #define LED_OFF     HIGH
#endif

// SSID and PW for Config Portal
String ssid = "ESP_" + String(ESP_getChipId(), HEX);
const char* password = "your_password";

// SSID and PW for your Router
String Router_SSID;
String Router_Pass;

#include <ESPAsync_WiFiManager.h>              //https://github.com/khoih-prog/ESPAsync_WiFiManager

AsyncWebServer webServer(80);
DNSServer dnsServer;
```
---

#### 2. Using many configurable parameters

- Include in your sketch

```cpp
// Default is 30s, using 20s now
#define TIME_BETWEEN_MODAL_SCANS          20000

// Default is 60s, using 30s now
#define TIME_BETWEEN_MODELESS_SCANS       30000

#ifdef ESP32
  #include <esp_wifi.h>
  #include <WiFi.h>
  #include <WiFiClient.h>

  #define ESP_getChipId()   ((uint32_t)ESP.getEfuseMac())

  #define LED_ON      HIGH
  #define LED_OFF     LOW
#else
  #include <ESP8266WiFi.h>          //https://github.com/esp8266/Arduino
  //needed for library
  #include <DNSServer.h>

  #define ESP_getChipId()   (ESP.getChipId())

  #define LED_ON      LOW
  #define LED_OFF     HIGH
#endif

// SSID and PW for Config Portal
String ssid = "ESP_" + String(ESP_getChipId(), HEX);
const char* password = "your_password";

// SSID and PW for your Router
String Router_SSID;
String Router_Pass;

// Use false if you don't like to display Available Pages in Information Page of Config Portal
// Comment out or use true to display Available Pages in Information Page of Config Portal
// Must be placed before #include <ESPAsync_WiFiManager.h>
#define USE_AVAILABLE_PAGES     true

// From v1.0.10 to permit disable/enable StaticIP configuration in Config Portal from sketch. Valid only if DHCP is used.
// You'll loose the feature of dynamically changing from DHCP to static IP, or vice versa
// You have to explicitly specify false to disable the feature.
//#define USE_STATIC_IP_CONFIG_IN_CP          false

// Use false to disable NTP config. Advisable when using Cellphone, Tablet to access Config Portal.
// See Issue 23: On Android phone ConfigPortal is unresponsive (https://github.com/khoih-prog/ESP_WiFiManager/issues/23)
#define USE_ESP_WIFIMANAGER_NTP     false

// Use true to enable CloudFlare NTP service. System can hang if you don't have Internet access while accessing CloudFlare
// See Issue #21: CloudFlare link in the default portal (https://github.com/khoih-prog/ESP_WiFiManager/issues/21)
#define USE_CLOUDFLARE_NTP          false

// New in v1.0.11
#define USING_CORS_FEATURE          true
//////

// Use USE_DHCP_IP == true for dynamic DHCP IP, false to use static IP which you have to change accordingly to your network
#if (defined(USE_STATIC_IP_CONFIG_IN_CP) && !USE_STATIC_IP_CONFIG_IN_CP)
// Force DHCP to be true
  #if defined(USE_DHCP_IP)
    #undef USE_DHCP_IP
  #endif
  #define USE_DHCP_IP     true
#else
  // You can select DHCP or Static IP here
  //#define USE_DHCP_IP     true
  #define USE_DHCP_IP     false
#endif

#if ( USE_DHCP_IP || ( defined(USE_STATIC_IP_CONFIG_IN_CP) && !USE_STATIC_IP_CONFIG_IN_CP ) )
  // Use DHCP
  #warning Using DHCP IP
  IPAddress stationIP   = IPAddress(0, 0, 0, 0);
  IPAddress gatewayIP   = IPAddress(192, 168, 2, 1);
  IPAddress netMask     = IPAddress(255, 255, 255, 0);
#else
  // Use static IP
  #warning Using static IP
  
  #ifdef ESP32
    IPAddress stationIP   = IPAddress(192, 168, 2, 232);
  #else
    IPAddress stationIP   = IPAddress(192, 168, 2, 186);
  #endif
  
  IPAddress gatewayIP   = IPAddress(192, 168, 2, 1);
  IPAddress netMask     = IPAddress(255, 255, 255, 0);
#endif

#define USE_CONFIGURABLE_DNS      true

IPAddress dns1IP      = gatewayIP;
IPAddress dns2IP      = IPAddress(8, 8, 8, 8);

#include <ESPAsync_WiFiManager.h>              //https://github.com/khoih-prog/ESPAsync_WiFiManager

AsyncWebServer webServer(80);
DNSServer dnsServer;
```

---

#### 3. Using STA-mode DHCP, but don't like to change to static IP or display in Config Portal

```cpp
// From v1.0.10 to permit disable/enable StaticIP configuration in Config Portal from sketch. Valid only if DHCP is used.
// You'll loose the feature of dynamically changing from DHCP to static IP, or vice versa
// You have to explicitly specify false to disable the feature.
#define USE_STATIC_IP_CONFIG_IN_CP          false

```

---

#### 4. Using STA-mode DHCP, but permit to change to static IP and display in Config Portal

```cpp
// From v1.0.10 to permit disable/enable StaticIP configuration in Config Portal from sketch. Valid only if DHCP is used.
// You'll loose the feature of dynamically changing from DHCP to static IP, or vice versa
// You have to explicitly specify false to disable the feature.
//#define USE_STATIC_IP_CONFIG_IN_CP          false

// Use USE_DHCP_IP == true for dynamic DHCP IP, false to use static IP which you have to change accordingly to your network
#if (defined(USE_STATIC_IP_CONFIG_IN_CP) && !USE_STATIC_IP_CONFIG_IN_CP)
  // Force DHCP to be true
  #if defined(USE_DHCP_IP)
    #undef USE_DHCP_IP
  #endif
  #define USE_DHCP_IP     true
#else
  // You can select DHCP or Static IP here
  #define USE_DHCP_IP     true
#endif

```

---

#### 5. Using STA-mode StaticIP, and be able to change to DHCP IP and display in Config Portal

```cpp
// From v1.0.10 to permit disable/enable StaticIP configuration in Config Portal from sketch. Valid only if DHCP is used.
// You'll loose the feature of dynamically changing from DHCP to static IP, or vice versa
// You have to explicitly specify false to disable the feature.
//#define USE_STATIC_IP_CONFIG_IN_CP          false

// Use USE_DHCP_IP == true for dynamic DHCP IP, false to use static IP which you have to change accordingly to your network
#if (defined(USE_STATIC_IP_CONFIG_IN_CP) && !USE_STATIC_IP_CONFIG_IN_CP)
// Force DHCP to be true
  #if defined(USE_DHCP_IP)
    #undef USE_DHCP_IP
  #endif
  #define USE_DHCP_IP     true
#else
  // You can select DHCP or Static IP here
  #define USE_DHCP_IP     false
#endif

```

---

#### 6. Using STA-mode StaticIP and configurable DNS, and be able to change to DHCP IP and display in Config Portal

```cpp
// From v1.0.10 to permit disable/enable StaticIP configuration in Config Portal from sketch. Valid only if DHCP is used.
// You'll loose the feature of dynamically changing from DHCP to static IP, or vice versa
// You have to explicitly specify false to disable the feature.
//#define USE_STATIC_IP_CONFIG_IN_CP          false

// Use USE_DHCP_IP == true for dynamic DHCP IP, false to use static IP which you have to change accordingly to your network
#if (defined(USE_STATIC_IP_CONFIG_IN_CP) && !USE_STATIC_IP_CONFIG_IN_CP)
  // Force DHCP to be true
  #if defined(USE_DHCP_IP)
    #undef USE_DHCP_IP
  #endif
  #define USE_DHCP_IP     true
#else
  // You can select DHCP or Static IP here
  #define USE_DHCP_IP     false
#endif

#define USE_CONFIGURABLE_DNS      true

IPAddress dns1IP      = gatewayIP;
IPAddress dns2IP      = IPAddress(8, 8, 8, 8);

```

---

#### 7. Using STA-mode StaticIP and auto DNS, and be able to change to DHCP IP and display in Config Portal

```cpp
// From v1.0.10 to permit disable/enable StaticIP configuration in Config Portal from sketch. Valid only if DHCP is used.
// You'll loose the feature of dynamically changing from DHCP to static IP, or vice versa
// You have to explicitly specify false to disable the feature.
//#define USE_STATIC_IP_CONFIG_IN_CP          false

// Use USE_DHCP_IP == true for dynamic DHCP IP, false to use static IP which you have to change accordingly to your network
#if (defined(USE_STATIC_IP_CONFIG_IN_CP) && !USE_STATIC_IP_CONFIG_IN_CP)
  // Force DHCP to be true
  #if defined(USE_DHCP_IP)
    #undef USE_DHCP_IP
  #endif
  #define USE_DHCP_IP     true
#else
  // You can select DHCP or Static IP here
  #define USE_DHCP_IP     false
#endif

#define USE_CONFIGURABLE_DNS      false

```

---

#### 8. Not using NTP to avoid issue with some WebBrowsers, especially in CellPhone or Tablets.


```cpp
// Use false to disable NTP config. Advisable when using Cellphone, Tablet to access Config Portal.
// See Issue 23: On Android phone ConfigPortal is unresponsive (https://github.com/khoih-prog/ESP_WiFiManager/issues/23)
#define USE_ESP_WIFIMANAGER_NTP     false

```

---

#### 9. Using NTP feature with CloudFlare. System can hang until you have Internet access for CloudFlare.


```cpp
// Use false to disable NTP config. Advisable when using Cellphone, Tablet to access Config Portal.
// See Issue 23: On Android phone ConfigPortal is unresponsive (https://github.com/khoih-prog/ESP_WiFiManager/issues/23)
#define USE_ESP_WIFIMANAGER_NTP     true

// Use true to enable CloudFlare NTP service. System can hang if you don't have Internet access while accessing CloudFlare
// See Issue #21: CloudFlare link in the default portal (https://github.com/khoih-prog/ESP_WiFiManager/issues/21)
#define USE_CLOUDFLARE_NTP          true

```

---

#### 10. Using NTP feature without CloudFlare to avoid system hang if no Internet access for CloudFlare.


```cpp
// Use false to disable NTP config. Advisable when using Cellphone, Tablet to access Config Portal.
// See Issue 23: On Android phone ConfigPortal is unresponsive (https://github.com/khoih-prog/ESP_WiFiManager/issues/23)
#define USE_ESP_WIFIMANAGER_NTP     true

// Use true to enable CloudFlare NTP service. System can hang if you don't have Internet access while accessing CloudFlare
// See Issue #21: CloudFlare link in the default portal (https://github.com/khoih-prog/ESP_WiFiManager/issues/21)
#define USE_CLOUDFLARE_NTP          false

```

---

#### 11. Using random AP-mode channel to avoid conflict


```cpp
// From v1.0.10 only
// Set config portal channel, default = 1. Use 0 => random channel from 1-13
ESPAsync_wifiManager.setConfigPortalChannel(0);
//////
```

---

#### 12. Using fixed AP-mode channel, for example channel 3


```cpp
// From v1.0.10 only
// Set config portal channel, default = 1. Use 0 => random channel from 1-13
ESPAsync_wifiManager.setConfigPortalChannel(3);
//////
```
---

#### 13. Setting STA-mode static IP


```cpp
// Set static IP, Gateway, Subnetmask, DNS1 and DNS2. New in v1.0.5
ESPAsync_wifiManager.setSTAStaticIPConfig(stationIP, gatewayIP, netMask, dns1IP, dns2IP);
```
---

#### 14. Using AUTOCONNECT_NO_INVALIDATE feature

1. Don't invalidate WiFi SSID/PW when calling autoConnect()  (default)

```cpp
#define AUTOCONNECT_NO_INVALIDATE     true
```

2. To invalidate WiFi SSID/PW when calling autoConnect()

```cpp
#define AUTOCONNECT_NO_INVALIDATE     false
```
---

#### 15. Using CORS (Cross-Origin Resource Sharing) feature

1. To use CORS feature

```cpp
// Default false for using only whenever necessary to avoid security issue
#define USING_CORS_FEATURE     true
```

2. Not use CORS feature (default)

```cpp
// Default false for using only whenever necessary to avoid security issue
#define USING_CORS_FEATURE     false
```

---
---

### HOWTO Open Config Portal

- When you want to open a config portal, with default DHCP hostname `ESP8266-XXXXXX` or `ESP32-XXXXXX`, just add

```cpp
#include <ESPAsync_WiFiManager.h>              //https://github.com/khoih-prog/ESPAsync_WiFiManager

AsyncWebServer webServer(80);
DNSServer dnsServer;

ESPAsync_WiFiManager ESPAsync_wifiManager(&webServer, &dnsServer);
```
If you'd like to have a personalized hostname 
`(RFC952-conformed,- 24 chars max,- only a..z A..Z 0..9 '-' and no '-' as last char)`

add

```cpp
ESPAsync_WiFiManager ESPAsync_wifiManager(&webServer, &dnsServer, "Personalized-HostName");
```

then later call

```cpp
ESPAsync_wifiManager.startConfigPortal()
```

While in AP mode, connect to it using its `SSID` (ESP_XXXXXX) / `Password` ("your_password"), then open a browser to the AP IP, default `192.168.4.1`, configure wifi then save. The WiFi connection information will be saved in non volatile memory. It will then reboot and autoconnect.

You can also change the AP IP by:

```cpp
//set custom ip for portal
ESPAsync_wifiManager.setAPStaticIPConfig(IPAddress(10,0,1,1), IPAddress(10,0,1,1), IPAddress(255,255,255,0));
```

and use fixed / dynamic / random AP channel by:

```cpp
// Set config portal channel, default = 1. Use 0 => random channel from 1-13
ESPAsync_wifiManager.setConfigPortalChannel(0);
//////
```

Once WiFi network information is saved in the `ESP32 / ESP8266`, it will try to autoconnect to WiFi every time it is started, without requiring any function calls in the sketch.

---

### Examples

 1. [Async_ConfigOnSwitch](examples/Async_ConfigOnSwitch)
 2. [Async_ConfigOnSwitchFS](examples/Async_ConfigOnSwitchFS)
 3. [Async_ConfigOnStartup](examples/Async_ConfigOnStartup) 
 4. [Async_ConfigOnDoubleReset](examples/Async_ConfigOnDoubleReset)  (now support ArduinoJson 6.0.0+ as well as 5.13.5-)
 5. [Async_ConfigPortalParamsOnSwitch](examples/Async_ConfigPortalParamsOnSwitch)  (now support ArduinoJson 6.0.0+ as well as 5.13.5-)
 6. [Async_AutoConnect](examples/Async_AutoConnect)
 7. [Async_AutoConnectWithFeedback](examples/Async_AutoConnectWithFeedback)
 8. [Async_AutoConnectWithFeedbackLED](examples/Async_AutoConnectWithFeedbackLED)
 9. [Async_AutoConnectWithFSParameters](examples/Async_AutoConnectWithFSParameters)
10. [Async_ConfigOnSwitchFS_MQTT_Ptr](examples/Async_ConfigOnSwitchFS_MQTT_Ptr)
11. [Async_AutoConnectWithFSParametersAndCustomIP](examples/Async_AutoConnectWithFSParametersAndCustomIP)
12. [ModelessConnect](examples/ModelessConnect)
13. [ModelessWithInterrupts](examples/ModelessWithInterrupts)
14. [Async_ESP32_FSWebServer](examples/Async_ESP32_FSWebServer)
15. [Async_ESP32_FSWebServer_DRD](examples/Async_ESP32_FSWebServer_DRD)
16. [Async_ESP_FSWebServer](examples/Async_ESP_FSWebServer)
17. [Async_ESP_FSWebServer_DRD](examples/Async_ESP_FSWebServer_DRD)
18. [Async_ConfigOnDRD_FS_MQTT_Ptr](examples/Async_ConfigOnDRD_FS_MQTT_Ptr)

---
---

## So, how it works?
In `ConfigPortal Mode`, it starts an access point called `ESP_XXXXXX`. Connect to it using the `configurable password` you can define in the code. For example, `your_password` (see examples):

```cpp
// SSID and PW for Config Portal
String ssid = "ESP_" + String(ESP_getChipId(), HEX);
const char* password = "your_password";
```
After you connected, please, go to http://192.168.4.1, you'll see this `Main` page:

<p align="center">
    <img src="https://github.com/khoih-prog/ESPAsync_WiFiManager/blob/master/Images/Main.png">
</p>

Select `Information` to enter the Info page where the board info will be shown (long page)

<p align="center">
    <img src="https://github.com/khoih-prog/ESPAsync_WiFiManager/blob/master/Images/Info.png">
</p>

or short page (default)

<p align="center">
    <img src="https://github.com/khoih-prog/ESPAsync_WiFiManager/blob/master/Images/Info_Short.png">
</p>

Select `Configuration` to enter this page where you can select an AP and specify its WiFi Credentials

<p align="center">
    <img src="https://github.com/khoih-prog/ESPAsync_WiFiManager/blob/master/Images/Configuration_AIO_MQTT.png">
</p>

Enter your credentials, then click ***Save***. The WiFi Credentials will be saved and the board reboots to connect to the selected WiFi AP.

If you're already connected to a listed WiFi AP and don't want to change anything, just select ***Exit Portal*** from the `Main` page to reboot the board and connect to the previously-stored AP. The WiFi Credentials are still intact.

---
---

## Documentation

#### Password protect the configuration Access Point
You can password protect the ConfigPortal AP.  Simply add an SSID as the first parameter and the password as a second parameter to `startConfigPortal`. See the above examples.

A short password seems to have unpredictable results so use one that's around 8 characters or more in length.
The guidelines are that a wifi password must consist of 8 to 63 ASCII-encoded characters in the range of 32 to 126 (decimal)

```cpp
ESPAsync_wifiManager.startConfigPortal( SSID , password )
```

#### Callbacks

##### Save settings
This gets called when custom parameters have been set **AND** a connection has been established. Use it to set a flag, so when all the configuration finishes, you can save the extra parameters somewhere.

See [Async_ConfigOnSwitchFS Example](examples/Async_ConfigOnSwitchFS).

```cpp
ESPAsync_wifiManager.setSaveConfigCallback(saveConfigCallback);
```
saveConfigCallback declaration and example

```cpp
//flag for saving data
bool shouldSaveConfig = false;

//callback notifying us of the need to save config
void saveConfigCallback () 
{
  Serial.println("Should save config");
  shouldSaveConfig = true;
}
```

#### ConfigPortal Timeout
If you need to set a timeout so the `ESP32 / ESP8266` doesn't hang waiting to be configured for ever. 

```cpp
ESPAsync_wifiManager.setConfigPortalTimeout(120);
```
which will wait 2 minutes (120 seconds). When the time passes, the startConfigPortal function will return and continue the sketch, 
unless you're accessing the Config Portal. In this case, the `startConfigPortal` function will stay until you save config data or exit 
the Config Portal.


#### On Demand ConfigPortal

Example usage

```cpp
void loop()
{
  // is configuration portal requested?
  if ((digitalRead(TRIGGER_PIN) == LOW) || (digitalRead(TRIGGER_PIN2) == LOW))
  {
    Serial.println("\nConfiguration portal requested.");
    digitalWrite(PIN_LED, LED_ON); // turn the LED on by making the voltage LOW to tell us we are in configuration mode.

    //Local intialization. Once its business is done, there is no need to keep it around
    // Use this to default DHCP hostname to ESP8266-XXXXXX or ESP32-XXXXXX
    //ESPAsync_WiFiManager ESPAsync_wifiManager(&webServer, &dnsServer);
    // Use this to personalize DHCP hostname (RFC952 conformed)
    ESPAsync_WiFiManager ESPAsync_wifiManager(&webServer, &dnsServer, "ConfigOnSwitch");

    ESPAsync_wifiManager.setMinimumSignalQuality(-1);

    // From v1.0.10 only
    // Set config portal channel, default = 1. Use 0 => random channel from 1-13
    ESPAsync_wifiManager.setConfigPortalChannel(0);
    //////

    //set custom ip for portal
    //ESPAsync_wifiManager.setAPStaticIPConfig(IPAddress(192, 168, 100, 1), IPAddress(192, 168, 100, 1), IPAddress(255, 255, 255, 0));

    // Set static IP, Gateway, Subnetmask, DNS1 and DNS2. New in v1.0.5
    ESPAsync_wifiManager.setSTAStaticIPConfig(stationIP, gatewayIP, netMask, dns1IP, dns2IP);

    //Check if there is stored WiFi router/password credentials.
    //If not found, device will remain in configuration mode until switched off via webserver.
    Serial.print("Opening configuration portal. ");
    Router_SSID = ESPAsync_wifiManager.WiFi_SSID();
    if (Router_SSID != "")
    {
      ESPAsync_wifiManager.setConfigPortalTimeout(120); //If no access point name has been previously entered disable timeout.
      Serial.println("Got stored Credentials. Timeout 120s");
    }
    else
      Serial.println("No stored Credentials. No timeout");

    //it starts an access point
    //and goes into a blocking loop awaiting configuration
    if (!ESPAsync_wifiManager.startConfigPortal((const char *) ssid.c_str(), password))
    {
      Serial.println("Not connected to WiFi but continuing anyway.");
    }
    else
    {
      //if you get here you have connected to the WiFi
      Serial.println("connected...yeey :)");
      Serial.print("Local IP: ");
      Serial.println(WiFi.localIP());
    }

    digitalWrite(PIN_LED, LED_OFF); // Turn led off as we are not in configuration mode.
  }

  // put your main code here, to run repeatedly
  check_status();

}
```

See  [Async_ConfigOnSwitch](examples/Async_ConfigOnSwitch) example for a more complex version.

---
---

#### Custom Parameters

Many applications need configuration parameters like `MQTT host and port`, [Blynk](http://www.blynk.cc) or [emoncms](http://emoncms.org) tokens, etc. While it is possible to use [`ESPAsync_WiFiManager`](https://github.com/khoih-prog/ESPAsync_WiFiManager) to collect additional parameters, it is better to read these parameters from a web service once [`ESPAsync_WiFiManager`](https://github.com/khoih-prog/ESPAsync_WiFiManager) has been used to connect to the Internet.

To capture other parameters with [`ESPAsync_WiFiManager`](https://github.com/khoih-prog/ESPAsync_WiFiManager) is a little bit more complicated than all the other features. This requires adding custom HTML to your form. 

If you want to do it with [`ESPAsync_WiFiManager`](https://github.com/khoih-prog/ESPAsync_WiFiManager) see the example [Async_ConfigOnSwitchFS](examples/Async_ConfigOnSwitchFS)

#### Custom IP Configuration

You can set a custom IP for both AP (access point, config mode) and STA (station mode, client mode, normal project state)

##### Custom Access Point IP Configuration

This will set your captive portal to a specific IP should you need/want such a feature. Add the following snippet before `startConfigPortal()`

```cpp
//set custom ip for portal
ESPAsync_wifiManager.setAPStaticIPConfig(IPAddress(10,0,1,1), IPAddress(10,0,1,1), IPAddress(255,255,255,0));
```

##### Custom Station (client) Static IP Configuration

This will use the specified IP configuration instead of using DHCP in station mode.
```cpp
ESPAsync_wifiManager.setSTAStaticIPConfig(IPAddress(192,168,0,99), IPAddress(192,168,0,1), IPAddress(255,255,255,0));
```

#### Custom HTML, CSS, Javascript

There are various ways in which you can inject custom HTML, CSS or Javascript into the ConfigPortal.

The options are:
- inject custom head element

You can use this to any html bit to the head of the ConfigPortal. If you add a `<style>` element, bare in mind it overwrites the included css, not replaces.

```cpp
ESPAsync_wifiManager.setCustomHeadElement("<style>html{filter: invert(100%); -webkit-filter: invert(100%);}</style>");
```

- inject a custom bit of html in the configuration form

```cpp
ESPAsync_WMParameter custom_text("<p>This is just a text paragraph</p>");
ESPAsync_wifiManager.addParameter(&custom_text);
```

- inject a custom bit of html in a configuration form element
Just add the bit you want added as the last parameter to the custom parameter constructor.

```cpp
ESPAsync_WMParameter custom_mqtt_server("server", "mqtt server", "iot.eclipse", 40, " readonly");
```

#### Filter Networks

You can filter networks based on signal quality and show/hide duplicate networks.

- If you would like to filter low signal quality networks you can tell WiFiManager to not show networks below an arbitrary quality %;

```cpp
ESPAsync_wifiManager.setMinimumSignalQuality(10);
```
will not show networks under 10% signal quality. If you omit the parameter it defaults to 8%;

- You can also remove or show duplicate networks (default is remove).
Use this function to show (or hide) all networks.

```cpp
ESPAsync_wifiManager.setRemoveDuplicateAPs(false);
```
---

### Example [Async_ConfigOnDRD_FS_MQTT_Ptr](examples/Async_ConfigOnDRD_FS_MQTT_Ptr)

```cpp
/****************************************************************************************************************************
  This example will open a Config Portal when there is no stored WiFi Credentials or when a DRD is detected.
  
  You can reconfigure to use another pin, such as the convenience FLASH / BOOT button @ PIN_D0;.
   
  A password is required to connect to the Config Portal so that only who know the password can access the Config Portal.
  
  The Credentials, being input via Config Portal, will then be saved into LittleFS / SPIFFS file, and be used to connect to 
  Adafruit MQTT Server at "io.adafruit.com" and publish a Temperature Topic
  
  Based on original sketch posted by "Marko"(https://github.com/wackoo-arduino) on https://forum.arduino.cc/index.php?topic=692108
 *****************************************************************************************************************************/
#if !( defined(ESP8266) ||  defined(ESP32) )
  #error This code is intended to run on the ESP8266 or ESP32 platform! Please check your Tools->Board setting.
#endif

// Use from 0 to 4. Higher number, more debugging messages and memory usage.
#define _ESPASYNC_WIFIMGR_LOGLEVEL_    3

// Default is 30s, using 20s now
#define TIME_BETWEEN_MODAL_SCANS          20000

// Default is 60s, using 30s now
#define TIME_BETWEEN_MODELESS_SCANS       30000

#include <FS.h>

// Now support ArduinoJson 6.0.0+ ( tested with v6.15.2 to v6.16.1 )
#include <ArduinoJson.h>        // get it from https://arduinojson.org/ or install via Arduino library manager

//Ported to ESP32
//For ESP32, To use ESP32 Dev Module, QIO, Flash 4MB/80MHz, Upload 921600
#if ESP32
  #include <esp_wifi.h>
  #include <WiFi.h>
  #include <WiFiClient.h>
  
  #define ESP_getChipId()   ((uint32_t)ESP.getEfuseMac())
  
  #define LED_ON      HIGH
  #define LED_OFF     LOW

  // Use SPIFFS
  #include <SPIFFS.h>
  #define FileFS                  SPIFFS
  #define FileFSType              "SPIFFS"
  #define ESP_DRD_USE_SPIFFS      true
  
#else

  #include <ESP8266WiFi.h>          //https://github.com/esp8266/Arduino
  //needed for library
  #include <DNSServer.h>
  
  #define ESP_getChipId()   (ESP.getChipId())
  
  #define LED_ON      LOW
  #define LED_OFF     HIGH

  #define USE_LITTLEFS      true

  #if USE_LITTLEFS
    #define FileFS                  LittleFS
    #define FileFSType              "LittleFS"
    #define ESP_DRD_USE_LITTLEFS    true
  #else
    #define FileFS                  SPIFFS
    #define FileFSType              "SPIFFS"
    #define ESP_DRD_USE_SPIFFS      true
  #endif

  #include <LittleFS.h>

#endif
 
#define DOUBLERESETDETECTOR_DEBUG       true  //false

#include <ESP_DoubleResetDetector.h>      //https://github.com/khoih-prog/ESP_DoubleResetDetector

// Number of seconds after reset during which a
// subseqent reset will be considered a double reset.
#define DRD_TIMEOUT 10

// RTC Memory Address for the DoubleResetDetector to use
#define DRD_ADDRESS 0

//DoubleResetDetector drd(DRD_TIMEOUT, DRD_ADDRESS);
DoubleResetDetector* drd = NULL;

// Indicates whether ESP has WiFi credentials saved from previous session, or double reset detected
bool initialConfig = false;

#include "Adafruit_MQTT.h"                //https://github.com/adafruit/Adafruit_MQTT_Library
#include "Adafruit_MQTT_Client.h"         //https://github.com/adafruit/Adafruit_MQTT_Library

#if ESP32
  //See file .../hardware/espressif/esp32/variants/(esp32|doitESP32devkitV1)/pins_arduino.h
  #define LED_BUILTIN       2         // Pin D2 mapped to pin GPIO2/ADC12 of ESP32, control on-board LED
  #define PIN_LED           2         // Pin D2 mapped to pin GPIO2/ADC12 of ESP32, control on-board LED
#endif    //ESP32

const char* CONFIG_FILE = "/ConfigMQTT.json";

// Indicates whether ESP has WiFi credentials saved from previous session
//bool initialConfig = true; //default false

// Default configuration values for Adafruit IO MQTT
// This actually works
#define AIO_SERVER              "io.adafruit.com"
#define AIO_SERVERPORT          1883 //1883, or 8883 for SSL
#define AIO_USERNAME            "private" //Adafruit IO
#define AIO_KEY                 "private"

// Labels for custom parameters in WiFi manager
#define AIO_SERVER_Label             "AIO_SERVER_Label"
#define AIO_SERVERPORT_Label         "AIO_SERVERPORT_Label"
#define AIO_USERNAME_Label           "AIO_USERNAME_Label"
#define AIO_KEY_Label                "AIO_KEY_Label"

// Just dummy topics. To be updated later when got valid data from FS or Config Portal
String MQTT_Pub_Topic   = "private/feeds/Temperature";

// Variables to save custom parameters to...
// I would like to use these instead of #defines
#define custom_AIO_SERVER_LEN       20
#define custom_AIO_USERNAME_LEN     20
#define custom_AIO_KEY_LEN          40

char custom_AIO_SERVER[custom_AIO_SERVER_LEN];
int  custom_AIO_SERVERPORT;
char custom_AIO_USERNAME[custom_AIO_USERNAME_LEN];
char custom_AIO_KEY[custom_AIO_KEY_LEN];

// Function Prototypes
void MQTT_connect();
bool readConfigFile();
bool writeConfigFile();

// For Config Portal
// SSID and PW for Config Portal
String ssid = "ESP_" + String(ESP_getChipId(), HEX);
const char* password = "your_password";

// SSID and PW for your Router
String Router_SSID;
String Router_Pass;

// Use false if you don't like to display Available Pages in Information Page of Config Portal
// Comment out or use true to display Available Pages in Information Page of Config Portal
// Must be placed before #include <ESPAsync_WiFiManager.h>
#define USE_AVAILABLE_PAGES     false

// From v1.0.10 to permit disable/enable StaticIP configuration in Config Portal from sketch. Valid only if DHCP is used.
// You'll loose the feature of dynamically changing from DHCP to static IP, or vice versa
// You have to explicitly specify false to disable the feature.
//#define USE_STATIC_IP_CONFIG_IN_CP          false

// Use false to disable NTP config. Advisable when using Cellphone, Tablet to access Config Portal.
// See Issue 23: On Android phone ConfigPortal is unresponsive (https://github.com/khoih-prog/ESP_WiFiManager/issues/23)
#define USE_ESP_WIFIMANAGER_NTP     false

// Use true to enable CloudFlare NTP service. System can hang if you don't have Internet access while accessing CloudFlare
// See Issue #21: CloudFlare link in the default portal (https://github.com/khoih-prog/ESP_WiFiManager/issues/21)
#define USE_CLOUDFLARE_NTP          false

// New in v1.0.11
#define USING_CORS_FEATURE          true
//////

// Use USE_DHCP_IP == true for dynamic DHCP IP, false to use static IP which you have to change accordingly to your network
#if (defined(USE_STATIC_IP_CONFIG_IN_CP) && !USE_STATIC_IP_CONFIG_IN_CP)
// Force DHCP to be true
#if defined(USE_DHCP_IP)
#undef USE_DHCP_IP
#endif
#define USE_DHCP_IP     true
#else
// You can select DHCP or Static IP here
//#define USE_DHCP_IP     true
#define USE_DHCP_IP     false
#endif

#if ( USE_DHCP_IP || ( defined(USE_STATIC_IP_CONFIG_IN_CP) && !USE_STATIC_IP_CONFIG_IN_CP ) )
// Use DHCP
#warning Using DHCP IP
IPAddress stationIP   = IPAddress(0, 0, 0, 0);
IPAddress gatewayIP   = IPAddress(192, 168, 2, 1);
IPAddress netMask     = IPAddress(255, 255, 255, 0);
#else
// Use static IP
#warning Using static IP
#ifdef ESP32
IPAddress stationIP   = IPAddress(192, 168, 2, 232);
#else
IPAddress stationIP   = IPAddress(192, 168, 2, 186);
#endif

IPAddress gatewayIP   = IPAddress(192, 168, 2, 1);
IPAddress netMask     = IPAddress(255, 255, 255, 0);
#endif

#define USE_CONFIGURABLE_DNS      true

IPAddress dns1IP      = gatewayIP;
IPAddress dns2IP      = IPAddress(8, 8, 8, 8);

#include <ESPAsync_WiFiManager.h>              //https://github.com/khoih-prog/ESPAsync_WiFiManager

#define HTTP_PORT           80

AsyncWebServer webServer(HTTP_PORT);
DNSServer dnsServer;

// Create an ESP32 WiFiClient class to connect to the MQTT server
WiFiClient *client                    = NULL;

Adafruit_MQTT_Client    *mqtt         = NULL;
Adafruit_MQTT_Publish   *Temperature  = NULL;

void heartBeatPrint(void)
{
  static int num = 1;

  if (WiFi.status() == WL_CONNECTED)
    Serial.print(F("W"));        // W means connected to WiFi
  else
    Serial.print(F("N"));        // N means not connected to WiFi

  if (num == 40)
  {
    Serial.println();
    num = 1;
  }
  else if (num++ % 5 == 0)
  {
    Serial.print(F(" "));
  }
}

void publishMQTT(void)
{
    float some_number = 25.0 + (float) ( millis() % 100 ) /  100;

    // For debug only
    //Serial.print(F("Published Temp = "));
    //Serial.println(some_number);
    
    MQTT_connect();

    if (Temperature->publish(some_number)) 
    {
      Serial.print(F("T"));        // T means publishing OK
    }
    else 
    {
      Serial.print(F("F"));        // F means publishing failure
    }
}

void check_status()
{
  static ulong checkstatus_timeout = 0;

#define HEARTBEAT_INTERVAL    10000L
  // Print hearbeat every HEARTBEAT_INTERVAL (10) seconds.
  if ((millis() > checkstatus_timeout) || (checkstatus_timeout == 0))
  {
    if (WiFi.status() == WL_CONNECTED)
    {
      publishMQTT();
    }
    
    heartBeatPrint();
    checkstatus_timeout = millis() + HEARTBEAT_INTERVAL;
  }
}

void deleteOldInstances(void)
{
  // Delete previous instances
  if (mqtt)
  {
    delete mqtt;
    mqtt = NULL;
    
    Serial.println(F("Deleting old MQTT object"));
  }

  if (Temperature)
  {
    delete Temperature;
    Temperature = NULL;
    
    Serial.println(F("Deleting old Temperature object"));
  }
}

void createNewInstances(void)
{
  if (!client)
  {
    client = new WiFiClient;
    
    Serial.print(F("\nCreating new WiFi client object : "));
    Serial.println(client? F("OK") : F("failed"));
  }
  
  // Create new instances from new data
  if (!mqtt)
  {
    // Setup the MQTT client class by passing in the WiFi client and MQTT server and login details.
    mqtt = new Adafruit_MQTT_Client(client, custom_AIO_SERVER, custom_AIO_SERVERPORT, custom_AIO_USERNAME, custom_AIO_KEY);
    
    Serial.print(F("Creating new MQTT object : "));
    
    if (mqtt)
    {
      Serial.println(F("OK"));
      Serial.println(String("AIO_SERVER = ")    + custom_AIO_SERVER    + ", AIO_SERVERPORT = "  + custom_AIO_SERVERPORT);
      Serial.println(String("AIO_USERNAME = ")  + custom_AIO_USERNAME  + ", AIO_KEY = "         + custom_AIO_KEY);
    }
    else
      Serial.println(F("Failed"));
  }
  
  if (!Temperature)
  {
    Serial.print(F("Creating new MQTT_Pub_Topic,  Temperature = "));
    Serial.println(MQTT_Pub_Topic);
    
    Temperature = new Adafruit_MQTT_Publish(mqtt, MQTT_Pub_Topic.c_str());
 
    Serial.print(F("Creating new Temperature object : "));
    
    if (Temperature)
    {
      Serial.println(F("OK"));
      Serial.println(String("Temperature MQTT_Pub_Topic = ")  + MQTT_Pub_Topic);
    }
    else
      Serial.println(F("Failed"));
    }
}

void wifi_manager() 
{
  Serial.println(F("\nConfig Portal requested."));
  digitalWrite(LED_BUILTIN, LED_ON); // turn the LED on by making the voltage LOW to tell us we are in configuration mode.

  //Local intialization. Once its business is done, there is no need to keep it around
  ESPAsync_WiFiManager ESPAsync_wifiManager(&webServer, &dnsServer, "ConfigOnSwichFS-MQTT");

  //Check if there is stored WiFi router/password credentials.
  //If not found, device will remain in configuration mode until switched off via webserver.
  Serial.print(F("Opening Config Portal. "));
  
  Router_SSID = ESPAsync_wifiManager.WiFi_SSID();
  
  if (Router_SSID != "")
  {
    ESPAsync_wifiManager.setConfigPortalTimeout(120); //If no access point name has been previously entered disable timeout.
    Serial.println(F("Got stored Credentials. Timeout 120s"));
  }
  else
    Serial.println(F("No stored Credentials. No timeout"));

  //Local intialization. Once its business is done, there is no need to keep it around

  // Extra parameters to be configured
  // After connecting, parameter.getValue() will get you the configured value
  // Format: <ID> <Placeholder text> <default value> <length> <custom HTML> <label placement>
  // (*** we are not using <custom HTML> and <label placement> ***)

  // AIO_SERVER
  ESPAsync_WMParameter AIO_SERVER_FIELD(AIO_SERVER_Label, "AIO SERVER", custom_AIO_SERVER, custom_AIO_SERVER_LEN /*20*/);

  // AIO_SERVERPORT (because it is int, it needs to be converted to string)
  char convertedValue[5];
  
  sprintf(convertedValue, "%d", custom_AIO_SERVERPORT);
  ESPAsync_WMParameter AIO_SERVERPORT_FIELD(AIO_SERVERPORT_Label, "AIO SERVER PORT", convertedValue, 5);

  // AIO_USERNAME
  ESPAsync_WMParameter AIO_USERNAME_FIELD(AIO_USERNAME_Label, "AIO USERNAME", custom_AIO_USERNAME, custom_AIO_USERNAME_LEN /*20*/);

  // AIO_KEY
  ESPAsync_WMParameter AIO_KEY_FIELD(AIO_KEY_Label, "AIO KEY", custom_AIO_KEY, custom_AIO_KEY_LEN /*40*/);

  // add all parameters here
  // order of adding is important
  //ESPAsync_wifiManager.addParameter(&hint_text);
  ESPAsync_wifiManager.addParameter(&AIO_SERVER_FIELD);
  ESPAsync_wifiManager.addParameter(&AIO_SERVERPORT_FIELD);
  ESPAsync_wifiManager.addParameter(&AIO_USERNAME_FIELD);
  ESPAsync_wifiManager.addParameter(&AIO_KEY_FIELD);

  // Sets timeout in seconds until configuration portal gets turned off.
  // If not specified device will remain in configuration mode until
  // switched off via webserver or device is restarted.
  //ESPAsync_wifiManager.setConfigPortalTimeout(120);

  ESPAsync_wifiManager.setMinimumSignalQuality(-1);

  // Set config portal channel, default = 1. Use 0 => random channel from 1-13
  ESPAsync_wifiManager.setConfigPortalChannel(0);
  //////
  
  //set custom ip for portal
  //ESPAsync_wifiManager.setAPStaticIPConfig(IPAddress(192, 168, 100, 1), IPAddress(192, 168, 100, 1), IPAddress(255, 255, 255, 0));
  
#if !USE_DHCP_IP    
  #if USE_CONFIGURABLE_DNS
    // Set static IP, Gateway, Subnetmask, DNS1 and DNS2. New in v1.0.5
    ESPAsync_wifiManager.setSTAStaticIPConfig(stationIP, gatewayIP, netMask, dns1IP, dns2IP);
  #else
    // Set static IP, Gateway, Subnetmask, Use auto DNS1 and DNS2.
    ESPAsync_wifiManager.setSTAStaticIPConfig(stationIP, gatewayIP, netMask);
  #endif 
#endif  

  // Start an access point
  // and goes into a blocking loop awaiting configuration.
  // Once the user leaves the portal with the exit button
  // processing will continue
  if (!ESPAsync_wifiManager.startConfigPortal((const char *) ssid.c_str(), password))
  {
    Serial.println(F("Not connected to WiFi but continuing anyway."));
  }
  else
  {
    // If you get here you have connected to the WiFi
    Serial.println(F("Connected...yeey :)"));
    Serial.print(F("Local IP: "));
    Serial.println(WiFi.localIP());
  }

  // Getting posted form values and overriding local variables parameters
  // Config file is written regardless the connection state
  strcpy(custom_AIO_SERVER, AIO_SERVER_FIELD.getValue());
  custom_AIO_SERVERPORT = atoi(AIO_SERVERPORT_FIELD.getValue());
  strcpy(custom_AIO_USERNAME, AIO_USERNAME_FIELD.getValue());
  strcpy(custom_AIO_KEY, AIO_KEY_FIELD.getValue());

  // Display new data
  newConfigData();

  // Writing JSON config file to flash for next boot
  writeConfigFile();

  digitalWrite(LED_BUILTIN, LED_OFF); // Turn LED off as we are not in configuration mode.

  deleteOldInstances();

  MQTT_Pub_Topic = String(custom_AIO_USERNAME) + "/feeds/Temperature";
  createNewInstances();
}

bool readConfigFile() 
{
  // this opens the config file in read-mode
  File f = FileFS.open(CONFIG_FILE, "r");

  if (!f)
  {
    Serial.println(F("Config File not found"));
    return false;
  }
  else
  {
    // we could open the file
    size_t size = f.size();
    // Allocate a buffer to store contents of the file.
    std::unique_ptr<char[]> buf(new char[size + 1]);

    // Read and store file contents in buf
    f.readBytes(buf.get(), size);
    // Closing file
    f.close();
    // Using dynamic JSON buffer which is not the recommended memory model, but anyway
    // See https://github.com/bblanchon/ArduinoJson/wiki/Memory%20model

#if (ARDUINOJSON_VERSION_MAJOR >= 6)

    DynamicJsonDocument json(1024);
    auto deserializeError = deserializeJson(json, buf.get());
    
    if ( deserializeError )
    {
      Serial.println(F("JSON parseObject() failed"));
      return false;
    }
    
    serializeJson(json, Serial);
    
#else

    DynamicJsonBuffer jsonBuffer;
    // Parse JSON string
    JsonObject& json = jsonBuffer.parseObject(buf.get());
    
    // Test if parsing succeeds.
    if (!json.success())
    {
      Serial.println(F("JSON parseObject() failed"));
      return false;
    }
    
    json.printTo(Serial);
    
#endif

    // Parse all config file parameters, override
    // local config variables with parsed values
    if (json.containsKey(AIO_SERVER_Label))
    {
      strcpy(custom_AIO_SERVER, json[AIO_SERVER_Label]);
    }

    if (json.containsKey(AIO_SERVERPORT_Label))
    {
      custom_AIO_SERVERPORT = json[AIO_SERVERPORT_Label];
    }

    if (json.containsKey(AIO_USERNAME_Label))
    {
      strcpy(custom_AIO_USERNAME, json[AIO_USERNAME_Label]);
    }

    if (json.containsKey(AIO_KEY_Label))
    {
      strcpy(custom_AIO_KEY, json[AIO_KEY_Label]);
    }
  }
  
  Serial.println(F("\nConfig File successfully parsed"));
  
  return true;
}

bool writeConfigFile() 
{
  Serial.println(F("Saving Config File"));

#if (ARDUINOJSON_VERSION_MAJOR >= 6)
  DynamicJsonDocument json(1024);
#else
  DynamicJsonBuffer jsonBuffer;
  JsonObject& json = jsonBuffer.createObject();
#endif

  // JSONify local configuration parameters
  json[AIO_SERVER_Label] = custom_AIO_SERVER;
  json[AIO_SERVERPORT_Label] = custom_AIO_SERVERPORT;
  json[AIO_USERNAME_Label] = custom_AIO_USERNAME;
  json[AIO_KEY_Label] = custom_AIO_KEY;

  // Open file for writing
  File f = FileFS.open(CONFIG_FILE, "w");

  if (!f)
  {
    Serial.println(F("Failed to open Config File for writing"));
    return false;
  }

#if (ARDUINOJSON_VERSION_MAJOR >= 6)
  serializeJsonPretty(json, Serial);
  // Write data to file and close it
  serializeJson(json, f);
#else
  json.prettyPrintTo(Serial);
  // Write data to file and close it
  json.printTo(f);
#endif

  f.close();

  Serial.println(F("\nConfig File successfully saved"));
  return true;
}

// this function is just to display newly saved data,
// it is not necessary though, because data is displayed
// after WiFi manager resets ESP32
void newConfigData() 
{
  Serial.println();
  Serial.print(F("custom_AIO_SERVER: ")); 
  Serial.println(custom_AIO_SERVER);
  Serial.print(F("custom_SERVERPORT: ")); 
  Serial.println(custom_AIO_SERVERPORT);
  Serial.print(F("custom_USERNAME_KEY: ")); 
  Serial.println(custom_AIO_USERNAME);
  Serial.print(F("custom_KEY: ")); 
  Serial.println(custom_AIO_KEY);
  Serial.println();
}

void MQTT_connect() 
{
  int8_t ret;

  MQTT_Pub_Topic = String(custom_AIO_USERNAME) + "/feeds/Temperature";

  createNewInstances();

  // Return if already connected
  if (mqtt->connected()) 
  {
    return;
  }

  Serial.println(F("Connecting to MQTT (3 attempts)..."));

  uint8_t attempt = 3;
  
  while ((ret = mqtt->connect()) != 0) 
  { 
    // connect will return 0 for connected
    Serial.println(mqtt->connectErrorString(ret));
    Serial.println(F("Another attemtpt to connect to MQTT in 2 seconds..."));
    
    mqtt->disconnect();
    delay(2000);  // wait 2 seconds
    attempt--;
    
    if (attempt == 0) 
    {
      Serial.println(F("MQTT connection failed. Continuing with program..."));
      return;
    }
  }
  
  Serial.println(F("MQTT connection successful!"));
}

// Setup function
void setup()
{
  // Put your setup code here, to run once
  Serial.begin(115200);
  while (!Serial);

  Serial.print("\nStarting Async_ConfigOnDRD_FS_MQTT_Ptr on " + String(ARDUINO_BOARD));
  Serial.println(" using FileFS = " + String(FileFSType));

  // Initialize the LED digital pin as an output.
  pinMode(LED_BUILTIN, OUTPUT);

  bool FileFSReady = true;

  // Mount the filesystem, auto-format if not ready
#if ESP32

  // Format SPIFFS if not yet
  if (!FileFS.begin(true))
  {
    Serial.println(F("FileFS failed! Formatting."));
    
    if (!FileFS.begin())
    {
      Serial.println(F("FileFS failed!"));
      FileFSReady = false;
    }
  }
  
#else

  // Format LittleFS/SPIFFS if not yet 
  if (!FileFS.begin())
  {
    Serial.println(F("FileFS failed! Formatting."));
    
    FileFS.format();
    
    if (!FileFS.begin())
    {
      Serial.println(F("FileFS failed!"));
      FileFSReady = false;
    }
  }
  
#endif

  Serial.print(F("FileFS opened: "));
  Serial.println(FileFSReady? F("OK") : F("Failed"));

  if (!readConfigFile())
  {
    Serial.println(F("Can't read Config File, using default values"));
  }

  drd = new DoubleResetDetector(DRD_TIMEOUT, DRD_ADDRESS);

  if (!drd)
    Serial.println(F("Can't instantiate. Disable DRD feature"));

  unsigned long startedAt = millis();

  //Here starts the WiFi Manager initialization
  //Local intialization. Once its business is done, there is no need to keep it around
  ESPAsync_WiFiManager ESPAsync_wifiManager(&webServer, &dnsServer, "ConfigOnSwichFS-MQTT");

  ESPAsync_wifiManager.setMinimumSignalQuality(-1);

  // From v1.0.10 only
  // Set config portal channel, default = 1. Use 0 => random channel from 1-13
  ESPAsync_wifiManager.setConfigPortalChannel(0);
  //////

  //set custom ip for portal
  //ESPAsync_wifiManager.setAPStaticIPConfig(IPAddress(192, 168, 100, 1), IPAddress(192, 168, 100, 1), IPAddress(255, 255, 255, 0));
    
#if !USE_DHCP_IP    
  #if USE_CONFIGURABLE_DNS
    // Set static IP, Gateway, Subnetmask, DNS1 and DNS2. New in v1.0.5
    ESPAsync_wifiManager.setSTAStaticIPConfig(stationIP, gatewayIP, netMask, dns1IP, dns2IP);
  #else
    // Set static IP, Gateway, Subnetmask, Use auto DNS1 and DNS2.
    ESPAsync_wifiManager.setSTAStaticIPConfig(stationIP, gatewayIP, netMask);
  #endif 
#endif  

  // We can't use WiFi.SSID() in ESP32as it's only valid after connected.
  // SSID and Password stored in ESP32 wifi_ap_record_t and wifi_config_t are also cleared in reboot
  // Have to create a new function to store in EEPROM/SPIFFS for this purpose
  Router_SSID = ESPAsync_wifiManager.WiFi_SSID();
  Router_Pass = ESPAsync_wifiManager.WiFi_Pass();

  //Remove this line if you do not want to see WiFi password printed
  Serial.println("Stored: SSID = " + Router_SSID + ", Pass = " + Router_Pass);

  // SSID to uppercase
  ssid.toUpperCase();

  if (Router_SSID != "")
  {
    ESPAsync_wifiManager.setConfigPortalTimeout(60); //If no access point name has been previously entered disable timeout.
    Serial.println(F("Got stored Credentials. Timeout 60s for Config Portal"));
  }
  else
  {
    Serial.println(F("Open Config Portal without Timeout: No stored Credentials."));
    initialConfig = true;
  }

  if (drd && drd->detectDoubleReset())
  {
    // DRD, disable timeout.
    ESPAsync_wifiManager.setConfigPortalTimeout(0);
    
    Serial.println(F("Open Config Portal without Timeout: Double Reset Detected"));
    initialConfig = true;
  }

  if (initialConfig)
  {
    #if 1
    wifi_manager();
    #else
    // Starts an access point
    if (!ESPAsync_wifiManager.startConfigPortal((const char *) ssid.c_str(), password))
      Serial.println(F("Not connected to WiFi but continuing anyway."));
    else
      Serial.println(F("WiFi connected...yeey :)"));
    #endif
  }

  digitalWrite(LED_BUILTIN, LED_OFF); // Turn led off as we are not in configuration mode.

#define WIFI_CONNECT_TIMEOUT        30000L
#define WHILE_LOOP_DELAY            200L
#define WHILE_LOOP_STEPS            (WIFI_CONNECT_TIMEOUT / ( 3 * WHILE_LOOP_DELAY ))

  startedAt = millis();

  while ( (WiFi.status() != WL_CONNECTED) && (millis() - startedAt < WIFI_CONNECT_TIMEOUT ) )
  {
    WiFi.mode(WIFI_STA);
    WiFi.persistent (true);

    // We start by connecting to a WiFi network
    Serial.print(F("Connecting to "));
    Serial.println(Router_SSID);

    //WiFi.config(stationIP, gatewayIP, netMask);
    //WiFi.config(stationIP, gatewayIP, netMask, dns1IP, dns2IP);

    WiFi.begin(Router_SSID.c_str(), Router_Pass.c_str());

    int i = 0;
    while ((!WiFi.status() || WiFi.status() >= WL_DISCONNECTED) && i++ < WHILE_LOOP_STEPS)
    {
      delay(WHILE_LOOP_DELAY);
    }
  }

  Serial.print(F("After waiting "));
  Serial.print((millis() - startedAt) / 1000);
  Serial.print(F(" secs more in setup(), connection result is "));

  if (WiFi.status() == WL_CONNECTED)
  {
    Serial.print(F("connected. Local IP: "));
    Serial.println(WiFi.localIP());
  }
  else
    Serial.println(ESPAsync_wifiManager.getStatus(WiFi.status()));
}

// Loop function
void loop()
{
  // Call the double reset detector loop method every so often,
  // so that it can recognise when the timeout expires.
  // You can also call drd.stop() when you wish to no longer
  // consider the next reset as a double reset.
  if (drd)
    drd->loop();

  // this is just for checking if we are connected to WiFi
  check_status();
}
```

---
---

### Debug Termimal Output Samples

1. This is terminal debug output when running [Async_ConfigOnDRD_FS_MQTT_Ptr](examples/Async_ConfigOnDRD_FS_MQTT_Ptr) on  ***ESP32 ESP32_DEV.***. Config Portal was requested by DRD to input and save MQTT Credentials. The boards then connected to Adafruit MQTT Server successfully.

```
Starting Async_ConfigOnDRD_FS_MQTT_Ptr on ESP32_DEV using FileFS = SPIFFS
FileFS opened: OK
{"AIO_SERVER_Label":"io.adafruit.com","AIO_SERVERPORT_Label":1883,"AIO_USERNAME_Label":"your_account","AIO_KEY_Label":"aio_********"}
Config File successfully parsed
[WM] RFC925 Hostname = ConfigOnSwichFS-MQTT
[WM] setSTAStaticIPConfig for USE_CONFIGURABLE_DNS
Stored: SSID = HueNet1, Pass = 12345678
Got stored Credentials. Timeout 60s for Config Portal
SPIFFS Flag read = 0xd0d01234
doubleResetDetected
Saving config file...
Saving config file OK
Open Config Portal without Timeout: Double Reset Detected

Config Portal requested.
[WM] RFC925 Hostname = ConfigOnSwichFS-MQTT
Opening Config Portal. Got stored Credentials. Timeout 120s
[WM] Adding parameter AIO_SERVER_Label
[WM] Adding parameter AIO_SERVERPORT_Label
[WM] Adding parameter AIO_USERNAME_Label
[WM] Adding parameter AIO_KEY_Label
[WM] setSTAStaticIPConfig for USE_CONFIGURABLE_DNS
[WM] WiFi.waitForConnectResult Done
[WM] SET AP
[WM] 

[WM] Custom STA IP/GW/Subnet
[WM] DNS1 and DNS2 set
[WM] setWifiStaticIP IP = 192.168.2.232
[WM] Connected after waiting (s) : 1.20
[WM] Local ip = 192.168.2.232
[WM] Timed out connection result: WL_CONNECTED
Connected...yeey :)
Local IP: 192.168.2.232

custom_AIO_SERVER: io.adafruit.com
custom_SERVERPORT: 1883
custom_USERNAME_KEY: your_account
custom_KEY: aio_********

Saving Config File
{
  "AIO_SERVER_Label": "io.adafruit.com",
  "AIO_SERVERPORT_Label": 1883,
  "AIO_USERNAME_Label": "your_account",
  "AIO_KEY_Label": "aio_********"
}
Config File successfully saved

Creating new WiFi client object : OK
Creating new MQTT object : OK
AIO_SERVER = io.adafruit.com, AIO_SERVERPORT = 1883
AIO_USERNAME = your_account, AIO_KEY = aio_********
Creating new MQTT_Pub_Topic,  Temperature = your_account/feeds/Temperature
Creating new Temperature object : OK
Temperature MQTT_Pub_Topic = your_account/feeds/Temperature
[WM] freeing allocated params!
After waiting 0 secs more in setup(), connection result is connected. Local IP: 192.168.2.232
[WM] freeing allocated params!
Connecting to MQTT (3 attempts)...
MQTT connection successful!
TWTWTWTWTW TWTWTWTWTW TWTWTWTWTW TWTWTWTWTW 
```

2. This is terminal debug output when running [Async_ConfigOnSwitchFS_MQTT_Ptr](examples/Async_ConfigOnSwitchFS_MQTT_Ptr) on  ***ESP8266 NodeMCU 1.0.***. Config Portal was requested to input and save MQTT Credentials. The boards then connected to Adafruit MQTT Server successfully.

```
Starting Async_ConfigOnSwichFS_MQTT_Ptr on ESP8266_NODEMCU using FileFS = LittleFS

LittleFS opened: OK
Configuration file not found
Failed to read configuration file, using default values
[WM] RFC925 Hostname = ConfigOnSwichFS-MQTT
[WM] setSTAStaticIPConfig for USE_CONFIGURABLE_DNS
Stored: SSID = HueNet1, Pass = 12345678
Connecting to HueNet1
After waiting 5 secs more in setup(), connection result is connected. Local IP: 192.168.2.148
[WM] freeing allocated params!

Creating new WiFi client object OK
Creating new MQTT object OK
AIO_SERVER = , AIO_SERVERPORT = 0
AIO_USERNAME = , AIO_KEY = 
Creating new MQTT_Pub_Topic,  Temperature = /feeds/Temperature
Creating new Temperature object OK
Temperature MQTT_Pub_Topic = /feeds/Temperature
Connecting to WiFi MQTT (3 attempts)...
Connection failed
Another attemtpt to connect to MQTT in 2 seconds...
Connection failed
Another attemtpt to connect to MQTT in 2 seconds...
Connection failed
Another attemtpt to connect to MQTT in 2 seconds...
WiFi MQTT connection failed. Continuing with program...
FW
Button double clicked!
Connecting to WiFi MQTT (3 attempts)...
Connection failed
Another attemtpt to connect to MQTT in 2 seconds...
Connection failed
Another attemtpt to connect to MQTT in 2 seconds...
Connection failed
Another attemtpt to connect to MQTT in 2 seconds...
WiFi MQTT connection failed. Continuing with program...
FW
Button clicked!

Configuration Portal requested.
[WM] RFC925 Hostname = ConfigOnDoubleReset
Opening Configuration Portal. Got stored Credentials. Timeout 120s
[WM] Adding parameter AIO_SERVER_Label
[WM] Adding parameter AIO_SERVERPORT_Label
[WM] Adding parameter AIO_USERNAME_Label
[WM] Adding parameter AIO_KEY_Label
[WM] setSTAStaticIPConfig for USE_CONFIGURABLE_DNS
[WM] WiFi.waitForConnectResult Done
[WM] SET AP_STA
[WM] 
Configuring AP SSID = ESP_1190DD
[WM] AP PWD = your_password
[WM] AP Channel = 10
[WM] AP IP address = 192.168.4.1
[WM] HTTP server started
[WM] ESPAsync_WiFiManager::startConfigPortal : Enter loop
[WM] Custom STA IP/GW/Subnet
[WM] DNS1 and DNS2 set
[WM] setWifiStaticIP IP = 192.168.2.188
[WM] Connected after waiting (s) : 2.23
[WM] Local ip = 192.168.2.188
[WM] Timed out connection result: WL_CONNECTED
Connected...yeey :)
Local IP: 192.168.2.188
Saving config file
{
  "AIO_SERVER_Label": "io.adafruit.com",
  "AIO_SERVERPORT_Label": 1883,
  "AIO_USERNAME_Label": "your_account",
  "AIO_KEY_Label": "aio_********"
}
Config file was successfully saved
Deleting old MQTT object
Deleting old Temperature object
Creating new MQTT object OK
AIO_SERVER = io.adafruit.com, AIO_SERVERPORT = 1883
AIO_USERNAME = your_account, AIO_KEY = aio_********
Creating new MQTT_Pub_Topic,  Temperature = your_account/feeds/Temperature
Creating new Temperature object OK
Temperature MQTT_Pub_Topic = your_account/feeds/Temperature
[WM] freeing allocated params!
Connecting to WiFi MQTT (3 attempts)...
WiFi MQTT connection successful!
TWTWTWTWTW TWTWTWTWTW TWTWTWTWTW TWTWTWTWTW TWTWTWTW
```
---

3. This is terminal debug output when running [Async_ConfigOnDoubleReset](examples/Async_ConfigOnDoubleReset)  on  ***ESP32 ESP32_DEV.***. Config Portal was requested by DRD to input and save Credentials. The boards then connected to WiFi using new Static IP successfully.

```cpp
Starting ConfigOnDoubleReset on ESP32_DEV
[WM] RFC925 Hostname = ConfigOnDoubleReset
[WM] setSTAStaticIPConfig for USE_CONFIGURABLE_DNS
Stored: SSID = HueNet1, Pass = password
Got stored Credentials. Timeout 120s
SPIFFS Flag read = 0xd0d01234
doubleResetDetected
Saving config file...
Saving config file OK
Open Config Portal without Timeout: Double Reset Detected
Starting configuration portal.
[WM] WiFi.waitForConnectResult Done
[WM] SET AP
[WM] 
Configuring AP SSID = ESP_9ABF498
[WM] AP PWD = your_password
[WM] AP Channel = 11
[WM] AP IP address = 192.168.4.1
[WM] HTTP server started
[WM] ESPAsync_WiFiManager::startConfigPortal : Enter loop
[WM] Connecting to new AP
[WM] Previous settings invalidated
[WM] Custom STA IP/GW/Subnet
[WM] DNS1 and DNS2 set
[WM] setWifiStaticIP IP = 192.168.2.222
[WM] Connect to new WiFi using new IP parameters
[WM] Connected after waiting (s) : 0.60
[WM] Local ip = 192.168.2.222
[WM] Connection result:  WL_CONNECTED
WiFi connected...yeey :)
After waiting 0 secs more in setup(), connection result is connected. Local IP: 192.168.2.222
[WM] freeing allocated params!
HHHHHHHHHH HHHHHHHHHH HHHHHHHHHH HHHHHHHHHH
```
---

4. This is terminal debug output when running [Async_ConfigOnDoubleReset](examples/Async_ConfigOnDoubleReset)  on  ***ESP8266_NODEMCU.***. Config Portal was requested by DRD to input and save Credentials. The boards then connected to WiFi using new Static IP successfully.

```cpp
Starting Async_ConfigOnDoubleReset on ESP8266_NODEMCU
[WM] RFC925 Hostname = ConfigOnDoubleReset
[WM] setSTAStaticIPConfig for USE_CONFIGURABLE_DNS
Stored: SSID = HueNet1, Pass = 12345678
Got stored Credentials. Timeout 120s
LittleFS Flag read = 0xd0d01234
doubleResetDetected
Saving config file...
Saving config file OK
Open Config Portal without Timeout: Double Reset Detected
Starting configuration portal.
[WM] WiFi.waitForConnectResult Done
[WM] SET AP_STA
[WM] 
Configuring AP SSID = ESP_1190DD
[WM] AP PWD = your_password
[WM] AP Channel = 8
[WM] AP IP address = 192.168.4.1
[WM] HTTP server started
[WM] ESPAsync_WiFiManager::startConfigPortal : Enter loop
[WM] Request redirected to captive portal
[WM] Handle root
[WM] Info
[WM] Info page sent
[WM] Handle root
[WM] Handle WiFi
[WM] handleWifi: Scan done
[WM] Static IP = 192.168.2.186
[WM] Sent config page
[WM] WiFi save
[WM] New Static IP = 192.168.2.186
[WM] New Static Gateway = 192.168.2.1
[WM] New Static Netmask = 255.255.255.0
[WM] New Static DNS1 = 192.168.2.1
[WM] New Static DNS2 = 8.8.8.8
[WM] Sent wifi save page
[WM] Custom STA IP/GW/Subnet
[WM] DNS1 and DNS2 set
[WM] setWifiStaticIP IP = 192.168.2.186
[WM] Connected after waiting (s) : 2.22
[WM] Local ip = 192.168.2.186
[WM] Timed out connection result: WL_CONNECTED
WiFi connected...yeey :)
After waiting 0 secs more in setup(), connection result is connected. Local IP: 192.168.2.186
[WM] freeing allocated params!
HHHHHHHHHH HHHHHHHHHH HHH
```

---
---

### Debug
Debug is enabled by default on Serial. To disable, add before `startConfigPortal()`

```cpp
ESPAsync_wifiManager.setDebugOutput(false);
```

You can also change the debugging level from 0 to 4

```cpp
// Use from 0 to 4. Higher number, more debugging messages and memory usage.
#define _ESPASYNC_WIFIMGR_LOGLEVEL_    3
```
---

4. This is terminal debug output when running [Async_ConfigOnDoubleReset](examples/Async_ConfigOnDoubleReset)  on  ***ESP8266_NODEMCU.***. Config Portal was requested by DRD to input and save Credentials. The boards then connected to WiFi using new Static IP successfully.

```cpp
Starting Async_ConfigOnDoubleReset on ESP8266_NODEMCU
[WM] RFC925 Hostname = ConfigOnDoubleReset
[WM] setSTAStaticIPConfig for USE_CONFIGURABLE_DNS
Stored: SSID = HueNet1, Pass = 12345678
Got stored Credentials. Timeout 120s
LittleFS Flag read = 0xd0d01234
doubleResetDetected
Saving config file...
Saving config file OK
Open Config Portal without Timeout: Double Reset Detected
Starting configuration portal.
[WM] WiFi.waitForConnectResult Done
[WM] SET AP_STA
[WM] 
Configuring AP SSID = ESP_1190DD
[WM] AP PWD = your_password
[WM] AP Channel = 8
[WM] AP IP address = 192.168.4.1
[WM] HTTP server started
[WM] ESPAsync_WiFiManager::startConfigPortal : Enter loop
[WM] Request redirected to captive portal
[WM] Handle root
[WM] Info
[WM] Info page sent
[WM] Handle root
[WM] Handle WiFi
[WM] handleWifi: Scan done
[WM] Static IP = 192.168.2.186
[WM] Sent config page
[WM] WiFi save
[WM] New Static IP = 192.168.2.186
[WM] New Static Gateway = 192.168.2.1
[WM] New Static Netmask = 255.255.255.0
[WM] New Static DNS1 = 192.168.2.1
[WM] New Static DNS2 = 8.8.8.8
[WM] Sent wifi save page
[WM] Custom STA IP/GW/Subnet
[WM] DNS1 and DNS2 set
[WM] setWifiStaticIP IP = 192.168.2.186
[WM] Connected after waiting (s) : 2.22
[WM] Local ip = 192.168.2.186
[WM] Timed out connection result: WL_CONNECTED
WiFi connected...yeey :)
After waiting 0 secs more in setup(), connection result is connected. Local IP: 192.168.2.186
[WM] freeing allocated params!
HHHHHHHHHH HHHHHHHHHH HHH
```

---

5. This is terminal debug output when running [Async_ESP_FSWebServer_DRD](examples/Async_ESP_FSWebServer_DRD)  on  ***ESP8266_NODEMCU.***. Config Portal was requested by DRD to input and save Credentials. The boards then connected to WiFi using new Static IP successfully.

```cpp
Starting Async_ESP_FSWebServer_DRD using LittleFS on ESP8266_NODEMCU
Opening / directory
FS File: CanadaFlag_1.png, size: 40.25KB
FS File: CanadaFlag_2.png, size: 8.12KB
FS File: CanadaFlag_3.jpg, size: 10.89KB
FS File: drd.dat, size: 4B
FS File: edit.htm.gz, size: 4.02KB
FS File: graphs.js.gz, size: 1.92KB
FS File: index.htm, size: 3.63KB

[WM] RFC925 Hostname = AsyncESP-FSWebServer
[WM] setAPStaticIPConfig
[WM] setSTAStaticIPConfig for USE_CONFIGURABLE_DNS
Stored: SSID = HueNet1, Pass = 12345678
Got stored Credentials. Timeout 60s for Config Portal
LittleFS Flag read = 0xd0d01234
doubleResetDetected
Saving config file...
Saving config file OK
Open Config Portal without Timeout: Double Reset Detected
[WM] WiFi.waitForConnectResult Done
[WM] SET AP_STA
[WM] 
Configuring AP SSID = ESP_1190DD
[WM] AP PWD = your_password
[WM] AP Channel = 9
[WM] Custom AP IP/GW/Subnet = 
[WM] 192.168.100.1 192.168.100.1 255.255.255.0
[WM] AP IP address = 192.168.100.1
[WM] HTTP server started
[WM] ESPAsync_WiFiManager::startConfigPortal : Enter loop
[WM] Custom STA IP/GW/Subnet
[WM] DNS1 and DNS2 set
[WM] setWifiStaticIP IP = 192.168.2.186
[WM] Connected after waiting (s) : 2.22
[WM] Local ip = 192.168.2.186
[WM] Timed out connection result: WL_CONNECTED
WiFi connected...yeey :)

Connected! IP address: 192.168.2.186
HTTP server started @ 192.168.2.186
===============================================================
Open http://async-esp8266fs.local/edit to see the file browser
Using username = admin and password = admin
===============================================================
[WM] freeing allocated params!
```

You can access using the HTTP server IP (http://192.168.2.186) or its mDNS hostname (http://async-esp8266fs.local)

<p align="center">
    <img src="https://github.com/khoih-prog/ESPAsync_WiFiManager/blob/master/examples/Async_ESP_FSWebServer/pics/async-esp8266fs.local.png">
</p>

By going to http://192.168.2.186/edit or http://async-esp8266fs.local/edit, you can **edit / delete / upload / download** any file in the folder 

<p align="center">
    <img src="https://github.com/khoih-prog/ESPAsync_WiFiManager/blob/master/examples/Async_ESP_FSWebServer/pics/async-esp8266fs.local_edit.png">
</p>

---
---

### Troubleshooting

If you get compilation errors, more often than not, you may need to install a newer version of the `ESP32 / ESP8266` core for Arduino.

Sometimes, the library will only work if you update the `ESP32 / ESP8266` core to the latest version because I am using some newly added function.

If you connect to the created configuration Access Point but the ConfigPortal does not show up, just open a browser and type in the IP of the web portal, by default `192.168.4.1`.

---

### Issues ###

Submit issues to: [ESPAsync_WiFiManager issues](https://github.com/khoih-prog/ESPAsync_WiFiManager/issues)

---
---

### Releases 1.0.11

1. Initial coding to use ESPAsyncWebServer instead of (ESP8266)WebServer.
2. Add more features and error checking to many examples.
3. Add example [Async_ConfigOnDRD_FS_MQTT_Ptr](examples/Async_ConfigOnDRD_FS_MQTT_Ptr)
4. Bump up to v1.0.11 to sync with ESP_WiFiManager v1.0.11.

---
---

This library is based on, modified, bug-fixed and improved from:

1. [`Tzapu's WiFiManager`](https://github.com/tzapu/WiFiManager)
2. [`Ken Taylor's WiFiManager`](https://github.com/kentaylor/WiFiManager)
3. [`Alan Steremberg's ESPAsyncWiFiManager`](https://github.com/alanswx/ESPAsyncWiFiManager)
4. [`Khoi Hoang's ESP_WiFiManager`](https://github.com/khoih-prog/ESP_WiFiManager)

to use the better **asynchronous** [ESPAsyncWebServer](https://github.com/me-no-dev/ESPAsyncWebServer) instead of (ESP8266)WebServer.

### Contributions and Thanks

1. Based on and modified from [Tzapu](https://github.com/tzapu/WiFiManager), [KenTaylor's version]( https://github.com/kentaylor/WiFiManager), [`Alan Steremberg's ESPAsyncWiFiManager`](https://github.com/alanswx/ESPAsyncWiFiManager) and [`Khoi Hoang's ESP_WiFiManager`](https://github.com/khoih-prog/ESP_WiFiManager).
2. Thanks to [me-no-dev](https://github.com/me-no-dev) for great [ESPAsyncWebServer Library](https://github.com/me-no-dev/ESPAsyncWebServer)
3. Thanks to good work of [Miguel Alexandre Wisintainer](https://github.com/tcpipchip) for working with, developing, debugging and testing.
4. Thanks to [cancodr](https://github.com/cancodr) for requesting an enhancement in [Issue #29: Is it possible to use AsyncWebServer.h instead of WebServer.h?](https://github.com/khoih-prog/ESP_WiFiManager/issues/29), leading to this [ESPAsync_WiFiManager Library](https://github.com/khoih-prog/ESPAsync_WiFiManager).


<table>
  <tr>
    <td align="center"><a href="https://github.com/me-no-dev"><img src="https://github.com/me-no-dev.png" width="100px;" alt="me-no-dev"/><br /><sub><b>⭐️⭐️ me-no-dev</b></sub></a><br /></td>
    <td align="center"><a href="https://github.com/Tzapu"><img src="https://github.com/Tzapu.png" width="100px;" alt="Tzapu"/><br /><sub><b>⭐️ Tzapu</b></sub></a><br /></td>
    <td align="center"><a href="https://github.com/kentaylor"><img src="https://github.com/kentaylor.png" width="100px;" alt="kentaylor"/><br /><sub><b>⭐️ kentaylor</b></sub></a><br /></td>
    <td align="center"><a href="https://github.com/alanswx"><img src="https://github.com/alanswx.png" width="100px;" alt="alanswx"/><br /><sub><b>⭐️ Alan Steremberg</b></sub></a><br /></td>
    <td align="center"><a href="https://github.com/tcpipchip"><img src="https://github.com/tcpipchip.png" width="100px;" alt="tcpipchip"/><br /><sub><b>tcpipchip</b></sub></a><br /></td>
    <td align="center"><a href="https://github.com/cancodr"><img src="https://github.com/cancodr.png" width="100px;" alt="cancodr"/><br /><sub><b>cancodr</b></sub></a><br /></td>
  </tr> 
</table>

### Contributing

If you want to contribute to this project:
- Report bugs and errors
- Ask for enhancements
- Create issues and pull requests
- Tell other people about this library

---

### License and credits ###

- The library is licensed under [MIT](https://github.com/khoih-prog/WebSockets2_Generic/blob/master/LICENSE)

---

## Copyright

Copyright 2020- Khoi Hoang


