-----------------------------------------
-----------------------------------------
## passing data to child

app.component.ts
```ts
import { Component } from '@angular/core';

@Component({
  selector: 'my-app',
  template: `
  <h1>THis is some component</h1>
  <test [parentData]="namep"></test>
  `,
  styles: [``],
})
export class AppComponent {
  public namep = 'Mozdalif';
}


```
test.component.ts
 ```ts
 import { Component, Input } from '@angular/core';

@Component({
  selector: 'test',
  template: `<h1>child {{ pdata}} </h1>
  `,
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
app.component.html
```blade
<div style="text-align:center">
  <h1>
    {{message}}
  </h1>
</div>
<app-test (childEvent)="message=$event" [parentData]="name"></app-test>

```


app.component.ts

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'app';
  public name = "Vishwas";
  public message = "";

}
```
#### child




```ts
import { Component, OnInit, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-test',
  template: `
    <h2>
      {{"Hello " + pdata}}
    </h2>
    <button (click)=fireEvent()>Send Event</button>
  `,
  styles: []
})


export class TestComponent implements OnInit {

  @Input('parentData') public pdata;
  @Output() public childEvent = new EventEmitter<string>();

  constructor() { }

  ngOnInit() {
  }

  fireEvent(){
    this.childEvent.emit('Hey Codevolution');
  }

}
```

