## <i class="fa fa-code"></i> Constructor

### AutoConnectConfig

```cpp
AutoConnectConfig()
```  
```cpp
AutoConnectConfig(const char* ap, const char* password)
```
```cpp
AutoConnectConfig(const char* ap, const char* password, const unsigned long timeout)
```
```cpp
AutoConnectConfig(const char* ap, const char* password, const unsigned long timeout, const uint8_t channel)
```
<dl class="apidl">
    <dt>**Parameters**</dt>
    <dd><span class="apidef">ap</span>SSID for SoftAP. The length should be up to 31. The default value is **esp8266ap** for ESP8266, **esp32ap** for ESP32.</dd>
    <dd><span class="apidef">password</span>Password for SodtAP. The length should be from 8 to up to 63. The default value is **12345678**.</dd>
    <dd><span class="apidef">timeout</span>The timeout value of the captive portal in [ms] units. The default value is 0.</dd>
    <dd><span class="apidef">channel</span>The channel number of WIFi when SoftAP starts. The default values is 1.</dd>
</dl>

## <i class="fa fa-code"></i> Public member variables

### <i class="fa fa-caret-right"></i> apid

SoftAP's SSID.
<dl class="apidl">
    <dt>**Type**</dt>
    <dd>String</dd>
</dl>

### <i class="fa fa-caret-right"></i> apip

Sets IP address for Soft AP in captive portal. When AutoConnect fails the initial WiFi.begin, it starts the captive portal with the IP address specified this.
<dl class="apidl">
    <dt>**Type**</dt>
    <dd><span class="apidef" style="width:230px;">IPAddress</span>The default value is **192.168.244.1**</dd>
</dl>

### <i class="fa fa-caret-right"></i> autoReconnect

Automatically will try to reconnect with the past established access point (BSSID) when the current configured SSID in ESP8266/ESP32 could not be connected. By enabling this option, *AutoConnect::begin()* function will attempt to reconnect to a known access point using credentials stored in the EEPROM, even if the connection failed by current SSID.  
If the connection fails, starts the captive portal in SoftAP + STA mode.  
<dl class="apidl">
    <dt>**Type**</dt>
    <dd>bool</dd>
    <dt>**Value**</dt>
    <dd><span class="apidef" style="width:230px;">true</span>Reconnect automatically.</dd>
    <dd><span class="apidef" style="width:230px;">false</span>Starts Captive Portal in SoftAP + STA mode without trying to reconnect. This is the default.</dd>
</dl>

When the autoReconnect option is enabled, an automatic connection will behave if the following conditions are satisfied.

- Invokes *AutoConnect::begin* without user name and password parameter as ```begin()```.
- If one of the saved BSSIDs (not the SSID) of the credentials matches the BSSID detected by the network scan.

### <i class="fa fa-caret-right"></i> autoReset

Reset ESP8266 module automatically after WLAN disconnected.
<dl class="apidl">
    <dt>**Type**</dt>
    <dd>bool</dd>
    <dt>**Value**</dt>
    <dd><span class="apidef" style="width:230px;">true</span>Reset after WiFi disconnected automatically.</dd>
    <dd><span class="apidef" style="width:230px;">false</span>No reset.</dd>
</dl>

### <i class="fa fa-caret-right"></i> autoRise

Captive portal activation switch. False for disabling the captive portal. It prevents starting the captive portal even if the connection at the first *WiFi.begin* fails.
<dl class="apidl">
    <dt>**Type**</dt>
    <dd>bool</dd>
    <dt>**Value**</dt>
    <dd><span class="apidef" style="width:230px;">true</span>Enable the captive portal. This is the default.</dd>
    <dd><span class="apidef" style="width:230px;">false</span>Disable the captive portal.</dd>
</dl>

### <i class="fa fa-caret-right"></i> autoSave

The credential saved automatically at the connection establishment.
<dl class="apidl">
    <dt>**Type**</dt>
    <dd>AC_SAVECREDENTIAL_t</dd>
    <dt>**Value**</dt>
    <dd><span class="apidef" style="width:230px;">AC_SAVECREDENTIAL_AUTO</span>The credential saved automatically. This is the default.</dd>
    <dd><span class="apidef" style="width:230px;">AC_SAVECREDENTIAL_NEVER</span>The credential no saved.</dd>
</dl>

### <i class="fa fa-caret-right"></i> bootUri

Specify the location to be redirected after module reset in the AutoConnect menu. It is given as an enumeration value of **AC_ONBOOTURI_t** indicating either the AutoConnect root path or the user screen home path.
<dl class="apidl">
    <dt>**Type**</dt>
    <dd>AC_ONBOOTURI_t</dd>
    <dt>**Value**</dt>
    <dd><span class="apidef" style="width:230px;">AC_ONBOOTURI_ROOT</span>Resetting the module redirects it to the AutoConnect root path. The root path is assumed to be AUTOCONNECT_URI defined in AutoConnectDefs.h.</dd>
    <dd><span class="apidef" style="width:230px;">AC_ONBOOTURI_HOME</span>It is redirected to the uri specified by [**AutoConnectConfig::homeUri**](apiconfig.md#homeuri).</dd>
</dl>

### <i class="fa fa-caret-right"></i> boundaryOffset

Sets the offset address of the credential storage area for EEPROM. This value must be between greater than 4 and less than flash sector size. (4096 by SDK)  
The default value is 0.
<dl class="apidl">
    <dt>**Type**</dt>
    <dd>uint16_t</dd>
</dl>

!!! warning "It will conflict with user data."
    If the sketch leaves this offset at zero, it will conflict the storage area of credentials with the user sketch owned data. It needs to use the behind of credential area.

### <i class="fa fa-caret-right"></i> channel

The channel number of WIFi when SoftAP starts.
<dl class="apidl">
    <dt>**Type**</dt>
    <dd>uint8_t</dd>
    <dt>**Value**</dt>
    <dd>1 ~ 14. The default value is 1.</dd>
</dl>

!!! info "How do I choose Channel"
    Espressif Systems had announced the [application note](https://www.espressif.com/sites/default/files/esp8266_wi-fi_channel_selection_guidelines.pdf) about Wi-Fi channel selection.

### <i class="fa fa-caret-right"></i> dns1

Set primary DNS server address when using static IP address.
<dl class="apidl">
    <dt>**Type**</dt>
    <dd>IPAddress</dd>
</dl>

### <i class="fa fa-caret-right"></i> dns2

Set secondary DNS server address when using static IP address.
<dl class="apidl">
    <dt>**Type**</dt>
    <dd>IPAddress</dd>
</dl>

### <i class="fa fa-caret-right"></i> gateway

Sets gateway address for Soft AP in captive portal. When AutoConnect fails the initial WiFi.begin, it starts the captive portal with the IP address specified this.
<dl class="apidl">
    <dt>**Type**</dt>
    <dd><span class="apidef" style="width:230px;">IPAddress</span>The default value is **192.168.244.1**</dd>
</dl>

### <i class="fa fa-caret-right"></i> hidden

Sets SoftAP to hidden SSID.
<dl class="apidl">
    <dt>**Type**</dt>
    <dd>uint8_t</dd>
    <dt>**Value**</dt>
    <dd><span class="apidef" style="width:230px;">0</span>SSID will be appeared. This is the default.</dd>
    <dd><span class="apidef" style="width:230px;">1</span>SSID will be hidden.</dd>
</dl>

### <i class="fa fa-caret-right"></i> homeUri

Sets the home path of user sketch. This path would be linked from 'HOME' in the AutoConnect menu. The default for homeUri is "/".
<dl class="apidl">
    <dt>**Type**</dt>
    <dd>String</dd>
</dl>

### <i class="fa fa-caret-right"></i> hostName

Sets the station host name of ESP8266/ESP32.
<dl class="apidl">
    <dt>**Type**</dt>
    <dd>String</dd>
</dl>

### <i class="fa fa-caret-right"></i> immediateStart

Disable the first WiFi.begin() and start the captive portal. If this option is enabled, the module will be in AP_STA mode and the captive portal will be activated regardless of [**AutoConnectConfig::autoRise**](apiconfig.md#autorise) specification.
<dl class="apidl">
    <dt>**Type**</dt>
    <dd>bool</dd>
    <dt>**Value**</dt>
    <dd><span class="apidef" style="width:230px;">true</span>Start the captive portal with [**AutoConnect::begin**](api.md#begin).</dd>
    <dd><span class="apidef" style="width:230px;">false</span>Enable the first WiFi.begin() and it will start captive portal when connection failed. This is default.</dd>
</dl>

### <i class="fa fa-caret-right"></i> netmask

Sets subnet mask for Soft AP in captive portal. When AutoConnect fails the initial WiFi.begin, it starts the captive portal with the IP address specified this.
<dl class="apidl">
    <dt>**Type**</dt>
    <dd><span class="apidef" style="width:230px;">IPAddress</span>The default value is **255.255.255.0**</dd>
</dl>

### <i class="fa fa-caret-right"></i> portalTimeout

Specify the timeout value of the captive portal in [ms] units. It is valid when the station is not connected and does not time out if the station is connected to the ESP module in SoftAP mode (ie Attempting WiFi connection with the portal function). If 0, the captive portal will not be timed-out.
<dl class="apidl">
    <dt>**Type**</dt>
    <dd><span class="apidef" style="width:230px;">unsigned long</span>Captive portal timeout value. The default value is 0.</dd>
</dl>

### <i class="fa fa-caret-right"></i> psk

Sets password for SoftAP. The length should be from 8 to up to 63. The default value is **12345678**.
<dl class="apidl">
    <dt>**Type**</dt>
    <dd>String</dd>
</dl>

### <i class="fa fa-caret-right"></i> retainlPortal

Specify whether to continue the portal function even if the captive portal timed out. If the true, when a timeout occurs, the [**AutoConnect::begin**](api.md#begin) function is exited with returns false, but the portal facility remains alive. So SoftAP remains alive and you can invoke AutoConnect while continuing sketch execution. The default is false.
<dl class="apidl">
    <dt>**Type**</dt>
    <dd>bool</dd>
    <dt>**Value**</dt>
    <dd><span class="apidef" style="width:230px;">true</span>Continue the portal function even if the captive portal times out. The STA + SoftAP mode of the ESP module continues and accepts the connection request to the AP.</dd>
    <dd><span class="apidef" style="width:230px;">false</span>When the captive portal times out, STA + SoftAP mode of the ESP module is stopped. This is default.</dd>
</dl>

!!! hint "Connection request after timed-out"
    With the **retainPortal**, even if AutoConnect::begin in the setup() is timed out, you can execute the sketch and the portal function as a WiFi connection attempt by calling AutoConnect::handleClient in the loop().

### <i class="fa fa-caret-right"></i> staip

Set a static IP address. The IP will behave with STA mode.
<dl class="apidl">
    <dt>**Type**</dt>
    <dd>IPAddress</dd>
</dl>

### <i class="fa fa-caret-right"></i> staGateway

Set the gateway address when using static IP address.
<dl class="apidl">
    <dt>**Type**</dt>
    <dd>IPAddress</dd>
</dl>

### <i class="fa fa-caret-right"></i> staNetmask

Set the subnetmask when using static IP address.
<dl class="apidl">
    <dt>**Type**</dt>
    <dd>IPAddress</dd>
</dl>

## <i class="fa fa-code"></i> AutoConnectConfig example

```cpp
AutoConenct        Portal;
AutoConenctConfig  Config("", "passpass");    // SoftAp name is determined at runtime
Config.apid = ESP.hostname();                 // Retrieve host name to SotAp identification
Config.apip = IPAddress(192,168,10,101);      // Sets SoftAP IP address
Config.gateway = IPAddress(192,168,10,1);     // Sets WLAN router IP address
Config.netmask = IPAddress(255,255,255,0);    // Sets WLAN scope
Config.autoReconnect = true;                  // Enable auto-reconnect
Config.autoSave = AC_SAVECREDENTIAL_NEVER;    // No save credential
Config.boundaryOffet = 64;                    // Reserve 64 bytes for the user data in EEPROM.
Config.portalTimeout = 60000;                 // Sets timeout value for the captive portal
Config.retainPortal = true;                   // Retains the portal function after timed-out
Config.homeUri = "/index.html"				  // Sets home path of the sketch application
Config.staip = IPAddress(192,168,10,10);      // Sets static IP
Config.staGateway = IPAddress(192,168,10,1);  // Sets WiFi router address
Config.staNetmask = IPAddress(255,255,255,0); // Sets WLAN scope
Config.dns1 = IPAddress(192,168,10,1);        // Sets primary DNS address
Portal.config(Config);                        // Configure AutoConnect
Portal.begin();                               // Starts and behaves captive portal
```