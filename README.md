# react-infinite-tree [![build status](https://travis-ci.org/cheton/react-infinite-tree.svg?branch=master)](https://travis-ci.org/cheton/react-infinite-tree) [![Coverage Status](https://coveralls.io/repos/cheton/react-infinite-tree/badge.svg)](https://coveralls.io/r/cheton/react-infinite-tree)
[![NPM](https://nodei.co/npm/react-infinite-tree.png?downloads=true&stars=true)](https://nodei.co/npm/react-infinite-tree/)

The [infinite-tree](https://github.com/cheton/infinite-tree) library for React.

Demo: http://cheton.github.io/react-infinite-tree

[![react-infinite-tree](https://raw.githubusercontent.com/cheton/react-infinite-tree/master/media/react-infinite-tree.gif)](http://cheton.github.io/react-infinite-tree)

## Features
* High performance infinite scroll with large data set
* [Customizable renderer](https://github.com/cheton/infinite-tree/wiki/Options#rowrenderer) to render the tree in any form
* [Load nodes on demand](https://github.com/cheton/infinite-tree/wiki/Options#loadnodes)
* Native HTML5 drag and drop API
* A rich set of [APIs](https://github.com/cheton/infinite-tree#api-documentation)

## Browser Support
![Chrome](https://raw.github.com/alrra/browser-logos/master/chrome/chrome_48x48.png)<br>Chrome | ![Edge](https://raw.github.com/alrra/browser-logos/master/edge/edge_48x48.png)<br>Edge | ![Firefox](https://raw.github.com/alrra/browser-logos/master/firefox/firefox_48x48.png)<br>Firefox | ![IE](https://raw.github.com/alrra/browser-logos/master/internet-explorer/internet-explorer_48x48.png)<br>IE |
![Opera](https://raw.github.com/alrra/browser-logos/master/opera/opera_48x48.png)<br>Opera | ![Safari](https://raw.github.com/alrra/browser-logos/master/safari/safari_48x48.png)<br>Safari
--- | --- | --- | --- | --- | --- |
 Yes | Yes | Yes| 9+ | Yes | Yes | 

## Notice
<i>The project is under heavy development and a lot of things are changing. Stay tuned for further updates.</i>

## Installation
```bash
npm install --save react react-dom infinite-tree
npm install --save react-infinite-tree
```

## Usage
```jsx
import React from 'react';
import InfiniteTree from 'react-infinite-tree';
import 'react-infinite-tree/dist/react-infinite-tree.css';

class App extends React.Component {
    tree = null;

    componentDidMount() {
        const data = generateData();
        this.tree.loadData(data);

        // Select the first node
        this.tree.selectNode(this.tree.getChildNodes()[0]);
    }
    render() {
        return (
            <div>
                <InfiniteTree
                    ref={(c) => this.tree = c.tree}
                    autoOpen={true}
                    droppable={true}
                    loadNodes={(parentNode, done) => {
                        const suffix = parentNode.id.replace(/(\w)+/, '');
                        const nodes = [
                            {
                                id: 'node1' + suffix,
                                label: 'Node 1'
                            },
                            {
                                id: 'node2' + suffix,
                                label: 'Node 2'
                            }
                        ];
                        setTimeout(() => {
                            done(null, nodes);
                        }, 1000);
                    }}
                    selectable={true} // Defaults to true
                    shouldSelectNode={(node) => { // Defaults to null
                        if (!node || (node === this.tree.getSelectedNode())) {
                            return false; // Prevent from deselecting the current node
                        }
                        return true;
                    }}
                    onDropNode={(node, e) => {
                        const source = e.dataTransfer.getData('text');
                        document.querySelector('#dropped-result').innerHTML = 'Dropped to <b>' + quoteattr(node.label) + '</b>';
                    }}
                    onOpenNode={(node) => {
                        console.log('open node:', node);
                    }}
                    onCloseNode={(node) => {
                        console.log('close node:', node);
                    }}
                    onScrollProgress={(progress) => {
                        document.querySelector('#scrolling-progress').style.width = progress + '%';
                    }}
                    onSelect={(node) => {
                        console.log('select node:', node);
                    }}
                    onUpdate={() => {
                        console.log(this.tree.getSelectedNode());
                    }}
                />
            </div>
        );
    }
}
```

## API Documentation

Check out API documentation from [infinite-tree](https://github.com/cheton/infinite-tree/wiki):

* [Options](https://github.com/cheton/react-infinite-tree/wiki/Options)
* [Functions: Tree](https://github.com/cheton/react-infinite-tree/wiki/Functions:-Tree)
* [Functions: Node](https://github.com/cheton/react-infinite-tree/wiki/Functions:-Node)
* [Events](https://github.com/cheton/react-infinite-tree/wiki/Events)

## License

Copyright (c) 2016 Cheton Wu

Licensed under the [MIT License](LICENSE).