# Angular

## component

### Callback function

```javascript
@Component({
  ...
  template: '<child [myCallback]="theBoundCallback"></child>'
})
export class ParentComponent{
  public theBoundCallback: Function;

  public ngOnInit(){
    this.theBoundCallback = this.theCallback.bind(this);
  }

  public theCallback(){
    ...
  }
}

@Component({...})
export class ChildComponent{
  //This will be bound to the ParentComponent.theCallback
  @Input()
  public myCallback: Function; 
  ...
}
```

```javascript
@Component({
  ...
  template: '<child [myCallback]="theCallback.bind(this)"></child>',
  directives: [ChildComponent]
})
export class ParentComponent {

  public theCallback(){
    ...
  }
}

@Component({...})
export class ChildComponent{
  //This will be bound to the ParentComponent.theCallback
  @Input()
  public myCallback: Function; 
  ...
}
```

## Transclusion

### single slot transclusion

<ng-content></ng-content>

#### USING ATTRIBUTE

```html
<-- add the select attribute to ng-content -->
<ng-content select="[card-body]"></ng-content>

<-- app.component.html -->
<div class="card-block" card-body>
    <h4 class="card-title">You can put any content here</h4>
    <p class="card-text">For example this line of text and</p>
    <a href="#" class="btn btn-primary">This button</a>
</div>
```

#### USING ATTRIBUTE WITH VALUE

```html
<-- card.component.html -->
<ng-content select="[card-type=body]"></ng-content>
<-- app.component.html -->
<div class="card-block" card-type="body"></div>
```

#### USING CSS CLASS SELECTOR 

```html
<-- card.component.html -->
<ng-content select=".card-body"></ng-content>
<-- app.component.html -->
<div class="card-block card-body">...</div>
```

#### USING MULTIPLE ATTRIBUTES OR CSS CLASSES
 * Atttributes: [card][body]
 * Classes: .card.body

```html
<ng-content select="[card][body]"></ng-content>

<div class="card-block" body card></div>
```

#### USING AN HTML TAG
 * However, you will hit an error if you use the <card-body> tag now. Unhandled Promise rejection: Template parse errors: 'card-body' is not a known element
 * Angular 2 does not recognize the card-body tag. card-body is neither a directive nor a component. A quick way to get around this error is to add schema metadata property in your module, set value to NO_ERRORS_SCHEMA in your module file.
 * In our case, we do it in our app module.
 * import { NgModule, NO_ERRORS_SCHEMA }      from '@angular/core';
 * schemas:      [ NO_ERRORS_SCHEMA ] 

```html
<ng-content select="card-body"></ng-content>

<card-body class="card-block"></card-body>
```

### Multi-Slot Transclusion

```html
<!-- card.component.html -->
<div class="card">
    <div class="card-header">
    <!-- header slot here -->
        <ng-content select="card-header"></ng-content>
    </div>
    <!-- body slot here -->
    <ng-content select="card-body"></ng-content>
    <div class="card-footer">
    <!-- footer -->
        <ng-content select="card-footer"></ng-content>
    </div>
</div>

<!-- app.component.html -->
<h1>Multi slot transclusion</h1>
<card>
    <!-- header -->
    <card-header>
        New <strong>header</strong>
    </card-header>

    <!-- body -->
    <card-body>
        <div class="card-block">
            <h4 class="card-title">You can put any content here</h4>
            <p class="card-text">For example this line of text and</p>
            <a href="#" class="btn btn-primary">This button</a>
          </div>
    </card-body>

    <!-- footer -->
    <card-footer>
        New <strong>footer</strong>
    </card-footer>
<card>
```
