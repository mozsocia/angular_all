```ts

import { HttpClient } from '@angular/common/http';
import { Component, Input, OnInit } from '@angular/core';

@Component({
  selector: 'new',
  template: `
  <ul class="list-group">
  <li 
      *ngFor="let post of data">
      {{ post.name }}
  </li>
</ul>
  `,
  styles: [`h1 { font-family: Lato; }`],
})
export class NewComponent implements OnInit {
  public data = [];
  public errorMsg;

  constructor(private http: HttpClient) {}

  ngOnInit() {
    this.http
      .get('https://run.mocky.io/v3/26c5c454-89d8-4ba6-9d86-d1ab397be9d2')
      .subscribe({
        next: (res: []) => {
          console.log(res);
          this.data = res;
        },
        error: (err) => {
          console.log('error', err);
          this.errorMsg = err.message;
          console.log(this.errorMsg);
        },
      });
  }
}
```