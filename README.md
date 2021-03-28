# Vue Lazytube
Embed a YouTube player easily and lazy load the video to save resources and reduces initial load size.
Useful when performance and page size is important or for sites with many embedded youtube videos.

For a simple example page with 10 videos, vue-lazytube will reduce loadtime by 7x and memory usage by 2-3x.

#### Buy Me a Coffee
[![Support me on Patreon](https://img.shields.io/endpoint.svg?url=https%3A%2F%2Fshieldsio-patreon.vercel.app%2Fapi%3Fusername%3Dseeratawan%26type%3Dpledges&style=for-the-badge)](https://patreon.com/seeratawan)

## Features
- reduces initial load size by ~1.1 MB per video
- fully responsive and customizable through `props`
- provides methods to control (`play`, `stop`, `pause` and `reset`) embedded videos
- provide options to set up custom title and preview of embedded videos

## Demo

[![view vue-lazytube](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/vue-lazytube-forked-17o8v?file=/src/App.vue)

### Installation

With a build systems

```sh
$ npm install --save vue-lazytube
```
```sh
$ yarn add vue-lazytube
```

### To make the plugin available globally
In your `main.js`:

```javascript
import LazyYoutube from "vue-lazytube";

Vue.component("LazyYoutube", LazyYoutube);
```

**OR**

To include only in specific components
```javascript
import LazyYoutube from 'vue-lazytube'

export default {
    name: 'YourComponent',
    components: {
        LazyYoutube,
    },
}
```
**OR**

Directly in browser

```html
<script src="https://cdn.jsdelivr.net/npm/vue"></script>

<script src="./vue-lazytube.umd.min.js"></script>

<script>
    // as a component
    Vue.use('LazyYoutube', LazyYoutube)
</script>
```

### Usage

```javascript
<template>
    <LazyYoutube src="https://www.youtube.com/watch?v=TcMBFSGVi1c" />
</template>
```

### API

#### Props
| Name | Type | Default Value | Description | Required |
| ------ | ------ | ------ | ------ | ------ |
| `src` | `String` | `` | To load video and iframe, should be youtube video link. | `true` |
| `aspectRatio` | `String` | `16:9` | Maintaining the aspect ratio of video, perfect for responsively handling video embeds based on the width of the parent, should be in `*:*` format. e.g, `1:1`, `4:3`, `16:9` and `21:9`. | `false` |
| `maxWidth` | `String` | `560px` | Defines maximum width of video container.  | `false` |
| `showTitle` | `Boolean` | `true` | Defines whether to show video title on top. | `false` |
| `autoplay` | `Boolean` | `false` | Defines whether to load the iframe as the page loads _(not recommended)_ | `false` |
| `thumbnailQuality` | `String` | `standard` | Defines the quality of thumbnail, should be one of the following `default`, `medium`, `high`, `standard` or `maxres` | `false` |
| `iframeClass` | `String` | `ly-iframe` | Defines the class on iframe element | `false` |
| `customTitle` | `String` | `` | Defines the custom title of the video | `false` |
| `customThumbnail` | `String` | `` | Defines the custom thumbnail image link of the video | `false` |

#### Methods
These methods let you control the player using JavaScript, so you can perform the operations like `play`, `stop`, `pause` and `reset`.

>The user's browser must support the HTML5 postMessage feature. Most modern browsers support postMessage.

| Name | Type | Usage |
| ------ | ------ | ------ | 
| playVideo | `function` | `this.$refs["lazyVideo"]['playVideo']()` |
| stopVideo | `function` | `this.$refs["lazyVideo"]['stopVideo']()` |
| pauseVideo | `function` | `this.$refs["lazyVideo"]['pauseVideo']()` |
| resetView | `function` | `this.$refs["lazyVideo"]['resetView']()` |

_Note: Must Replace `lazyVideo` with your [ref](https://v3.vuejs.org/guide/component-template-refs.html)._
#### Example
```javascript
<template>
    <LazyYoutube
        ref="lazyVideo"
        src="https://www.youtube.com/watch?v=TcMBFSGVi1c"
    />
    
    <button @click="handleClick('playVideo')">Play</button>
    <button @click="handleClick('stopVideo')">Stop</button>
    <button @click="handleClick('pauseVideo')">Pause</button>
    <button @click="handleClick('resetView')">Reset</button>
</template>

<script>
    export default {
      name: "YourComponent",
      components: {},
      methods: {
        handleClick(event) {
          this.$refs["lazyVideo"][event]();
        },
      },
    };
</script>
```

### Open Source License

You may use it under the terms of the [MIT Licenses](https://opensource.org/licenses/MIT)