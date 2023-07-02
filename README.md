# Wlanthermo
After trying and copy&paste a lot of code I have found, I was not able to to get WlanThermo running in Home Assistant. So I played around and integrated it my own.

This code is based on the work of others! So credit to these people:  
mfdir: https://github.com/mfdlr/homeassistant-wlanthermo  
m0uH: https://github.com/m0uH/homeassistant-wlanthermo  
dermichahc: https://wlanthermo.de/threads/home-assistant-wlanthermo-nano.575/#post-5576

### configuration.yaml changes

Besides the files in repo, which you need to add to your config folder, you need to add some stuff to configuration.yaml:
```yaml
mqtt: !include mqtt.yaml
sensor: !include sensor.yaml
input_number: !include input_number.yaml
input_datetime: !include input_datetime.yaml
input_text: !include input_text.yaml
input_boolean: !include input_boolean.yaml

template: !include template.yaml
switch: !include switch.yaml
automation: !include automations.yaml
```
### Additional plugins for displaying dashboard
Also you need to add some custom components from HACS if you want to use the Layout I provided in bbq.yaml:  
https://github.com/thomasloven/lovelace-badge-card  
https://github.com/thomasloven/lovelace-layout-card  
https://github.com/iantrich/config-template-card  
https://github.com/custom-cards/button-card  
https://github.com/maykar/kiosk-mode  
https://github.com/ofekashery/vertical-stack-in-card  
https://github.com/RomRider/apexcharts-card  

Please refer to the quidlines in readme of HASC and github repo how to add all these. For my files, the easiest way is to add "File editor" from HA Add-on store and create files with same name, add content and save.  
For the bbq.yaml, create new Dashboard, go to 3 dots at top right, edit and edit raw configuration yaml. Then paste content and save.

### MQTT setup

To get information from WlanThermo to Home Assistant, you need a MQTT broker. I use [Mosquitto broker](https://github.com/home-assistant/addons/blob/master/mosquitto/DOCS.md "Mosquitto broker") for that and set WlanThermo to work with it. Change IP to you HA IP  
![MQTT](https://raw.githubusercontent.com/MStapelfeldt/wlanthermo/main/WT-MQTT.PNG "MQTT")  
It is important you change your host to **MINIV3** to make the files work without changes, otherwise change **mqtt.yaml** to fit your name.  

![System](https://raw.githubusercontent.com/MStapelfeldt/wlanthermo/main/WT%20system.PNG "System")
```
 # change MINIV3 to your host these 2 lines:
    state_topic: "WLanThermo/MINIV3/status/data"
    json_attributes_topic: "WLanThermo/MINIV3/status/data"
```
### Final Dashboard
After adding all files, change configuration.yaml, setting up MQTT and installing addons, you should be able to see this Dashboard:  
![Dashboard](https://raw.githubusercontent.com/MStapelfeldt/wlanthermo/main/WT%20Dashboard.PNG "Dashboard")  
- Top row shows temprature of all 8 channels. If you press one of these, Detail view comes up in 3rd row.
- Tecond row shows Timer on the left site (times are quest by calculation. :D ) when BBQ is ready.
- Right site shows the Pitmaster1 Settings. "Soll" is a input_number to set temperature. Modus and Profile can be selected from WT Settings. The Channel I would recomment to leave at 9.
- Third row left site is the current selected channel (see top row buttons). You can adjust the temperature and alarms for each channel or Pitmaster 2.
- Right site is the graph with all your history temperatures. I am not 100% happy with that right now, so changes may come in future. (Hide unused channels and stuff)

Have fun and post to [WlanThermo Forum](https://wlanthermo.de/threads/home-assistant-wlanthermo-nano.575/ "WlanThermo Forum") if you have questions.
