
# Vue

*Note: Be sure that you have the demo API Server running before you start this exercise.*

## Vue (Downgraded Experience)

### Project Creation

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
### Completed Examples

* [Basic](/demos/basic/vue-cli)
* [Complete](/demos/complete/vue-cli)
