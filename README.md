# React DnD Multi Backend [![NPM Version][npm-image]][npm-url]

[Try it here!](https://louisbrunner.github.io/react-dnd-multi-backend/examples)

This project is a Drag'n'Drop backend compatible with [React DnD](https://github.com/gaearon/react-dnd).
It enables your application to use different backends depending on the situation.
You can either generate your own backend pipeline or use the default one (`HTML5toTouch`).

[HTML5toTouch](src/lib/HTML5toTouch.js) starts by using the [React DnD HTML5 Backend](https://github.com/gaearon/react-dnd-html5-backend), but switches to the [React DnD Touch Backend](https://github.com/yahoo/react-dnd-touch-backend) if a touch event is triggered.
You application can smoothly use the nice HTML5 compatible backend and fallback on the Touch one on mobile devices!

Moreover, because some backends don't support preview, a `Preview` component has been added to make it easier to mock the Drag'n'Drop "ghost".

This is the next version of this package, see [Migrating from 2.x.x](#migrating-from-2.x.x) for instructions if you are coming from `react-dnd-multi-backend@2.x.x`.


## Installation

### Node Installation

```sh
npm install react-dnd-multi-backend@next
```

You can then `MultiBackend = require('react-dnd-multi-backend')` or `import MultiBackend from 'react-dnd-multi-backend'`.
To get the `HTML5toTouch` pipeline, just require/import `react-dnd-multi-backend/lib/HTML5toTouch`.

### Browser Installation

Use the minified UMD build in the `dist` folder: [here](dist/ReactDnDMultiBackend.min.js).
It exports a global `window.ReactDnDMultiBackend` when imported as a `<script>` tag.

If you want to use the `HTML5toTouch` pipeline, also include [RDMBHTML5toTouch.min.js](dist/RDMBHTML5toTouch.min.js).
It exports a global `window.RDMBHTML5toTouch` when imported as a `<script>` tag.
This file also includes the `HTML5` and `Touch` backends, so no need to include them as well.


## Usage

Every code snippet will be presented in 3 different styles: Node.js `require`, Node.js `import` and Browser Javascript (with required HTML `<script>`s).

### Backend

You can plug this backend in the `DragDropContext` the same way you do for any backend (e.g. `ReactDnDHTML5Backend`), you can see [the docs](http://gaearon.github.io/react-dnd/docs-html5-backend.html) for more information.

You must pass a 'pipeline' to use as argument. This package includes `HTML5toTouch`, but you can write your own.

 - *require*:
```js
  var ReactDnD = require('react-dnd');
  var MultiBackend = require('react-dnd-multi-backend');
  var HTML5toTouch = require('react-dnd-multi-backend/lib/HTML5toTouch'); // or any other pipeline
  ...
  module.exports = ReactDnD.DragDropContext(MultiBackend(HTML5toTouch))(App);
```

 - *import*:
```js
  import { DragDropContext } from 'react-dnd';
  import MultiBackend from 'react-dnd-multi-backend';
  import HTML5toTouch from 'react-dnd-multi-backend/lib/HTML5toTouch'; // or any other pipeline
  ...
  export default DragDropContext(MultiBackend(HTML5toTouch))(App);
```

 - *browser*:
```js
  <script src="ReactDnDMultiBackend.min.js"></script>
  <script src="RDMBHTML5toTouch.min.js"></script> <!-- or any other pipeline -->
  ...
  var AppDnD = ReactDnD.DragDropContext(ReactDnDMultiBackend.default(RDMBHTML5toTouch.default))(App); // `.default` is only used to get the ES6 module default export
```

### Create a custom pipeline

TODO


### Preview

Concerning the `Preview` class, it is created using the following snippet:

 - *require*:
```js
  var MultiBackend = require('react-dnd-multi-backend');
  ...
  <MultiBackend.Preview generator={this.generatePreview} />
```

 - *import*:
```js
  import MultiBackend, { Preview } from 'react-dnd-multi-backend';
  ...
  <Preview generator={this.generatePreview} />
```

 - *browser*:
```js
  <script src="ReactDnDMultiBackend.min.js"></script>
  ...
  <ReactDnDMultiBackend.Preview generator={this.generatePreview} />
```

You must pass a function as the `generator` prop which takes 3 arguments:

 - `type`: the type of the item (`monitor.getItemType()`)
 - `item`: the item (`monitor.getItem()`)
 - `style`: an object representing the style (used for positioning), it should be passed to the `style` property of your preview component

Note that this component will only be showed while using a backend flagged with `preview: true` (see [Create a custom pipeline](#create-a-custom-pipeline)) which is the case for the Touch backend in the default `HTML5toTouch` pipeline.


### Example

You can see an example [here](src/examples/) (Node.js style with `import`s).


## Migration from 2.x.x

TODO


## Tasks

 - Update documentation for new version (+ migration instructions)
 - Write some tests (+ coverage)
 - Use CI?
 - TouchBackend doesn't handle mouse events anymore


## Thanks

Thanks to the [React DnD HTML5 Backend](https://github.com/gaearon/react-dnd-html5-backend) maintainers which obviously greatly inspired this project.


## License

MIT, Copyright (c) 2016-2017 Louis Brunner



[npm-image]: https://img.shields.io/npm/v/react-dnd-multi-backend.svg
[npm-url]: https://npmjs.org/package/react-dnd-multi-backend
