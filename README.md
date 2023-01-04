# IR-Beam-Sensor
IR Beam Sensor for Home Assistant using ESPHome. Detect when someone crosses an IR beam.

## Parts
- [Indoor beam sensor](https://www.amazon.co.uk/gp/product/B07BTZDNBC/ref=ppx_yo_dt_b_search_asin_image?ie=UTF8&psc=1)
- [Outdoor beam sensor](https://www.amazon.co.uk/gp/product/B01M14S944/ref=ppx_yo_dt_b_search_asin_image?ie=UTF8&psc=1)
- [DC power jack - DC005](https://www.amazon.co.uk/gp/product/B07F68RZY9/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1)
- Wemos D1 Mini
- XH-2A connectors

## Wiring

## Brief History

### V1
I followed [this excellent tutorial](https://www.inspectmygadgets.com/ir-beam-break-sensors-with-tasmota-and-home-assistant/), to use Tasmota on a Wemos D1 Mini.
Ideally, I wanted all my projects to be in ESPHome and preferred Tasmota to be used for switches only.

The following code is placed inside the mqtt.yaml
```
binary_sensor:
  - name: "Beam sensor motion"
    state_topic: "stat/Front_garden_beam_sensor/POWER"
    payload_on: "ON"
    payload_off: "OFF"
    qos: 0
    device_class: motion
    icon: "mdi:leak"
```


### V2
I created my first PCB using EasyEDA and used a [voltage regulator from Amazon] (https://www.amazon.co.uk/gp/product/B07PPKR4HW/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1), I should have paid more attention as it was a: 
> 5.5V DC Voltage Regulator Step Down Power Supply Module 4.75V-12V to 5V 800mA
Which seemed to work fine on the protype board but destroyed (3) ESP8266's when made into a finished PCB circuit.

### V3 (final)
I experimented with:
- powering the esp and the beam sensor seperately, which worked well.
- pulling the resistor high in esphome
- setting inverted to true

After a lot of "experimentation", and mis-directions about sensors not closing, I [reached out to the Home Assistant community](https://community.home-assistant.io/t/esphome-ir-beam-sensor-code-help/507588)
and got some simple and excellent advice from [Aruffell](https://community.home-assistant.io/u/aruffell/summary) and [Julian Hall](https://community.home-assistant.io/u/juliandh/summary)

I made the following checks
- Beam sensor relay was a DRY relay (no connection on either terminal to the supply +ve / -ve)
- Relay was set to normally closed (NC) 


