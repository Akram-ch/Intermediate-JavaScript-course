# var vs let vs const
```Javascript
let a = "a";
var b = "b";
const c = "c";

if (true){
    let a = 2;
    var b = 2;
    const c = 2;
}
console.log(a) // "a"
console.log(b) // 2
console.log(c) // "c"
```
The var keyword is not scope safe.
var will overwrite existing variable in parent scope if defined with the same name.

whereas let and const are scope safe. i.e defining a variable with the same name will not overwrite the variable in the parent scope.


```Javascript
{
    var inScopeVar = "in scope";
    let inScopeLet = "in scope";
    const inScopeConst = "in scope";
}
console.log(inScopeVar)//"in scope"
console.log(inScopeLet)//error
console.log(inScopeConst)//error
```
Hoisting : raised up

variables declared with Var are "hoisted" up to the parent scope

```Javascript
console.log(aLet);// error undefined
console.log(aConst);// error undefined
console.log(aVar);// "aVar"

let aLet = "let";
const aConst ="const"
var= "aVar"
```
variables delcared with Var are hoisted up to the top

Var variables are added to the windows object by default

### conclusion
* Var Sucks
* Var is not scope safe
* Var variables are hoisted
* We can't acess let/const variable before declaration
* var Variables are added to the window object by default.

# The "This" keyword
"This" represents the context of the code

``` Javascript
const car = {
    model: 'corolla',
    brand: 'toyota',
    drive: function(){
        cosnole.log(this);
    }
}

car.drive(); // car object

const boom = car.drive();
boom(); //windows object

```

### Takeaways
* The 'this' keyword represents the context of the code
* by default, 'this' resolves to the global object, ie 'window' object in the browser
* 'this' is useful to access information in the current context, eg updating value of the object instance

# Arrow function vs normal function
```Javascript
function add(x){
    return x+5;
}

const substract = (x,y)=>{
    return x - y;
}

const multiply = (x, y)=> x * y; // === return x*y

const add2 = num => num + 2
``` 
### Diffrences
* arrow : we can ommit curly braces and return statement if function is a  liner
* arrow : when theres only one argument brackets are optional
* the 'this' keyword in arrow functions is automatically bound to the parents context
```Javascript
    let car{
        color: 'red'
        drive: function(){
            const inner = function(){
                console.log(this)
            }
            inner() // window object
        }
        honk : function(){
            const inner = ()=>{
                console.log(this);
            }
            inner() // car object
        }
    }
```

## Closure and higher order functions
___

Higher order functions are functions that take in another function or returns another function. 

### factory function: 
function that manufactures/creates functions

### closure :
functions inside a function

```html
<main>

</main>

<script>
    const main = document.querySelector('main');

    function headingFactory(colour){
        const closure = function(text){
            const heading = document.createElement('h1');
            heading.setAttribute('style', 'color: ' + colour);
            heading.textContent = text;
            return heading;
        }
        return closure;
    }

    const createRedHeading = headingFactory('red');
    const head1 = createRedHeading("Hello") // read heading is generated"
    main.appendChild(head1);

</script>

```

# Callbacks
callback functions are functions that are passed to another function.

example: 
```Javascript
window.addEventListener('click', function(event){
    // this is a callback function
})
```

```Javascript
function shopping(budget, afterShoppingCallback){
    const spent = 100;
    budget = budget - spent;
    afterShoppingCallback(budeget);
    return budget;
}

shopping(1000, function(budget){
console.log('watch movie');
})
```
Callback code is very hard to read and to debug, you should avoid is as much as possible.