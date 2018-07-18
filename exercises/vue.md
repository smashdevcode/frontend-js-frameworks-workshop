
# Vue

*Note: Be sure that you have the demo API Server running before you start this exercise.*

## Vue (Downgraded Experience)

### Getting Started

* Include Vue via a CDN and a `<script>` tag
* No build process

#### Project Creation

Just create an HTML file!

```
<html>

<head></head>

<body>
  <div id="app">
    <h2 v-text="appName" v-once></h2>
  </div>

  <script src="https://unpkg.com/vue@2.5.13/dist/vue.js"></script>
  <script>
    var app = new Vue({
      el: '#app',
      data: {
        appName: 'Our Awesome App!'
      }
    });
  </script>
</body>

</html>
```

* The Vue instance
* The mounting point in the HTML becomes your template

### Dev Workflow

* Make changes to your code
* Run a local server... I like `http-server`
* Refresh the page in the browser

### The Vue Instance

* Every Vue application has a top level Vue instance
* Created by instantiating an instance of Vue
* `el` is the selector for the mounting point
* `data` is an object literal that defines the state for our app
  * Properties in the data object are reactive (as their values change Vue will update the DOM)
* `created()` is one of the lifecycle events we can hook into

```javascript
var app = new Vue({
  el: '#app',
  data: {
    albums: []
  },
  created() {
    fetch('http://localhost:3000/albums')
      .then(response => response.json())
      .then(data => this.albums = data);
  }
});
```

### The Vue Instance Template

* The DOM element that we bind our instance to provides our template
* Vue provides built-in directives that we can use in our templates
  * `v-for` is used to create a list

```html
<div id="app">
  <div v-for="album in albums">
    <h2>{{ album.title }}</h2>
  </div>
</div>
```

* The `v-bind` directive allows you to bind to element attributes
* You can also use interpolation to write values to the DOM

```html
<div class="column is-half">
  <div class="box">
    <div class="columns">
      <div class="column">
        <figure class="image is-square">
          <img v-bind:src="imageUrl" v-bind:alt="album.title" />
        </figure>
      </div>
      <div class="column">
        <h2 class="title">{{ album.title }}</h2>
        <h3 class="subtitle">{{ album.artist }}</h3>
        <div>
          Category: {{ album.category }}
        </div>
      </div>      
    </div>      
  </div>
</div>
```

* The `v-on` directive allows you to bind to events

```html
<div>
  <h2>{{ album.title }}</h2>
  <button v-on:click="viewDetails">View Details</button>
</div>
```

### Defining Components

To define a global component (available to all Vue instances), you call the Vue `component()` method

```
Vue.component('album', {
  props: ['album'],
  methods: {
    viewDetails() {
      this.$emit('view-details', this.album.id);
    }
  },
  template: `
    <div>
      <h2>{{ album.title }}</h2>
      <button v-on:click="viewDetails">View Details</button>
    </div>
  `
});
```

* Notice that just like with our top level Vue instance, we pass an object literal
  * Basically the same object shape
* `props` defines the properties that our component exposes
* `template` defines the HTML template for our component
* We use the special `$emit()` method to raise an event that can be handled by the parent component

### Completed Examples

* [Basic](/demos/basic/vue-downgraded)
* [Complete](/demos/complete/vue-downgraded)
* [Complete (with Components)](/demos/complete/vue-downgraded-components)

## Vue (Upgraded Experience)

Introduces single file components!

### Getting Started

* Vue CLI
* Install it globally to give you access to the `vue` command

```
npm install -g @vue/cli
```

[https://github.com/vuejs/vue-cli/blob/dev/docs/README.md](https://github.com/vuejs/vue-cli/blob/dev/docs/README.md)

#### Project Creation

```
vue create my-app
cd my-app
npm run serve
```

### Single File Components

* Syntax highlighting
* CommonJS modules
* Component-scoped CSS
  * CSS is extracted from each component and combined into a single resource
* Precompiled templates

```
<template>
  <div class="column is-half">
    <div class="box">
      <div class="columns">
        <div class="column">
          <figure class="image is-square">
            <img v-bind:src="imageUrl" v-bind:alt="album.title" />
          </figure>
        </div>
        <div class="column">
          <h2 class="title">{{ album.title }}</h2>
          <h3 class="subtitle">{{ album.artist }}</h3>
          <div>
            Category: {{ album.category }}
          </div>
        </div>      
      </div>      
    </div>
  </div>
</template>

<script>
export default {
  name: 'AlbumBox',
  props: {
    album: {
      type: Object,
      required: true
    },
  },
  computed: {
    imageUrl() {
      return require(`../assets/${this.album.id}.png`);
    }
  },
}
</script>

<style scoped>
</style>
```

## Debugging

* Using Chrome's DevTools
  * Just set a breakpoint within any .js file in the "Sources" tab
* Chrome and Firefox browser extensions
  * [vue-devtools](https://github.com/vuejs/vue-devtools)
* [Debugging in Visual Studio Code](https://vuejs.org/v2/cookbook/debugging-in-vscode.html)

## Production Builds

```
npm run build
```

Vue generates files into a `dist` folder

### Completed Examples

The "Basic" version is the version that we built in this exercise. The "Complete" version implements a basic search feature and includes styles and images.

* [Basic](/demos/basic/vue-cli)
* [Complete](/demos/complete/vue-cli)
