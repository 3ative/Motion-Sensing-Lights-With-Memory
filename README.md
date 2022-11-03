# Motion Sensing Lights With Memory

A simple setup to change the colour, or even run an effect when motion (or any trigger) is detected. Then return the Light to its previous state.

> - ### Watch the step-by-step tutorial here: https://youtu.be/9BZuC-LA_XI

## Function Node Code:
```yaml
// Enter your Light entity and if used the Effect Name
var light = "light.table_lights";
var effect = "none"; 

const cs = global.get('homeassistant').homeAssistant.states[light].state;
const cc = global.get('homeassistant').homeAssistant.states[light].attributes.rgb_color;
const cb = global.get('homeassistant').homeAssistant.states[light].attributes.brightness;

var s = context.get('s'); // These lines retrieve the lables 's', 'c' & 'b' 
var c = context.get('c'); // from memory and apply thier values to the
var b = context.get('b'); // variables s, c & b used to retun the Light state

if (msg.payload === "trigger_off" && s == "off") {
    msg.payload =  {"service": "turn_on", data:{"entity_id": light, "rgb_color": c,"brightness": b, "effect":"none"}};
    msg.payload =  {"service": "turn_off", data:{"entity_id": light}};
    }

if (msg.payload === "trigger_off") {
    msg.payload =  {"service": "turn_on", data:{"entity_id": light, "rgb_color": c,"brightness": b, "effect":"none"}};
    }

if (msg.payload === "trigger_on") {
    context.set('s', cs); // These line save the values of cs, cc & cb
    context.set('c', cc); // and save them in memory with lables:
    context.set('b', cb); // 's', 'c' & 'b' 
    
    // 'Alarm state' will be RED & 100% Brighness - Adjust this line to suit your needs
    msg.payload =  {"service": "turn_on",data:{"entity_id": light, "rgb_color": [255,0,0],"brightness": 255, "effect":effect}};
    }

return msg
```

#### 💖 Found this useful, want to say '*Thanks*' and support my efforts. *CHEERS*🍺
| Buy me a Coffee | PATREON |
|-----------------|---------|
| https://www.buymeacoffee.com/3ative | https://www.patreon.com/3ative |
