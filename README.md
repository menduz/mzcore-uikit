# mzcore-uikit

Simple components for mzcore, includes: `<mz-autocomplete>` `<clear />` 

## Install

* Install with bower: `$ bower install mzcore-uikit --save`  
* Include the following line where you want use this components
```typescript
// in your own module 'modules/select_user_page.ts'
import * as uikit 'bower_components/mzcore-uikit/index'
```  
```typescript
// or in 'components/components.ts'
export * from 'bower_components/mzcore-uikit/index'
```  
*  We are ready to use the components

# Components

## `<mz-autocomplete>`
Is a simple autocomplete component with a very basic style, so you can add a custom theme. It extends MzInput in order to use with a `mz-model="selectedItem"` attribute.
You must provide a method used for fullfill the autocomplete list, this method should return a Promise which resolves as an array with values or objects.

### Usage:

```xml
<!-- myView.xml -->
...

<mz-autocomplete searchMethod="{this.performSearch}" placeholder="Search an user" mz-model="selectedUser">
  <b>{scope.Name}</b> (<span>{scope.Email}</span>)
</mz-autocomplete>

<h1>Selected user details</h1>
<ul visible="{this.selectedUser}">
  <li>Name: {this.selectedUser.Name}</li>
  <li>Email: {this.selectedUser.Email}</li>
</ul>
<div visible="{!this.selectedUser}">
  No user selected!
</div>

...
```

```typescript
/// myController.ts
interface IUser { Name: string; Email: string; }

@MyController.Template(`myView.xml`)
export class MyController extends mz.widgets.BasePagelet /* or mz.app.Page or any other widget or component */ {


  @MyController.proxy
  selectedUser: IUser;
  
  performSearch(typedText: string){
    return mz.xr.get(mz.xr.urlEncode `@api/users?filter=${typedText}`)
                .then(x => x.data);
  }
  
  
  
  
  /*
    perfomSearch(){
      return Promise.resolve(
        [
          { Name: 'Agustin', Email: 'agustin@soflex.com.ar' }, 
          { Name: 'Uriel', Email: 'uriel@soflex.com.ar' }
        ]
      );
    }
  */
}

```

You also can initialize with a value:
```typescript
export class UserSearchWindow extends mz.app.Page {
  @UserSearchWindow.proxy
  selectedUser = {
    Name: 'Agustin',
    Email: 'agustin@soflex.com.ar'
  }
}
```
