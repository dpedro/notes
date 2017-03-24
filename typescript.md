# Typescript
## Interfaces

```javascript
interface LabelledValue {
    label: string;
}

function printLabel(labelledObj: LabelledValue) {
    console.log(labelledObj.label);
}

let myObj = {size: 10, label: "Size 10 Object"};
printLabel(myObj);
```
## Class
### Static properties and methods

```javascript
class MyClassWithStaticMembers {
    static aStaticCounter: number = 0;
    aPublicNumber: number = 0;
    constructor() {
        console.log(MyClassWithStaticMembers.aStaticCounter++);
    }
    aPublicMethod() {
        console.log("This is a public method")
    }
    static aStaticMethod() {
        console.log("This is a static method")
    }
}
MyClassWithStaticMembers.aStaticMethod(); // This is a static method
let foo = new MyClassWithStaticMembers(); // 0
let bar = new MyClassWithStaticMembers(); // 1
foo.aPublicMethod() // This is a public method
foo.aStaticMethod() // Error
MyClassWithStaticMembers.aPublicMethod() // Error
```

Compiled JavaScript
```javascript
var MyClassWithStaticMembers = (function () {
    function MyClassWithStaticMembers() {
        console.log(MyClassWithStaticMembers.aStaticCounter++);
    }
    MyClassWithStaticMembers.prototype.aPublicMethod = function () {
        console.log("This is a public method");
    };
    MyClassWithStaticMembers.aStaticMethod = function () {
        console.log("This is a static method");
    };
    MyClassWithStaticMembers.aStaticCounter = 0;
    return MyClassWithStaticMembers;
}());
```
