# Drawflow

![Demo](https://github.com/jerosoler/Drawflow/blob/master/docs/drawflow.gif)

Simple flow library.

Drawflow allows you to create data flows easily and quickly.

Installing only a javascript library and with four lines of code.

[LIVE DEMO](https://jerosoler.github.io/Drawflow/)

## Table of contents
- [Features](#features)
- [Installation](#installation)
  - [Running](#running)
- [Mouse and  Keys](#mouse-and-keys)
- [Editor](#editor)
- [Modules](#modules)
- [Nodes](#nodes)
  - [Node example](#node-example)
- [Methods](#methods)
  - [Methods example](#methods-example)
- [Events](#events)
  - [Events example](#events-example)
- [Export / Import](#export-/-import)
  - [Export example](#export-example)
- [Exaple](#example)

## Features
- Drag Nodes
- Multiple Inputs / Outputs
- Multiple connections
- Delete Nodes and Connections
- Data sync on Nodes
- Zoom in / out
- Clear data module
- Support modules
- Editor mode `fixed` and `edit`
- Import / Export data
- Events
- Mobile support
- Vanilla javascript (No dependencies)

## Installation
Download or clone repository and copy the dist folder. Or CDN option.  
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/jerosoler/Drawflow/dist/drawflow.min.css">
<script src="https://cdn.jsdelivr.net/gh/jerosoler/Drawflow/dist/drawflow.min.js"></script>
```
Create the parent element of **drawflow**.
```html
<div id="drawflow"></div>
```
### Running
Start drawflow.
```javascript
var id = document.getElementById("drawflow");
const editor = new Drawflow(id);
editor.start();
```
## Mouse and  Keys
- `del key` to remove element.
- `Right click` to show remove options (Mobile long press).
- `Left click press` to move editor or node selected.

## Editor
You can change the editor to **fixed** type to block. Only editor can be moved. You can put it before start.
```javascript
editor.editor_mode = 'edit'; // Default
editor.editor_mode = 'fixed'; // Only scroll
```
You can also adjust the zoom values.
```javascript
editor.zoom_max = 1.6;
editor.zoom_min = 0.5;
```

## Modules
Separate your flows in different editors.
```javascript
editor.addModule('nameNewModule');
editor.changeModule('nameNewModule');
// Default Module is Home
editor.changeModule('Home');
```

## Nodes
Adding a node is simple.
```javascript
editor.addNode(name, inputs, outputs, posx, posy, class, data, html);
```
Parameter | Type | Description
--- | --- | ---
`name` | text | Name of module
`inputs` | number | Number of de inputs
`outputs` | number | Number of de outputs
`pos_x` | number | Position on start node left
`pos_y` | number | Position on start node top
`class` | text | Added classname to de node
`data` | json | Data passed to node
`html` | text | HTML drawn on node

You can use the attribute `df-*` in **inputs, textarea or select** to synchronize with the node data.

Atrributs multiples parents support `df-*-*...`

### Node example
```javascript
var html = `
<div><input type="text" df-name></div>
`;
var data = { "name": '' };

editor.addNode('github', 0, 1, 150, 300, 'github', data, html);
```
## Methods
Other available functions.

Mehtod | Description
--- | ---
`zoom_in()` | Increment zoom +0.1
`zoom_out()` | Decrement zoom -0.1
`removeNodeId(id)` | Remove node. Ex id: `node-x`
`removeConnectionNodeId(id)` | Remove node connections. Ex id: `node-x`
`clearModuleSelected()` | Clear data of module selected
`clear()` | Clear all data of all modules and modules remove.

### Methods example

```javascript
editor.removeNodeId('node-4');
```

## Events
You can detect events that are happening.

List of available events:

Event | Return | Description
--- | --- | ---
  `nodeCreated` | id | `id` of Node
  `nodeRemoved` | id | `id` of Node
  `nodeSelected` | id | `id` of Node
  `connectionCreated` | { ouput_id, input_id, ouput_class, input_class } | `id`'s of nodes and ouput/input selected
  `connectionRemoved` | { ouput_id, input_id, ouput_class, input_class } | `id`'s of nodes and ouput/input selected
  `moduleCreated` | name | `name` of Module
  `moduleChanged` | name | `name` of Module
  `mouseMove` | { x, y } | Position
  `zoom` | zoom_level | Level of zoom
  `translate` | { x, y } | Position translate editor

### Events example
```javascript
editor.on('nodeCreated', function(id) {
  console.log("Node created " + id);
})
```

## Export / Import
You can export and import your data.
```javascript
var exportdata = editor.export();
editor.import(exportdata);
```
### Export example
Example of exported data:
```json
{
    "drawflow": {
        "Home": {
            "data": {}
        },
        "Other": {
            "data": {
                "16": {
                    "id": 16,
                    "name": "facebook",
                    "data": {},
                    "class": "facebook",
                    "html": "\n        
\n          
 Facebook Message
\n        
\n        ",
                    "inputs": {},
                    "outputs": {
                        "output_1": {
                            "connections": [
                                {
                                    "node": "17",
                                    "output": "input_1"
                                }
                            ]
                        }
                    },
                    "pos_x": 226,
                    "pos_y": 138
                },
                "17": {
                    "id": 17,
                    "name": "log",
                    "data": {},
                    "class": "log",
                    "html": "\n            
\n              
 Save log file
\n            
\n            ",
                    "inputs": {
                        "input_1": {
                            "connections": [
                                {
                                    "node": "16",
                                    "input": "output_1"
                                }
                            ]
                        }
                    },
                    "outputs": {},
                    "pos_x": 690,
                    "pos_y": 129
                }
            }
        }
    }
}

```

## Example
View the complete example in folder [example](https://github.com/jerosoler/Drawflow/tree/master/example).