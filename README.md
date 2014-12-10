Serial IoT Gateway
==================
The GLIDERBITS's Serial IoT Gateway is an open source (GNU GPL v3), open hardware (CC BY-SA 3.0) serial-ethernet module that you can use to very easly connect to the Internet of Things.

## How to use it

Just connect the module to your microcontroller using a serial line communication (GND, TX, RX, +5V) and send string commands to the module. Example:
```C++
Serial.println("K:xively:YOURAPIKEY\n");
Serial.println("P:xively:12345\nMyTemperature:-3.2\n");
```
That will update the MyTemperature to -3.2 in your xively account in the 12345 feed. Easy? A more complete Arduino example that updates a channel feed with an analog input value:

```C++
void setup()
{
  Serial.begin(9600);                       // Setup serial port speed
}

void loop()
{
  String strAnalogPin0 = String(analogRead(0), DEC);  // Read analog value from channel 0
  Serial.println("K:xively:YOURAPIKEY\n");  // Set up API key
  Serial.println("P:xively:12345\nAnalogPin0:" + strAnalogPin0 + "\n"); // Post it!
  delay(60 * 1000); // 1 minute delay
}
```

## Suported data services

- [ ] Xively
- [ ] Emoncms
- [ ] Data.Sparkfun
- [ ] ThingSpeak

### Xively
http://xively.com

#### Terms and conditions:
> https://xively.com/dev/docs/api/communicating/usage_limits/
> https://xively.com/dev/docs/api/api_terms_and_conditions/

### Emoncms
http://emoncms.org

#### Terms and conditions:
> http://emoncms.org/site/usage
> "Post rate limit: 5-10s.. keep the brakes on your arduino's and nanodes!"

### Data.Sparkfun
https://data.sparkfun.com
https://learn.sparkfun.com/tutorials/pushing-data-to-datasparkfuncom/what-is-phant

#### Terms and conditions:
> https://data.sparkfun.com
> "Each stream has a maximum of 50mb. After you hit the limit, the oldest data will be erased. (These limitations can be removed if installed on your own server). Logging is limited to 100 pushes in a 15 minute window. This allows you to push data in bursts, or spread them out over the 15 minute window."

### ThingSpeak
https://thingspeak.com

#### Terms and conditions:
> http://community.thingspeak.com/documentation/api/
> "API Rate Limit: The open service via ThingSpeak.com has a rate limit of an update per channel every 15 seconds."

## Serial Protocol

### Module configurations

"C:RESET\n" - Reset module<br>
"C:ack:0\n" - Disable acknowledge of messages<br>
"C:ack:1\n" - Enable acknowledge of messages<br>

### Data services commands
The protocol is the same for all services. However, mind that each service have different meanings for their feeds (feeds, streams, ... )

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
"P:emoncms:optional_feed_id\nfeed:value\n\n"<br>
"G:service:optional_feed_id\nfeed\n"<br>

#### Data.Sparkfun
"K:sparkfun:YOUR_API_KEY\n"<br>
"P:sparkfun:optional_feed_id\nfeed:value\n\n"<br>
"G:service:optional_feed_id\nfeed\n"<br>

### Misc services

## Licences

### Source code licence

    Copyright (C) 2014  Mario Luzeiro

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <http://www.gnu.org/licenses/>.

### Hardware licence

    The hardware files are licensed under the Creative Commons Attribution-Share Alike 3.0 Unported License
    (CC BY-SA 3.0)
    http://creativecommons.org/licenses/by-sa/3.0/deed.en
  
