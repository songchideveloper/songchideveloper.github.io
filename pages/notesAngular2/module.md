
##### Typical Module Structual
We'll have one root Module (AppModule) to launch the app; we then import feature modules to **extend** our app.


##### Scope between Modules
The root module and the feature modules share the same execution context, the same dependency injector, which means **the services in one module are available to all.**

##### BrowserModule or CommonModule
Details: [Should I import BrowserModule or CommonModule?](https://angular.io/docs/ts/latest/cookbook/ngmodule-faq.html#!#q-browser-vs-common-module)
* The **root module** (AppModule) should import `BrowserModule` from `@angular/platform-browser`
  * The `BrowserModule` re-exports the `CommomModule` from `@angular/common`, which includes common directives like `NgIf` and `NgFor`
* Feature modules and lazy-loaded modules should import `CommonModule` instead. 
