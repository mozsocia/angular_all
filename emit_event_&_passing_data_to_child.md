-----------------------------------------
-----------------------------------------
## passing data to child

app.component.ts
```blade 
<h1>THis is some component</h1>
<test [parentData]="namep"></test>
```
```ts
import { Component } from '@angular/core';

@Component({
  selector: 'my-app',
  template: `above block`,
  styles: [``],
})
export class AppComponent {
  public namep = 'Mozdalif';
}


```
<br>

test.component.ts
```blade
<h1>child {{ pdata}} </h1> 
 ```
 ```ts
 import { Component, Input } from '@angular/core';

@Component({
  selector: 'test',
  template: `above block `,
  styles: [``],
})
export class TestComponent {
  @Input('parentData') pdata;
}

 
 ````
 



-------------------------------------------
----------------------------------------

## event emit
#### parent 
app.component.ts
```blade

<h1> {{message}} </h1>
<test (childEvent)="fireFn($event)" ></test>

```

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'my-app',
  template: `above block`,
  styles: [``],
})
export class AppComponent {
  public message = '';

  fireFn(para) {
    console.log(para);
  }
}

```
#### child


test.component.ts
```blade
<h2> Hello  </h2>
<button (click)=fireEvent()>Send Event</button>
```
```ts
import { Component, OnInit, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'test',
  template: `above block`,
  styles: [``],
})
export class TestComponent {
  @Output() public childEvent = new EventEmitter<string>();

  fireEvent() {
    this.childEvent.emit('Hey Codevolution');
  }
}

```

