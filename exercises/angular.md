
# Angular

*Note: Be sure that you have the demo API Server running before you start this exercise.*

## Components

* The Angular CLI, by default, generates four files for each component in your application
  * CSS file... scoped styles for your component
  * HTML file... this is your template
  * A TypeScript spec file... unit tests for your component
  * A TypeScript class file... the class for the component

### The Component Class

```javascript
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit {
  albums: Album[] = [];

  constructor(private http: HttpClient) { }

  ngOnInit(): void {
    this.http.get<Album[]>('http://localhost:3000/albums')
      .subscribe(data => this.albums = data);
  }
}
```

* Components are just plain TypeScript classes that are decorated with a Component decorator
  * No base class is required
  * The decorator is what makes our class a component
* We can any number of properties and methods on our class to be used internally by the component
  * As we'll see in a bit, anything that we want to expose outside of our component needs to be declared as "input" or "output"
* API call is being made when the component is being initialized
  * Notice the use of Angular's HttpClient... which uses RxJS (instead of a Promise) to handle the async HTTP call
* The instance of the HttpClient will be injected into our component via Angular's DI container

### The Component Template

* An Angular template just uses HTML
* You write values using interpolation:
* Any attribute that begins with an asterisk (*) is a structural directive
  * They shape or reshape the structure of the DOM

```html
<div>
  <div *ngFor="let album of albums">
    <h2>{{ album.title }}</h2>
  </div>
</div>
```

* You can bind element attributes to properties

```html
<div class="box">
  <div class="columns">
    <div class="column">
      <figure class="image is-square">
        <img [src]="imageUrl" [alt]="album.title" />
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
```

* You can bind element events to methods

```html
<div>
  <h2>{{ album.title }}</h2>
  <button (click)="viewDetails()">View Details</button>
</div>
```

## Component Input and Output

* Components that accept input or raise events as output need to declare that using "Input" and "Output" decorators
  * Like React props, "Input" properties provide one-way data flow (from parent to child)
  * That being said, Angular allows you to declare a two-way binding (i.e. a banana in a box `[()]`) if you defined an input property `someProp` and an output property `somePropChange` (see [https://angular.io/guide/template-syntax#two-way-binding---](https://angular.io/guide/template-syntax#two-way-binding---))

```javascript
@Component({
  selector: 'app-album',
  templateUrl: './album.component.html',
  styleUrls: ['./album.component.css']
})
export class AlbumComponent {
  @Input() album: Album;
  @Output() onViewDetails = new EventEmitter();

  constructor() { }

  viewDetails() {
    this.onViewDetails.emit();
  }
}
```

And the template would look like:

```html
<div>
  <h2>{{ album.title }}</h2>
  <button (click)="viewDetails()">View Details</button>
</div>
```

And the parent component class would look like:

```javascript
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit {
  albums: Album[] = [];

  constructor(private http: HttpClient) { }

  handleViewDetails() {
    alert('View details!');
  }

  ngOnInit(): void {
    this.http.get<Album[]>('http://localhost:3000/albums')
      .subscribe(data => this.albums = data);
  }
}
```

And its template would look like:

```html
<div>
  <div *ngFor="let album of albums">
    <app-album [album]="album" (onViewDetails)="handleViewDetails()"></app-album>
  </div>
</div>
```

## Modules and Components

* Angular gives you a container for your components
  * You can think of the module conceptually as an assembly
  * You can share modules across apps
  * You can control the visibility of components within a module

```javascript
@NgModule({
  declarations: [
    AppComponent,
    AlbumComponent
  ],
  imports: [
    BrowserModule,
    HttpClientModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

## Completed Examples

[Basic](/demos/basic/angular-cli)
[Complete](/demos/complete/angular-cli)
