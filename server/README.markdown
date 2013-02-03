#Using the Interface.js Server

The Interface.js Server has two purposes: 
  1) it serves interfaces to your browser 
  2) it translates network messages from your browser into OSC or MIDI messages.
  
If you want to use the server, you'll need to have [node.js][nodejs] installed. Node.js will provide most of the functionality we need to serve web pages, but we'll also need to add a few utility libraries to send OSC and MIDI and carry out a few other specialized tasks. We can install these utilities using the Node Package Manager, or NPM. First [download and install NPM][npm]. Then run the following commands in a terminal:

```
npm install midi
npm install omgosc
npm install connect
npm install ws
```

Once these libraries are installed, cd into the server folder and then execute the following command:

```node interface.server.js```

This will start the web server running on port 8080.

All interface files should be stored in the server > interfaces. When you navigate to your computer's url and port 8080 in a browser, you should see a list of all the files in the interfaces directory. Selecting any file in your browser will run the interface and interface.server.js will transmit any messages it receives into either OSC messages on port 8082 or MIDI messages that leave the virtual midi output named "Interface Out".

To define widgets that send OSC messages, simply set their target to be Interface.OSC and their key to be the OSC address you would like them to output to. For example, to send a message to /speed we could create the following slider

```javascript
a = new Interface.Slider({
  bounds:[0,0,1,1],
  target:Interface.OSC, key:'/speed',
});
```

For MIDI, we specify a target of Interface.MIDI instead of Interface.OSC. For the key, we pass an array specifying the type of message we want to send, the channel it should go out on and the number of the message. Possible message types currently include 'noteon', 'noteoff', 'cc' and 'prgoramchange'. For example, to create a button that outputs NoteOn on channel 1, number 64 we would use:

```javascript
a = new Interface.Button({
  bounds:[0,0,1,1],
  target:Interface.MIDI, key:['noteon', 0, 64],
});
```


[nodejs][http://nodejs.org]
[npm][http://nodejs.org/download/]