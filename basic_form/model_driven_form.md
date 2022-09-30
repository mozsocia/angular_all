```ts
@NgModule({
  imports: [BrowserModule, FormsModule,ReactiveFormsModule],
  declarations: [AppComponent],
  bootstrap: [AppComponent],
})
```

```blade
<div class="container">
    <h2>User Data</h2>
    <form [formGroup]="userForm" (ngSubmit)="onSubmit()" >
        <div class="form-group">
            <label>Name:</label>
            <input type="text" #refName class="form-control" formControlName="name">                       
            <div *ngIf="userForm.controls['name'].hasError('required')" class="alert alert-danger">
                Please enter a name.
            </div>
            <div *ngIf="userForm.controls['name'].hasError('minlength')" class="alert alert-danger">
                Name needs to be atleast 3 characters long.
            </div>
            <div *ngIf="userForm.controls['name'].hasError('maxlength')" class="alert alert-danger">
                Name cannot exceed 10 characters.
            </div>
        </div>
        <div class="form-group">
            <label>Email:</label>
            <input type="text" class="form-control" formControlName="email">
        </div>
        <div formGroupName="address">
            <div class="form-group">
                <label>Street:</label>
                <input type="text" class="form-control" formControlName="street">
            </div>
            <div class="form-group">
                <label>City:</label>
                <input type="text" class="form-control" formControlName="city">
            </div>
            <div class="form-group">
                <label>Postal Code:</label>
                <input type="text" class="form-control" formControlName="postalcode">
                <div *ngIf="userForm.controls['address'].controls['postalcode'].hasError('pattern')" class="alert alert-danger">
                    Invalid format.
                </div>
            </div>
        </div>    
        <button type="submit" [disabled]="!userForm.valid" class="btn btn-primary">Submit</button>    
    </form>
</div>

```

```ts
import { Component } from '@angular/core';
import { FormGroup, FormControl, Validators } from '@angular/forms';

@Component({
  selector: 'my-app',
  templateUrl : 'app.component.html'
})
export class AppComponent { 
  userForm = new FormGroup({
    name: new FormControl('Vishwas', [Validators.required, Validators.minLength(4), Validators.maxLength(10)]),
    email: new FormControl(),
    address: new FormGroup({
      street: new FormControl(),
      city: new FormControl(),
      postalcode: new FormControl(null, Validators.pattern('^[1-9][0-9]{4}$'))
    })
  });
  onSubmit(){
    console.log(this.userForm.value);
  }
}

```