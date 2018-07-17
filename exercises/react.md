
# React

*Note: Be sure that you have the demo API Server running before you start this exercise.*

## Component Types

* Two types of components
  * Stateless functional components
  * Stateful class components

### Stateless Functional Components

* Stateless functional components are just ordinary functions
* A props object is passed into the function
  * This object gives you access to the properties that are set on the component
* Returns a React element
  * This example makes use of JSX
  * Syntax extension to JavaScript
  * JSX (after it's been transpiled by Babel) produces React "elements"

```javascript
function Album(props) {
  return (
    <div>
      <h2>{props.album.title}</h2>
    </div>
  );
}
```

### Stateful Class Components

The previous stateless functional component could be rewritten as a stateful class component:

```javascript
class Album extends Component {
  render() {
    return (
      <div>
        <h2>{this.props.album.title}</h2>
      </div>
    );
  }
}
```

But that example doesn't have any state... let's look at an example that has state:

```javascript
class App extends Component {
  constructor(props) {
    super(props);

    this.state = {
      albums: []
    };
  }

  componentDidMount() {
    fetch('http://localhost:3000/albums')
      .then(response => response.json())
      .then(data => {
        this.setState({
          albums: data
        });
      });
  }

  render() {
    return (
      <div>
        {this.state.albums.map(album => (
          <Album album={album} key={album.id} />
        ))}
      </div>
    );
  }
}
```

## JSX

```javascript
function AlbumBox(props) {
  const album = props.album;

  return (
    <div className="column is-half">
      <div className="box">
        <div className="columns">
          <div className="column">
            <AlbumCover albumId={album.id} albumTitle={album.title} />
          </div>
          <div className="column">
            <h2 className="title">{album.title}</h2>
            <h3 className="subtitle">{album.artist}</h3>
            <div>
              Category: {album.category}
            </div>
          </div>      
        </div>      
      </div>
    </div>
  );
}
```

* JSX is not HTML!
* Element attributes mirror their JavaScript element properties
* How to create elements
  * HTML elements start with a lowercase letter
  * Components start with an uppercase letter
* How to set element attribute values

## Events

To handle an event, you wire up an event handler function or method to the element or component event you want to handle:

```javascript
function handleClick() {
  alert('Viewing details!');
}

function Album(props) {
  return (
    <div>
      <h2>{props.album.title}</h2>
      <button onClick={handleClick}>View Details</button>
    </div>
  );
}
```

Or if you were using stateful class components:

```javascript
class Album extends Component {
  handleViewDetails = () => {
    alert('Viewing details!');    
  }

  render() {
    return (
      <div>
        <h2>{this.props.album.title}</h2>
        <button onClick={this.handleViewDetails}>View Details</button>
      </div>
    );
  }
}
```

* Notice the use of property initializer syntax for the `handleViewDetails()` method
  * This approach is being used in order to workaround a problem that arises with `this` not being bound to the expected object instance
  * There are other ways to workaround "this" problem, including calling `bind()` on all class methods that will be used as event handlers

Or if you were passing an event handler down into a child component:

```javascript
function Album(props) {
  return (
    <div>
      <h2>{props.album.title}</h2>
      <button onClick={props.viewDetails}>View Details</button>
    </div>
  );
}

class App extends Component {

  ...

  handleViewDetails = () => {
    alert('View details!');
  }

  render() {
    return (
      <div>
        {this.state.albums.map(album => (
          <Album 
            album={album} 
            viewDetails={this.handleViewDetails} 
            key={album.id} />
        ))}
      </div>
    );
  }
}
```

## Props

* Props are readonly!

## State

* State must not be directly mutated
* Use `setState()` to mutate the state object

## Completed Examples

* [Basic](/demos/basic/react-cli)
* [Complete](/demos/complete/react-cli)
