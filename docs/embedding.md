﻿# Embedding the Mesoscale Viewer

This guide will walk you through the process of embedding the Mesoscale Viewer into your website, enabling interactive molecular visualizations for your audience.

## iFrame

```
 <iframe src="https://molstar.org/me/viewer/?example=petworld-synvesicle&&hide-controls=1" height="600" width="100%" title="Mesoscale Explorer"></iframe>
```
See the code in action below 


<iframe src="https://molstar.org/me/viewer/?example=petworld-synvesicle&&hide-controls=1" height="600" width="100%" title="Mesoscale Explorer"></iframe>


See the [query parameters](query-parameters.md) for more options.

## Javascript

You can fork the molstar source repository, build and deploy your own mesoscale explorer and customized it using typeScript.
You can also reuse the mesoscale-explorer molstar.js to embed it in your html, see below example. 

### Example

Here's a complete example of an HTML file that embeds the Mesoscale Viewer:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        html, body {
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-start;
            overflow: hidden;
        }
        #controls {
            display: flex;
            justify-content: center;
            width: 800px;
            margin-bottom: 10px;
            z-index: 1;
        }
        button {
            margin: 5px;
            padding: 10px 20px;
            font-size: 14px;
            cursor: pointer;
        }
        #viewer-container {
            width: 100%;
            height: 600px;
            border: 1px solid #ccc;
            position: relative;
        }
    </style>
    <link rel="stylesheet" type="text/css" href="./molstar.css" />
</head>
<body>
    <div id="controls">
        <button onclick="loadExample('cellpack-hiv1')">Load HIV-1 Example</button>
        <button onclick="loadExample('machineryoflife-tour')">Load Machinery of Life Tour</button>
        <button onclick="loadExample('petworld-synvesicle')">Load Synaptic Vesicle Example</button>
    </div>
    <div id="viewer-container">
        <div id="meso-viewer" style="position: relative; width: 100%; height: 400px;"></div>
    </div>

    <script src="./molstar.js"></script>
    <script type="text/javascript">
        let mesoExplorer;

        function loadExample(example) {
            if (mesoExplorer) {
                mesoExplorer.loadExample(example);
            }
        }

        molstar.MesoscaleExplorer.create('meso-viewer', {
            layoutShowControls: false,
            viewportShowExpand: false,
	        layoutIsExpanded: false,
            powerPreference: 'high-performance',
            graphicsMode: 'quality'
        }).then(me => {
            mesoExplorer = me;
            me.loadExample('cellpack-hiv1');  // Load the default example on page load

            window.addEventListener('unload', () => {
                me.dispose();
            });
        });
    </script>
</body>
</html>
```

[See it live](https://mesoscope.scripps.edu/explorer/viewer/embeding.html) 