<!------------------login.html------------------------>
<!---<div class="jumbotron">
    <div class="container">
    
            <div class="row">
                <div class="col-sm-2"></div>
                <div class="col-sm-8">
                <h1 style="text-align:center;margin-bottom:20px;">LoginForm</h1></div></div>

                <form [formGroup]="loginForm" (ngSubmit)="onSubmit()">
                    <div class="form-group">
                        <div class="row">
                            <div class="col-sm-2">
                                 <label>user name</label><span>*</span>
                            </div>
                            <div class="col-sm-8">
                                <input type="text" formControlName="username" [(ngModel)]="user.username" name="username" class="form-control" [ngClass]="{ 'is-invalid': submitted && f.username.errors }" />
                                <div *ngIf="submitted && f.username.errors" class="invalid-feedback">
                                    <div *ngIf="f.username.errors.required">user name is required</div>
                                    
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="form-group">
                            <div class="row">
                                <div class="col-sm-2">
                                    <label>password</label><span>*</span></div>
                                <div class="col-sm-8">
                                    <input type="password"   [(ngModel)]="user.password" name="password" formControlName="password" class="form-control" [ngClass]="{ 'is-invalid': submitted && f.password.errors }" />
                                    <div *ngIf="submitted && f.password.errors" class="invalid-feedback">
                                        <div *ngIf="f.password.errors.required">Last Name is required</div>
                                    </div>
                                </div>
                            </div>
                    </div>
                    
                    
                    <div class="form-group">
                            <div class="row">
                                <div class="col-sm-2">
                                    <label></label></div>
                                <div class="col-sm-2">
                                <button class="btn btn-info">Save</button>

                                </div>
                            </div>
                           
                    </div>
                   
                </form>
               
        
        
    </div>
</div>-->

<div class="container">
    
       

            <form  >
                    <div class="row">
                            <div class="col-sm-2"></div>
                            <div class="col-sm-8">
                            <h5 style="margin-bottom:20px;">LoginForm</h5></div></div>
 
                    <div class="row">
                        <div class="col-sm-2">
                             <label>user name</label><span>*</span>
                        </div>
                        <div class="col-sm-8">
                            <input type="text" [(ngModel)]="user.username" name="username"  />
                         
                        </div>
                    </div>
            
              
                        <div class="row">
                            <div class="col-sm-2">
                                <label>password</label><span>*</span></div>
                            <div class="col-sm-8">
                                <input type="password"   [(ngModel)]="user.password" name="password" />
                                
                            </div>
                        </div>
              
                
              
                        <div class="row">
                            <div class="col-sm-2">
                                <label></label></div>
                            <div class="col-sm-2">
                            <button class="btn btn-info" (click)="submit()">Save</button>
                            <button class="btn btn-info" (click)="cancel()" style="margin-left:10px;">cancel</button>
                            </div>
                        </div>

            </form>

</div>
<!------------login.ts------------->
import { Component, OnInit } from '@angular/core';
import { User } from '../user.model';
import { UserserviceService } from '../userservice.service';
import { Router } from '@angular/router';
import { Validators, FormBuilder, FormGroup } from '@angular/forms';

@Component({
  selector: 'app-login',
  templateUrl: './login.component.html',
  styleUrls: ['./login.component.css']
})
export class LoginComponent implements OnInit {
  user:User={
  username:null,
 password:null
 
   
   
  }
  
 /* loginForm: FormGroup;
  submitted = false;*/

  constructor(private formBuilder: FormBuilder, private __userService:UserserviceService, private _router:Router) { }

 

 
 /* ngOnInit() {
      this.loginForm = this.formBuilder.group({
         username: ['', Validators.required],
          password: ['', Validators.required],
  
      });
  }

  // convenience getter for easy access to form fields
  get f() { return this.loginForm.controls; }*/

  submit() {

     //stop here if form is invalid
    
      this.__userService.save(this.user);
    this._router.navigate(['storing']);
    
  }

  ngOnInit() {
  }
  
}
<!!--------------strong.html------------>
<div *ngFor="let use of user">
 
    <p>{{use.username}}</p>
    <p>{{use.password}}</p>
</div>

<!----------------storing.ts----------------->
import { Component, OnInit, Input } from '@angular/core';
import { User } from '../user.model';
import { UserserviceService } from '../userservice.service';

@Component({
  selector: 'app-storing',
  templateUrl: './storing.component.html',
  styleUrls: ['./storing.component.css']
})
export class StoringComponent implements OnInit {

 user:User[]=[
  
  ];
  constructor( private _userservice:UserserviceService) { }

  ngOnInit() {
    this.user=this._userservice.getUsers();
  }
}
<!--------------services.ts----------->
import { Injectable } from '@angular/core';
import { User } from './user.model';

@Injectable({
  providedIn: 'root'
})
export class UserserviceService {
  userlist:User[]=[ 
  ];
  getUsers():User[]{
      return this.userlist;

  }
  save(user:User){                                                         
     
      this.userlist.push(user);

  }

}
<!------------------model.ts------------------>
export class User{
    username:string;
    password:string;
}
