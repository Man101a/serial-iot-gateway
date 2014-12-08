GLIDERBITS - Serial IoT Gateway
===============================
The GLIDERBITS Serial IoT Gateway is an open source (GNU GPL v3), open hardware (CC BY-SA 3.0) Serial-Ethernet module that you can use to very easly send to or get data from Internet of Things services cloud.

## How to use it

Just connect the module to your microcontroller using a serial line communication (GND, TX, RX, +5V) and send string commands to the module. Example:
```C
Serial.println("K:xively:YOURAPIKEY\n");
Serial.println("P:xively:12345\nMyTemperature:-3.2\n");
```
And it will update the MyTemperature to -3.2 in your xively account in the 12345 feed.

## Suported data services

- [ ] Xively
- [ ] Emoncms
- [ ] Data.Sparkfun

### Xively
http://xively.com

Limits:

### Emoncms
http://emoncms.org

Limits:
> http://emoncms.org/site/usage
> Post rate limit:
> 5-10s.. keep the brakes on your arduino's and nanodes!

### Data.Sparkfun
https://data.sparkfun.com
https://learn.sparkfun.com/tutorials/pushing-data-to-datasparkfuncom/what-is-phant

Limits:
> https://data.sparkfun.com
> Each stream has a maximum of 50mb. After you hit the limit, the oldest data will be erased. (These limitations can be removed if installed on your own server). Logging is limited to 100 pushes in a 15 minute window. This allows you to push data in bursts, or spread them out over the 15 minute window."


## Serial Protocol

### Module configurations

"RESET"

### Data services commands
The protocol is the same for all services. However each service have different meanings for their feeds (feeds, streams, .. )

"K:service:YOUR_API_KEY\n"<br>
"P:service:optional_feed_id\nfeed:value\n\n"<br>
"G:service:optional_feed_id\nfeed\n"<br>

K - Configure the API Key to use in this sessions. You can setup it just once, it will keep this same API key for the next posts and gets.<br>
P - Post one or multiple data. You can send multiple "feed:value\n" in the same sequence. In the end just send '\n'<br>
G - Get one data value from service<br>

#### Xively
"K:xively:YOUR_API_KEY\n"<br>
"P:xively:feed_id\nfeed:value\n\n"<br>
"G:service:optional_feed_id\nfeed\n"<br>

#### Emoncms
"K:emoncms:YOUR_API_KEY\n"<br>
"P:emoncms:optinal_feed_id\nfeed:value\n\n"<br>
"G:service:optional_feed_id\nfeed\n"<br>

#### Data.Sparkfun
"K:sparkfun:YOUR_API_KEY\n"<br>
"P:sparkfun:optinal_feed_id\nfeed:value\n\n"<br>
"G:service:optional_feed_id\nfeed\n"<br>

### Misc services

## Licence
