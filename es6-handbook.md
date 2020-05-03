# ES6 Handbook

### Function & Method

**Named Function**
```ecmascript 6
function namedFunction(param = 'default') {
    return param;
}
console.log(namedFunction('arg'));;
```

**Anonymous Function**
```ecmascript 6
// Function Expression
const anonymousFunction = function (param = 'default') { 
    return param;
}
console.log(anonymousFunction('arg'));;
```

**Arrow Function**
```ecmascript 6
// Function Expression
const arrowFunction = (param = 'default') => param;
console.log(arrowFunction('arg'));
```

**this**

The place in your code where you call a function is called the execution context. The
execution context determines the value of `this`.

**Method**
```ecmascript 6
const car = new Object(
    {
        color: 'Green',
        brand: 'Nissan',
        secondHandValue: function (usedYears = 0) { //This is method instead of function
            const oriValue = 200000;
            return oriValue - (usedYears * 10000);
        },
        showValue: function (usedYears ) { //This is method instead of function
            console.log(`${this.color} ${(this.brand)} pricing : ${this.secondHandValue(usedYears)}`);
        },
    }
)
car.showValue(4);
```

**Callback (Named Function)**
```ecmascript 6
function testCallback(callbackFunction) {
    const result = 'Done!';
    callbackFunction(result);
}
function callableFunction(result) {
    console.log(result);
}
testCallback(callableFunction);
```

**Callback (Arrow Function)**
```ecmascript 6
const testCallback = callbackFunction => {
    const result = 'Done!';
    callbackFunction(result);
};
const callableFunction = result => {
    console.log(result);
};
//callableFunction is not invoked, only passed as callback
testCallback(callableFunction); 
```

**Promise (Declare as Promise Object)**
```ecmascript 6
const doSomething = new Promise((resolve, reject) => {
    let val = Math.random().toFixed(2)
    if (val > 0.5)
        resolve(() => `${val} = Passed`) //pass a "function" to resolve function
    else
        reject(() => `${val} = Failed`)
})

doSomething
    .then(result => console.log(result()))
    .catch(error => console.log(error()))
```

**Promise (Declare as Arrow Function)**
```ecmascript 6
const doSomething = () => new Promise((resolve, reject) => {
    let val = Math.random().toFixed(2)
    if (val > 0.5)
        resolve(`${val} = Passed`) //pass a "value" to resolve function
    else
        reject(`${val} = Failed`)
});

doSomething()
    .then(result => console.log(result))
    .catch(error => console.log(error))
```

**IIFE (Immediately Invoked Function Expression)**
```ecmascript 6
// Assigning the IIFE to a variable stores the function's return value, not the function definition itself.
let result = (function () {
    return "Hello World!";
})();
// Immediately creates the output: 
console.log(result); //Immediately creates the output: Hello World!
```

**Function declaration hoisting**
```ecmascript 6
// Function declarations in JavaScript are hoisted to the top of the enclosing function or global scope.
// You can use the function before you declared it.
hoisted();
function hoisted() {
    console.log('Hello World!');
}

// function expressions are not hoisted
// ReferenceError: hoisted is not defined
notHoisted();
let notHoisted = function() {
    console.log('Hello World!');
};
```

**Async & Await (Example 1)**
```ecmascript 6
const getData = () => {
    return new Promise(resolve => {
        const period = 2000;
        setTimeout(() =>
            resolve('Final Value Received!'), period)
        console.log(`Awaiting for ${period/1000} seconds`)
    });
};

const doSomething = async () => {
    return await getData();
};

doSomething().then(result => console.log(result));
```

**Async & Await (Example 2)**
```ecmascript 6
const sleep = ms => new Promise(resolve => {
    console.log("step 2");
    // setTimeout method to resolve a Promise after a given number of milliseconds
    setTimeout(() => resolve('step 5'), ms);
    console.log("step 3");
});

const delayed = async () => {
    console.log("step 1");
    // do not pause the entire program execution. Only your function sleeps
    // effectively makes each call appear as though it’s synchronous
    // while not holding up JavaScript’s single processing thread
    await sleep(2000).then((result) => console.log(result));
    console.log("step 6");
};

delayed().then(() => console.log('step 7'));
console.log("step 4");
```


**Imperative Code vs Declarative Code**
```ecmascript 6
const array = ["One", "Two", "Three"];
//Imperative code describing how a program operates
for(let i = 0; array.length > i; i++){
    console.log(array[i]); //returns One, Two, Three
}

//Declarative code showing how a program should work
array.map((value, index, arr) => {
    console.log(value); //returns One, Two, Three
});
```

**Prototype vs Class**
```ecmascript 6
function PrototypicalGreeting(greeting) {
    this.greeting = greeting
}

PrototypicalGreeting.prototype.greet = function () {
    return this.greeting
}

const greetProto = new PrototypicalGreeting('Hello World!')
console.log(greetProto.greet())
```

```ecmascript 6
class ClassicalGreeting {
    constructor(greeting) {
        this.greeting = greeting
    }

    greet() {
        return this.greeting
    }
}

const classyGreeting = new ClassicalGreeting('Hello World!')

console.log(classyGreeting.greet())
```

**Closure**
```ecmascript 6
const counter = (function () {
    let privateCounter = 0;

    function changeBy(val) {
        privateCounter += val;
    }

    return {
        increment: function () {
            changeBy(1);
        },

        decrement: function () {
            changeBy(-1);
        },

        value: function () {
            return privateCounter;
        }
    };
})();

console.log(counter);

console.log(counter.value());  // 0.

counter.increment();
counter.increment();
console.log(counter.value());  // 2.

counter.decrement();
console.log(counter.value());  // 1.
```