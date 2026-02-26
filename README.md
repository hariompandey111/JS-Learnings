<div align="center">
  <h1>⚡ JavaScript Interview Questions & Answers</h1>
  <p>From basic to advanced: test your JavaScript knowledge, refresh your skills, or prepare for your next interview 🚀</p>

  <a href="https://github.com/hariompandey111/JS-Learnings/stargazers"><img src="https://img.shields.io/github/stars/hariompandey111/JS-Learnings?style=flat-square" alt="Stars"></a>
  <a href="https://github.com/hariompandey111/JS-Learnings/network/members"><img src="https://img.shields.io/github/forks/hariompandey111/JS-Learnings?style=flat-square" alt="Forks"></a>
</div>

---

> **How to use:** Click the **▼ View Answer** toggle below each question to reveal the answer. Click again to hide it.  
> **Run Code:** Each snippet has a **▶ Run Code** link — click it to execute the code live in your browser via [RunKit](https://runkit.com).

---

## 📋 Table of Contents

| # | Question |
|---|----------|
| 1 | [What is the output?](#q1) |
| 2 | [What is the output?](#q2) |
| 3 | [What is the output?](#q3) |
| 4 | [What is the output?](#q4) |
| 5 | [What is the output?](#q5) |
| 6 | [What is the output?](#q6) |
| 7 | [What is the output?](#q7) |
| 8 | [What is the output?](#q8) |
| 9 | [What is the output?](#q9) |
| 10 | [What is the output?](#q10) |
| 11 | [What is the output?](#q11) |
| 12 | [What is the output?](#q12) |
| 13 | [What is the output?](#q13) |
| 14 | [What is the output?](#q14) |
| 15 | [What is the output?](#q15) |
| 16 | [What is the output?](#q16) |
| 17 | [What is the output?](#q17) |
| 18 | [What is the output?](#q18) |
| 19 | [What is the output?](#q19) |
| 20 | [What is the output?](#q20) |

---

<a name="q1"></a>
### 1. What is the output?

```javascript
function sayHi() {
  console.log(name);
  console.log(age);
  var name = "Lydia";
  let age = 21;
}

sayHi();
```

- A: `Lydia` and `21`
- B: `Lydia` and `undefined`
- C: `undefined` and `ReferenceError`
- D: `ReferenceError` and `ReferenceError`

<details>
<summary><b>▼ View Answer</b></summary>
<br/>

**Answer: C**

Within the function, we first declare `name` with the `var` keyword. This means that the variable gets **hoisted** (memory space is set up during the creation phase) with the default value of `undefined`, until we actually get to the line where we define the variable.

Variables declared with `let` (and `const`) are **hoisted but not initialized** — accessing them before their declaration causes a `ReferenceError`. This is called the **Temporal Dead Zone**.

```
undefined   ← var name is hoisted with value undefined
ReferenceError ← let age is in the Temporal Dead Zone
```

[▶ Run Code](https://runkit.com/embed/javascript?source=function%20sayHi()%20%7B%0A%20%20console.log(name)%3B%0A%20%20console.log(age)%3B%0A%20%20var%20name%20%3D%20%22Lydia%22%3B%0A%20%20let%20age%20%3D%2021%3B%0A%7D%0AsayHi()%3B)

</details>

---

<a name="q2"></a>
### 2. What is the output?

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}

for (let j = 0; j < 3; j++) {
  setTimeout(() => console.log(j), 1);
}
```

- A: `0 1 2` and `0 1 2`
- B: `0 1 2` and `3 3 3`
- C: `3 3 3` and `0 1 2`
- D: `3 3 3` and `3 3 3`

<details>
<summary><b>▼ View Answer</b></summary>
<br/>

**Answer: C**

Because of the **event queue** in JavaScript, the `setTimeout` callback is called _after_ the loop has executed.

The variable `i` in the first loop is declared with `var` — it is **global**. During the loop, we increment `i` each time. By the time `setTimeout` fires, `i` is already `3` in all three callbacks.

In the second loop, the variable `j` is declared with `let` — it has **block scope**. Each iteration creates a new binding of `j`, so each `setTimeout` closure captures its own `j`.

```
3 3 3   ← var i shared across all callbacks
0 1 2   ← let j creates a new scope each iteration
```

[▶ Run Code](https://runkit.com/embed/javascript?source=for%20(var%20i%20%3D%200%3B%20i%20%3C%203%3B%20i%2B%2B)%20%7B%0A%20%20setTimeout(()%20%3D%3E%20console.log(i)%2C%201)%3B%0A%7D%0Afor%20(let%20j%20%3D%200%3B%20j%20%3C%203%3B%20j%2B%2B)%20%7B%0A%20%20setTimeout(()%20%3D%3E%20console.log(j)%2C%201)%3B%0A%7D)

</details>

---

<a name="q3"></a>
### 3. What is the output?

```javascript
const shape = {
  radius: 10,
  diameter() {
    return this.radius * 2;
  },
  perimeter: () => 2 * Math.PI * this.radius,
};

console.log(shape.diameter());
console.log(shape.perimeter());
```

- A: `20` and `62.83185307179586`
- B: `20` and `NaN`
- C: `20` and `63`
- D: `NaN` and `63`

<details>
<summary><b>▼ View Answer</b></summary>
<br/>

**Answer: B**

`diameter` is a **regular function**, so `this` refers to the `shape` object → `this.radius` is `10` → returns `20`.

`perimeter` is an **arrow function**. Arrow functions do **not** have their own `this` — they inherit `this` from the surrounding (lexical) scope, which here is the global scope. In the global scope `this.radius` is `undefined`, so `2 * Math.PI * undefined` = `NaN`.

```
20
NaN
```

[▶ Run Code](https://runkit.com/embed/javascript?source=const%20shape%20%3D%20%7B%0A%20%20radius%3A%2010%2C%0A%20%20diameter()%20%7B%20return%20this.radius%20*%202%3B%20%7D%2C%0A%20%20perimeter%3A%20()%20%3D%3E%202%20*%20Math.PI%20*%20this.radius%2C%0A%7D%3B%0Aconsole.log(shape.diameter())%3B%0Aconsole.log(shape.perimeter())%3B)

</details>

---

<a name="q4"></a>
### 4. What is the output?

```javascript
+true;
!"Lydia";
```

- A: `1` and `false`
- B: `false` and `NaN`
- C: `false` and `false`

<details>
<summary><b>▼ View Answer</b></summary>
<br/>

**Answer: A**

The unary `+` operator coerces its operand to a number. `true` coerces to `1`.

The `!` (logical NOT) operator first coerces its operand to a boolean, then negates it. A non-empty string is **truthy**, so `!"Lydia"` → `!true` → `false`.

```
1
false
```

[▶ Run Code](https://runkit.com/embed/javascript?source=console.log(%2Btrue)%3B%0Aconsole.log(!%22Lydia%22)%3B)

</details>

---

<a name="q5"></a>
### 5. Which one is true?

```javascript
const bird = {
  size: "small",
};

const mouse = {
  name: "Mickey",
  small: true,
};
```

- A: `mouse.bird.size` is not valid
- B: `mouse[bird.size]` is not valid
- C: `mouse[bird["size"]]` is not valid
- D: All of them are valid

<details>
<summary><b>▼ View Answer</b></summary>
<br/>

**Answer: A**

`mouse.bird` is `undefined` because there is no `bird` property on `mouse`. Accessing `.size` on `undefined` throws a `TypeError`.

`bird.size` evaluates to `"small"`, so `mouse[bird.size]` → `mouse["small"]` → `true`. ✅  
`bird["size"]` also evaluates to `"small"`, so `mouse[bird["size"]]` → `mouse["small"]` → `true`. ✅

[▶ Run Code](https://runkit.com/embed/javascript?source=const%20bird%20%3D%20%7B%20size%3A%20%22small%22%20%7D%3B%0Aconst%20mouse%20%3D%20%7B%20name%3A%20%22Mickey%22%2C%20small%3A%20true%20%7D%3B%0Aconsole.log(mouse%5Bbird.size%5D)%3B%0Aconsole.log(mouse%5Bbird%5B%22size%22%5D%5D)%3B%0A%2F%2F%20mouse.bird.size%20would%20throw%20TypeError)

</details>

---

<a name="q6"></a>
### 6. What is the output?

```javascript
let c = { greeting: "Hey!" };
let d;

d = c;
c.greeting = "Hello";
console.log(d.greeting);
```

- A: `Hello`
- B: `Hey!`
- C: `undefined`
- D: `ReferenceError`
- E: `TypeError`

<details>
<summary><b>▼ View Answer</b></summary>
<br/>

**Answer: A**

Objects are stored and copied **by reference**. When you write `d = c`, both `d` and `c` point to the **same object** in memory. Changing `c.greeting` also changes `d.greeting` because they reference the same object.

```
Hello
```

[▶ Run Code](https://runkit.com/embed/javascript?source=let%20c%20%3D%20%7B%20greeting%3A%20%22Hey!%22%20%7D%3B%0Alet%20d%3B%0Ad%20%3D%20c%3B%0Ac.greeting%20%3D%20%22Hello%22%3B%0Aconsole.log(d.greeting)%3B)

</details>

---

<a name="q7"></a>
### 7. What is the output?

```javascript
let a = 3;
let b = new Number(3);
let c = 3;

console.log(a == b);
console.log(a === b);
console.log(b === c);
```

- A: `true` `false` `true`
- B: `false` `false` `true`
- C: `true` `false` `false`
- D: `false` `true` `false`

<details>
<summary><b>▼ View Answer</b></summary>
<br/>

**Answer: C**

`new Number(3)` creates a **Number wrapper object**, not a primitive number. 

`==` performs type coercion — the object is coerced to the primitive `3`, so `a == b` → `3 == 3` → `true`.

`===` checks both value **and type** without coercion. `a` is a number primitive; `b` is a Number **object**. Different types → `false`.

```
true
false
false
```

[▶ Run Code](https://runkit.com/embed/javascript?source=let%20a%20%3D%203%3B%0Alet%20b%20%3D%20new%20Number(3)%3B%0Alet%20c%20%3D%203%3B%0Aconsole.log(a%20%3D%3D%20b)%3B%0Aconsole.log(a%20%3D%3D%3D%20b)%3B%0Aconsole.log(b%20%3D%3D%3D%20c)%3B)

</details>

---

<a name="q8"></a>
### 8. What is the output?

```javascript
class Chameleon {
  static colorChange(newColor) {
    this.newColor = newColor;
    return this.newColor;
  }

  constructor({ newColor = "green" } = {}) {
    this.newColor = newColor;
  }
}

const freddie = new Chameleon({ newColor: "purple" });
console.log(freddie.colorChange("orange"));
```

- A: `orange`
- B: `purple`
- C: `green`
- D: `TypeError`

<details>
<summary><b>▼ View Answer</b></summary>
<br/>

**Answer: D**

`colorChange` is a **static** method. Static methods are only available on the class itself, not on instances. `freddie` is an instance, so `freddie.colorChange` is `undefined`, and calling it throws a `TypeError`.

```
TypeError: freddie.colorChange is not a function
```

[▶ Run Code](https://runkit.com/embed/javascript?source=class%20Chameleon%20%7B%0A%20%20static%20colorChange(newColor)%20%7B%0A%20%20%20%20this.newColor%20%3D%20newColor%3B%0A%20%20%20%20return%20this.newColor%3B%0A%20%20%7D%0A%20%20constructor(%7B%20newColor%20%3D%20%22green%22%20%7D%20%3D%20%7B%7D)%20%7B%0A%20%20%20%20this.newColor%20%3D%20newColor%3B%0A%20%20%7D%0A%7D%0Aconst%20freddie%20%3D%20new%20Chameleon(%7B%20newColor%3A%20%22purple%22%20%7D)%3B%0Aconsole.log(freddie.colorChange(%22orange%22))%3B)

</details>

---

<a name="q9"></a>
### 9. What is the output?

```javascript
let greeting;
greetign = {}; // Typo!
console.log(greetign);
```

- A: `{}`
- B: `ReferenceError: greetign is not defined`
- C: `undefined`

<details>
<summary><b>▼ View Answer</b></summary>
<br/>

**Answer: A**

`greetign` (the misspelled variable) is assigned `{}` without `let`/`const`/`var`. In **non-strict mode**, JavaScript creates a **global variable** named `greetign`. So `console.log(greetign)` prints `{}`.

> 💡 Use `"use strict"` at the top of your files to catch accidental global variable creation (`ReferenceError` would be thrown).

```
{}
```

[▶ Run Code](https://runkit.com/embed/javascript?source=let%20greeting%3B%0Agreetign%20%3D%20%7B%7D%3B%0Aconsole.log(greetign)%3B)

</details>

---

<a name="q10"></a>
### 10. What happens when we do this?

```javascript
function bark() {
  console.log("Woof!");
}

bark.animal = "dog";
```

- A: Nothing, this is totally fine!
- B: `SyntaxError`. You cannot add properties to a function this way.
- C: `"Woof"` gets logged.
- D: `ReferenceError`

<details>
<summary><b>▼ View Answer</b></summary>
<br/>

**Answer: A**

In JavaScript, functions are **first-class objects** — you can add properties to them just like any other object. `bark.animal = "dog"` is perfectly valid. `bark.animal` will return `"dog"`.

[▶ Run Code](https://runkit.com/embed/javascript?source=function%20bark()%20%7B%20console.log(%22Woof!%22)%3B%20%7D%0Abark.animal%20%3D%20%22dog%22%3B%0Aconsole.log(bark.animal)%3B)

</details>

---

<a name="q11"></a>
### 11. What is the output?

```javascript
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const member = new Person("Lydia", "Hallie");
Person.getFullName = function() {
  return `${this.firstName} ${this.lastName}`;
};

console.log(member.getFullName());
```

- A: `TypeError`
- B: `SyntaxError`
- C: `Lydia Hallie`
- D: `undefined undefined`

<details>
<summary><b>▼ View Answer</b></summary>
<br/>

**Answer: A**

`getFullName` is added directly to the **constructor function**, not to its `prototype`. `member` is an instance — it does not have access to properties added directly on `Person`. Calling `member.getFullName()` throws a `TypeError`.

> 💡 To make `getFullName` available on all instances, add it to `Person.prototype`:
> ```javascript
> Person.prototype.getFullName = function() { ... }
> ```

[▶ Run Code](https://runkit.com/embed/javascript?source=function%20Person(firstName%2C%20lastName)%20%7B%0A%20%20this.firstName%20%3D%20firstName%3B%0A%20%20this.lastName%20%3D%20lastName%3B%0A%7D%0Aconst%20member%20%3D%20new%20Person(%22Lydia%22%2C%20%22Hallie%22)%3B%0APerson.getFullName%20%3D%20function()%20%7B%20return%20%60%24%7Bthis.firstName%7D%20%24%7Bthis.lastName%7D%60%3B%20%7D%3B%0Aconsole.log(member.getFullName())%3B)

</details>

---

<a name="q12"></a>
### 12. What is the output?

```javascript
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const lydia = new Person("Lydia", "Hallie");
const sarah = Person("Sarah", "Smith");

console.log(lydia);
console.log(sarah);
```

- A: `Person {firstName: "Lydia", lastName: "Hallie"}` and `undefined`
- B: `Person {firstName: "Lydia", lastName: "Hallie"}` and `Person {firstName: "Sarah", lastName: "Smith"}`
- C: `Person {firstName: "Lydia", lastName: "Hallie"}` and `{}`
- D: `Person {firstName: "Lydia", lastName: "Hallie"}` and `ReferenceError`

<details>
<summary><b>▼ View Answer</b></summary>
<br/>

**Answer: A**

`lydia` is created with `new`, so `this` inside `Person` refers to the new object. The new object is returned and assigned to `lydia`.

`sarah` calls `Person` as a **regular function** (no `new`). `this` refers to the global object (`window` in browsers). `firstName` and `lastName` are set on the global object. `Person` has no explicit `return` statement, so it returns `undefined`.

```
Person { firstName: 'Lydia', lastName: 'Hallie' }
undefined
```

[▶ Run Code](https://runkit.com/embed/javascript?source=function%20Person(firstName%2C%20lastName)%20%7B%0A%20%20this.firstName%20%3D%20firstName%3B%0A%20%20this.lastName%20%3D%20lastName%3B%0A%7D%0Aconst%20lydia%20%3D%20new%20Person(%22Lydia%22%2C%20%22Hallie%22)%3B%0Aconst%20sarah%20%3D%20Person(%22Sarah%22%2C%20%22Smith%22)%3B%0Aconsole.log(lydia)%3B%0Aconsole.log(sarah)%3B)

</details>

---

<a name="q13"></a>
### 13. What are the three phases of event propagation?

- A: Target > Capturing > Bubbling
- B: Bubbling > Target > Capturing
- C: Capturing > Target > Bubbling
- D: Capturing > Bubbling > Target

<details>
<summary><b>▼ View Answer</b></summary>
<br/>

**Answer: C**

During the **capturing** phase, the event travels down from the root through all ancestors to the target element.

At the **target** phase, the event fires on the element itself.

During the **bubbling** phase, the event travels back up from the target to the root.

```
Capturing → Target → Bubbling
```

</details>

---

<a name="q14"></a>
### 14. All objects have prototypes.

- A: True
- B: False

<details>
<summary><b>▼ View Answer</b></summary>
<br/>

**Answer: B**

All objects have prototypes **except the base object** (`Object.prototype`). `Object.prototype.__proto__` is `null` — it is the root of the prototype chain.

```javascript
console.log(Object.prototype.__proto__); // null
```

[▶ Run Code](https://runkit.com/embed/javascript?source=console.log(Object.prototype.__proto__)%3B)

</details>

---

<a name="q15"></a>
### 15. What is the output?

```javascript
function sum(a, b) {
  return a + b;
}

sum(1, "2");
```

- A: `NaN`
- B: `TypeError`
- C: `"12"`
- D: `3`

<details>
<summary><b>▼ View Answer</b></summary>
<br/>

**Answer: C**

JavaScript is **dynamically typed** — values can change type at runtime. When one operand of `+` is a string, the other is **coerced to a string** and the two are concatenated.

```
"12"
```

[▶ Run Code](https://runkit.com/embed/javascript?source=function%20sum(a%2C%20b)%20%7B%20return%20a%20%2B%20b%3B%20%7D%0Aconsole.log(sum(1%2C%20%222%22))%3B)

</details>

---

<a name="q16"></a>
### 16. What is the output?

```javascript
let number = 0;
console.log(number++);
console.log(++number);
console.log(number);
```

- A: `1` `1` `2`
- B: `1` `2` `2`
- C: `0` `2` `2`
- D: `0` `1` `2`

<details>
<summary><b>▼ View Answer</b></summary>
<br/>

**Answer: C**

**Post-increment** (`number++`): returns the current value (`0`), then increments → `number` becomes `1`.

**Pre-increment** (`++number`): increments first (`number` becomes `2`), then returns the new value → `2`.

The final `console.log(number)` prints `2`.

```
0
2
2
```

[▶ Run Code](https://runkit.com/embed/javascript?source=let%20number%20%3D%200%3B%0Aconsole.log(number%2B%2B)%3B%0Aconsole.log(%2B%2Bnumber)%3B%0Aconsole.log(number)%3B)

</details>

---

<a name="q17"></a>
### 17. What is the output?

```javascript
function getPersonInfo(one, two, three) {
  console.log(one);
  console.log(two);
  console.log(three);
}

const person = "Lydia";
const age = 21;

getPersonInfo`${person} is ${age} years old`;
```

- A: `"Lydia"` `21` `["", " is ", " years old"]`
- B: `["", " is ", " years old"]` `"Lydia"` `21`
- C: `"Lydia"` `["", " is ", " years old"]` `21`

<details>
<summary><b>▼ View Answer</b></summary>
<br/>

**Answer: B**

When using **tagged template literals**, the first argument is always an array of the string parts, and the remaining arguments are the interpolated values.

```
["", " is ", " years old"]
Lydia
21
```

[▶ Run Code](https://runkit.com/embed/javascript?source=function%20getPersonInfo(one%2C%20two%2C%20three)%20%7B%0A%20%20console.log(one)%3B%0A%20%20console.log(two)%3B%0A%20%20console.log(three)%3B%0A%7D%0Aconst%20person%20%3D%20%22Lydia%22%3B%0Aconst%20age%20%3D%2021%3B%0AgetPersonInfo%60%24%7Bperson%7D%20is%20%24%7Bage%7D%20years%20old%60%3B)

</details>

---

<a name="q18"></a>
### 18. What is the output?

```javascript
function checkAge(data) {
  if (data === { age: 18 }) {
    console.log("You are an adult!");
  } else if (data == { age: 18 }) {
    console.log("You are still an adult.");
  } else {
    console.log(`Hmm.. You don't have an age I guess`);
  }
}

checkAge({ age: 18 });
```

- A: `You are an adult!`
- B: `You are still an adult.`
- C: `Hmm.. You don't have an age I guess`

<details>
<summary><b>▼ View Answer</b></summary>
<br/>

**Answer: C**

When comparing objects, `===` and `==` both check **reference equality** (do they point to the same object in memory?). `{ age: 18 }` in the condition is a **new object literal** each time — it does not reference the same object as `data`. Neither comparison is `true`.

```
Hmm.. You don't have an age I guess
```

[▶ Run Code](https://runkit.com/embed/javascript?source=function%20checkAge(data)%20%7B%0A%20%20if%20(data%20%3D%3D%3D%20%7B%20age%3A%2018%20%7D)%20%7B%0A%20%20%20%20console.log(%22You%20are%20an%20adult!%22)%3B%0A%20%20%7D%20else%20if%20(data%20%3D%3D%20%7B%20age%3A%2018%20%7D)%20%7B%0A%20%20%20%20console.log(%22You%20are%20still%20an%20adult.%22)%3B%0A%20%20%7D%20else%20%7B%0A%20%20%20%20console.log(%60Hmm..%20You%20don't%20have%20an%20age%20I%20guess%60)%3B%0A%20%20%7D%0A%7D%0AcheckAge(%7B%20age%3A%2018%20%7D)%3B)

</details>

---

<a name="q19"></a>
### 19. What is the output?

```javascript
function getAge(...args) {
  console.log(typeof args);
}

getAge(21);
```

- A: `"number"`
- B: `"array"`
- C: `"object"`
- D: `"NaN"`

<details>
<summary><b>▼ View Answer</b></summary>
<br/>

**Answer: C**

**Rest parameters** (`...args`) collect all remaining arguments into an **array**. Arrays are objects in JavaScript, so `typeof args` returns `"object"`.

```
object
```

[▶ Run Code](https://runkit.com/embed/javascript?source=function%20getAge(...args)%20%7B%20console.log(typeof%20args)%3B%20%7D%0AgetAge(21)%3B)

</details>

---

<a name="q20"></a>
### 20. What is the output?

```javascript
const promise1 = new Promise((resolve) => {
  setTimeout(resolve, 500, "one");
});

const promise2 = new Promise((resolve) => {
  setTimeout(resolve, 100, "two");
});

Promise.race([promise1, promise2]).then((value) => {
  console.log(value);
});
```

- A: `"one"`
- B: `"two"`
- C: `"one"` `"two"`
- D: `"two"` `"one"`

<details>
<summary><b>▼ View Answer</b></summary>
<br/>

**Answer: B**

`Promise.race()` settles with the first promise that **settles** (resolves or rejects). `promise2` resolves after `100ms`, which is before `promise1`'s `500ms`. So the `.then` callback receives `"two"`.

```
"two"
```

[▶ Run Code](https://runkit.com/embed/javascript?source=const%20p1%20%3D%20new%20Promise((resolve)%20%3D%3E%20setTimeout(resolve%2C%20500%2C%20%22one%22))%3B%0Aconst%20p2%20%3D%20new%20Promise((resolve)%20%3D%3E%20setTimeout(resolve%2C%20100%2C%20%22two%22))%3B%0APromise.race(%5Bp1%2C%20p2%5D).then((v)%20%3D%3E%20console.log(v))%3B)

</details>

---

<div align="center">

## 🌟 More coming soon!

Found an error? Want to contribute a new question?  
[Open an issue](https://github.com/hariompandey111/JS-Learnings/issues) or submit a Pull Request!

**Happy Learning! 🚀**

</div>
