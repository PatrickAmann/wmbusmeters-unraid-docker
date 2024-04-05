
# Example configuration
  

Adjust configuration File ```/wmbusmeters_data/etc/wmbusmeters.conf``` to match your system configuration

This configuration works with a nanoCUL Dongle from [smart-home-komponente.de](https://www.smart-home-komponente.de/nano-cul/nano-cul-868/) running the nanoCUL_r568_mbus_c1t1_bufsize300 firmware provided by the developers from [wmbusmeters](https://github.com/wmbusmeters/wmbusmeters-wiki/blob/master/nanoCUL.md)
 
```
loglevel=normal
# set USB-Stick for IMST 871A for a wmbus device and meter-type = 40; set it to c1.
# set USB-Stick for IMST 871A for a wmbus device and meter-type = 41; set it to t1.
device=/dev/ttyUSB0:cul:c1
# But do not probe this serial tty.
donotprobe=/dev/ttyAMA0
logtelegrams=true
format=json
meterfiles=/wmbusmeters_data/logs/meter_readings
meterfilesaction=overwrite
meterfilesnaming=name-id
meterfilestimestamp=day
logfile=/wmbusmeters_data/logs/wmbusmeters.log
shell=/usr/local/bin/mosquitto_pub -h mqtt-host -P password -u username -t wmbusmeters/$METER_ID -m "$METER_JSON"
alarmshell=/usr/local/bin/mosquitto_pub -h mqtt-host -P password -u username -t wmbusmeters_alarm -m "$ALARM_TYPE $ALARM_MESSAGE"
alarmtimeout=1h
alarmexpectedactivity=mon-sun(00-23)
```

create a configuration file for your Meter in ```/wmbusmeters_data/etc/wmbusmeters.d``` with the following info matching your meter 

```
name=Multical21
id=11112222333
key=00112233445566778899AABBCCDDEEFF
driver=multical21
```
