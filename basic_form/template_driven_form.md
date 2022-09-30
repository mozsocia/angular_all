```blade
<div class="container">
  <h2>User Data</h2>
  <form #userForm="ngForm" (ngSubmit)="onSubmit(userForm.value)">
    <div class="form-group">
      <label>Name</label>
      <input
        type="text"
        #varName="ngModel"
        class="form-control"
        name="Name"
        ngModel
        required
        minlength="4"
        maxlength="10"
      />
      <b>{{ varName.valid }}</b>
      <div
        *ngIf="varName.errors && (varName.dirty || varName.touched)"
        class="alert alert-danger"
      >
        <div [hidden]="!varName.errors.required">Name is required</div>
        <div [hidden]="!varName.errors.minlength">
          Name must be at least 4 characters long.
        </div>
        <div [hidden]="!varName.errors.maxlength">
          Name cannot exceed 10 characters.
        </div>
      </div>
    </div>
    <div class="form-group">
      <label>Email</label>
      <input type="text" class="form-control" name="Email" ngModel />
    </div>
    <div ngModelGroup="Address">
      <div class="form-group">
        <label>Street</label>
        <input type="text" class="form-control" name="Street" ngModel />
      </div>
      <div class="form-group">
        <label>City</label>
        <input type="text" class="form-control" name="City" ngModel />
      </div>
      <div class="form-group">
        <label>Postal Code</label>
        <input
          type="text"
          #varpostalCode="ngModel"
          class="form-control"
          name="PostalCode"
          ngModel
          pattern="^[1-9][0-9]{4}$"
        />
        <div
          *ngIf="
            varpostalCode.errors &&
            (varpostalCode.dirty || varpostalCode.touched)
          "
          class="alert alert-danger"
        >
          <div [hidden]="!varpostalCode.errors.pattern">
            Invalid format for PostalCode
          </div>
        </div>
      </div>
    </div>
    <button
      type="submit"
      class="btn btn-primary"
      [disabled]="!userForm.form.valid"
    >
      Submit
    </button>
  </form>
</div>

```
```ts
import { Component, VERSION } from '@angular/core';

@Component({
  selector: 'my-app',
  templateUrl: './app.component.html',
  styles: [
    `
  input.ng-invalid{border-left: 5px solid red;}
  .ng-valid[required]{border-left: 5px solid green;}
`,
  ],
})
export class AppComponent {
  // name = 'Angular ';
  name = 'mozdalif';

  public myName = 'Vishwas';
  onSubmit(value: any) {
    console.log(value);
  }
}

```