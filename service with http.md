[https://stackblitz.com/edit/angular-ivy-g3z5sq?file=src/app/employee-detail.component.ts](https://stackblitz.com/edit/angular-ivy-g3z5sq?file=src/app/app.module.ts)



app.module.ts
```ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms';

import { AppComponent } from './app.component';
import { EmployeeListComponent } from './employee-list.component';
import { EmployeeService } from './employee.service';
import { HttpClientModule } from '@angular/common/http';

@NgModule({
  imports: [BrowserModule, FormsModule, HttpClientModule],
  declarations: [AppComponent, EmployeeListComponent],
  providers: [EmployeeService],
  bootstrap: [AppComponent],
})
export class AppModule {}

```

employee.service.ts
```ts
import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';

@Injectable()
export class EmployeeService {
  private _url = 'https://my-json-server.typicode.com/mozsocia/json_db/profile';
  constructor(private http: HttpClient) {}

  getEmployees() {
    return this.http.get(this._url);
  }
}
```
app.compnent.ts
```blade
<div style="text-align:center">
  <h1>Welcome to {{ title }}!</h1>
</div>
<employee-list></employee-list>
```
```ts
import { Component } from '@angular/core';

@Component({
  selector: 'my-app',
  templateUrl: './app.component.html',
  styles: [``]
})
export class AppComponent {
  title = 'Codevolution';
}
```



employee-list.component.ts
```blade
  <h2>Employee List</h2>
    <ul *ngFor="let employee of employees">
      <li>{{employee.name}}</li>
   </ul>
```
```ts
import { Component, OnInit } from '@angular/core';
import { EmployeeService } from './employee.service';

@Component({
  selector: 'employee-list',
  template: ``,
  styles: [],
})
export class EmployeeListComponent implements OnInit {
  public employees = [];
  public errorMsg;
  constructor(private _employeeService: EmployeeService) {}

  ngOnInit() {
    this._employeeService.getEmployees().subscribe({
      next: (res: []) => {
        console.log(res);
        this.employees = res;
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
