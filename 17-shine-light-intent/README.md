# Day 17 - Shine Light Intent 

Today we’ll train TJBot how to understand natural language and shine the light a color using the converse node and the Watson Conversation service.

[![Train TJBot to Shine Light Intent in Node-RED](http://img.youtube.com/vi/yG-4wXAdc0A/0.jpg)](https://www.youtube.com/watch?v=yG-4wXAdc0A&list=PLddOPkVMz1dtN3I_4JKava4GBLLXuUevV&index=20 "Train TJBot to Shine Light Intent in Node-RED") 

## Flow

The flow consists of an inject node to run the flow, a see node to recognize objects and colors using the Watson Visual Recognition service, a function node to format the list of colors from the results, and a debug node to output the result to the debug window.

![Shine Light Intent Flow](assets/flow.png) 

## Flow JSON

```
[{"id":"951321ce.a08938","type":"inject","z":"4f8a700b.20a01","name":"","topic":"","payload":"turn light red","payloadType":"str","repeat":"","crontab":"","once":false,"x":150,"y":140,"wires":[["70223a88.057714"]]},{"id":"70223a88.057714","type":"tjbot-converse","z":"4f8a700b.20a01","botId":"1d72afad.6feb48","name":"","x":320,"y":140,"wires":[["6206c4ab.7cb38c"]]},{"id":"6206c4ab.7cb38c","type":"switch","z":"4f8a700b.20a01","name":"Has An Intent?","property":"response.object.intents.length","propertyType":"msg","rules":[{"t":"gt","v":"0","vt":"num"},{"t":"else"}],"checkall":"false","outputs":2,"x":480,"y":140,"wires":[["9028e3cf.935918"],["e25f5904.40682"]]},{"id":"9028e3cf.935918","type":"switch","z":"4f8a700b.20a01","name":"Has Shine Intent?","property":"response.object.intents[0].intent","propertyType":"msg","rules":[{"t":"eq","v":"shine_light","vt":"str"},{"t":"else"}],"checkall":"false","outputs":2,"x":670,"y":120,"wires":[["1d2e0e22.25bfd2"],["e25f5904.40682"]]},{"id":"1d2e0e22.25bfd2","type":"switch","z":"4f8a700b.20a01","name":"Has An Entity?","property":"response.object.entities.length","propertyType":"msg","rules":[{"t":"gt","v":"0","vt":"num"},{"t":"else"}],"checkall":"false","outputs":2,"x":860,"y":100,"wires":[["b83023bc.cd2ca"],["e25f5904.40682"]]},{"id":"b83023bc.cd2ca","type":"switch","z":"4f8a700b.20a01","name":"Has Color Entity?","property":"response.object.entities[0].entity","propertyType":"msg","rules":[{"t":"eq","v":"color","vt":"str"},{"t":"else"}],"checkall":"false","outputs":2,"x":1050,"y":80,"wires":[["c5e2d687.5fe9c"],["e25f5904.40682"]]},{"id":"c5e2d687.5fe9c","type":"change","z":"4f8a700b.20a01","name":"Set Color","rules":[{"t":"set","p":"color","pt":"msg","to":"response.object.entities[0].value","tot":"msg"}],"action":"","property":"","from":"","to":"","reg":false,"x":1220,"y":60,"wires":[["6831f238.b7f904","e25f5904.40682"]]},{"id":"6831f238.b7f904","type":"tjbot-shine","z":"4f8a700b.20a01","botId":"1d72afad.6feb48","mode":"shine","color":"msg.color","duration":"","name":"","x":1410,"y":60,"wires":[]},{"id":"e25f5904.40682","type":"debug","z":"4f8a700b.20a01","name":"","active":true,"console":"false","complete":"response.object.output.text[0]","x":1380,"y":160,"wires":[]},{"id":"b6c0a256.fff378","type":"inject","z":"4f8a700b.20a01","name":"","topic":"","payload":"turn light aqua","payloadType":"str","repeat":"","crontab":"","once":false,"x":150,"y":180,"wires":[["70223a88.057714"]]},{"id":"1d72afad.6feb48","type":"tjbot-config","z":"","botGender":"male","name":"TJBot","hasServo":false,"hasLED":true,"hasSpeaker":false,"hasMicrophone":false,"hasCamera":false,"speakerDeviceId":"plughw:0,0"}]

```

## Conversation Workspace JSON

```
{"name":"TJBot","created":"2017-08-17T06:30:02.252Z","intents":[{"intent":"shine_light","created":"2017-08-17T06:30:17.586Z","updated":"2017-08-17T06:30:55.391Z","examples":[{"text":"turn light red","created":"2017-08-17T06:30:31.958Z","updated":"2017-08-17T06:30:31.958Z"},{"text":"change light blue","created":"2017-08-17T06:30:36.003Z","updated":"2017-08-17T06:30:36.003Z"},{"text":"change color to red","created":"2017-08-17T06:30:39.874Z","updated":"2017-08-17T06:30:39.874Z"},{"text":"change light color to green","created":"2017-08-17T06:30:46.270Z","updated":"2017-08-17T06:30:46.270Z"},{"text":"shine light yellow","created":"2017-08-17T06:30:55.391Z","updated":"2017-08-17T06:30:55.391Z"}],"description":null}],"updated":"2017-08-17T06:33:57.422Z","entities":[{"entity":"color","values":[{"value":"red","created":"2017-08-17T06:31:59.483Z","updated":"2017-08-17T06:31:59.483Z","metadata":null,"synonyms":[]},{"value":"yellow","created":"2017-08-17T06:32:01.778Z","updated":"2017-08-17T06:32:01.778Z","metadata":null,"synonyms":[]},{"value":"blue","created":"2017-08-17T06:32:03.341Z","updated":"2017-08-17T06:32:03.341Z","metadata":null,"synonyms":[]},{"value":"green","created":"2017-08-17T06:32:05.014Z","updated":"2017-08-17T06:32:05.014Z","metadata":null,"synonyms":[]},{"value":"pink","created":"2017-08-17T06:32:06.999Z","updated":"2017-08-17T06:32:06.999Z","metadata":null,"synonyms":[]},{"value":"purple","created":"2017-08-17T06:32:08.739Z","updated":"2017-08-17T06:32:08.739Z","metadata":null,"synonyms":[]},{"value":"magenta","created":"2017-08-17T06:32:11.437Z","updated":"2017-08-17T06:32:11.437Z","metadata":null,"synonyms":[]}],"created":"2017-08-17T06:31:18.141Z","updated":"2017-08-17T06:32:11.437Z","metadata":null,"description":null}],"language":"en","metadata":{"api_version":{"major_version":"v1","minor_version":"2017-05-26"}},"description":"","dialog_nodes":[{"title":null,"output":{},"parent":null,"context":null,"created":"2017-08-17T06:32:32.202Z","updated":"2017-08-17T06:32:45.466Z","metadata":null,"next_step":null,"conditions":"#shine_light","description":null,"dialog_node":"node_1_1502951551873","previous_sibling":"Welcome"},{"title":null,"output":{"text":{"values":["Hello. How can I help you?"],"selection_policy":"sequential"}},"parent":null,"context":null,"created":"2017-08-17T06:32:25.075Z","updated":"2017-08-17T06:32:25.075Z","metadata":null,"next_step":null,"conditions":"welcome","description":null,"dialog_node":"Welcome","previous_sibling":null},{"title":null,"output":{"text":{"values":["I didn't understand. You can try rephrasing.","Can you reword your statement? I'm not understanding.","I didn't get your meaning."],"selection_policy":"sequential"}},"parent":null,"context":null,"created":"2017-08-17T06:32:25.075Z","updated":"2017-08-17T06:32:25.075Z","metadata":null,"next_step":null,"conditions":"anything_else","description":null,"dialog_node":"Anything else","previous_sibling":"node_1_1502951551873"},{"type":"response_condition","title":null,"output":{"text":{"values":["Hmm. I don't recognize that color. Please try a color like red, yellow, blue, green, pink, purple, or magenta."],"selection_policy":"sequential"}},"parent":"node_1_1502951551873","context":null,"created":"2017-08-17T06:33:23.975Z","updated":"2017-08-17T06:33:57.422Z","metadata":null,"next_step":null,"conditions":" true","description":null,"dialog_node":"node_3_1502951603755","previous_sibling":"node_2_1502951564888"},{"type":"response_condition","title":null,"output":{"text":{"values":["Okay. I've turned the light <? @color ?>"],"selection_policy":"sequential"}},"parent":"node_1_1502951551873","context":null,"created":"2017-08-17T06:32:45.107Z","updated":"2017-08-17T06:33:20.609Z","metadata":null,"next_step":null,"conditions":" @color","description":null,"dialog_node":"node_2_1502951564888","previous_sibling":null}],"workspace_id":"c6627175-06c9-4209-a633-329e12bc22b8","counterexamples":[],"learning_opt_out":false}
```

## Tips

* Don't forget to create a Watson Conversation service and use the service credentials in the TJBot configuration
* Enable the LED in the TJBot configuration

## Extra Credit

* Add additional training phrases 
* Use more specific conditions to make specific colors and respond in different ways
	
## Resources

If this is your first time using [Node-RED](https://nodered.org/), check out the [docs](https://nodered.org/docs/) for the Getting Started guide.