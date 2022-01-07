# Motion Sensing Lights With Memory

A Simple setup to change the colour, or even run an effect when motion (or any trigger) is detected. Then return the Light to its previous state.

## Function Node Code:
```yaml
// Enter your Light and if used the Effect Name
var light = "light.table_lights";
var effect = "police"; 

const cs = global.get('homeassistant').homeAssistant.states[light].state;
const cc = global.get('homeassistant').homeAssistant.states[light].attributes.rgb_color;
const cb = global.get('homeassistant').homeAssistant.states[light].attributes.brightness;

var s = context.get('s');
var c = context.get('c');
var b = context.get('b');

if (msg.payload === "trigger_off" && s == "off") {
    msg.payload =  {"service": "turn_on", data:{"entity_id": light, "rgb_color": c,"brightness": b, "effect":"none"}};
    msg.payload =  {"service": "turn_off", data:{"entity_id": light}};
    }

if (msg.payload === "trigger_off") {
    msg.payload =  {"service": "turn_on", data:{"entity_id": light, "rgb_color": c,"brightness": b, "effect":"none"}};
    }

if (msg.payload === "trigger_on") {
    context.set('s', cs);
    context.set('c', cc);
    context.set('b', cb);
    
    // 'Alarm state will be RED & 100% Brighness - Adjust this line to suit your needs'
    msg.payload =  {"service": "turn_on",data:{"entity_id": light, "rgb_color": [255,0,0],"brightness": 255, "effect":effect}};
    }

return msg
```

# Watch the step-by-step build guide here: https://youtu.be/hADsxDkyFeA


🎁 Found this useful or want to say 'thanks' and support my efforts...

[![BMC](https://www.buymeacoffee.com/assets/img/custom_images/white_img.png)](https://www.buymeacoffee.com/3ative) **And leave a me a message to let me know.**  ❤

🍺 CHEERS! 👍
