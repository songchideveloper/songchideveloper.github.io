## The JavaScript Module Pattern

_Date: 7/7/2016 Thur_

#### Below is the clean way to apply the _module pattern_ in JavaScript.

```javascript
var Person = (
    
    var _name = null; 
    
    var setName = function (name) {
        _name = name;
    };
    
    var displayName = function () {
        console.log('Hi, my name is ', _name);
    };
    
    
    return {
        setName: setName,
        displayName: displayName
    };
    
)();

// now calling the module
Person.setName('Will');
Person.displayName();  // ==> 'Hi, my name is Will'

```

#### To extend the original module
Here is the clean way to __extend__ our original module, by passing the original Module to the `IIFE` expression of the new module:
```javascript
var ModuleExt = (function(Person){
    
    var _age = null;
    
    var setAge = function(age) {
        _age = age;
    };
    
    var displayAge = function() {
        console.log('Not really want to mention that, but I am ' + age + ' years old now.');
    };
    
})(Person || {});

// Now the Person module got extended
Person.setAge(88);
Person.displayAge(); // ==> 'Not really want to mention that, but I am 88 years old now.'
```