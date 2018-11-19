# Functions

## Problem Statement

Functions are the single most important unit of code in JavaScript. Much like a
`<div>` or a `<section>` in HTML, functions serve as ways to group together
related bits of JavaScript code.  Grouped code is easier to read, debug, and
improve.

## Objectives

1. Define abstraction
2. Explain that functions are abstractions
3. Explain how to _call_ a function
4. Define "Generalization"
5. Demonstrate "Generalization" by using _parameters_ and _arguments_
6. Demonstrate _return values_

## Define Abstraction

Abstraction comes from Latin roots which mean "to pull away." It's the
"take-away" or "impression" of a whole thing.  As humans, we often take sets of
single actions or things and _abstract them_ into another word.

That word that we "pull away" is the "abstraction." Literally it means "the
pulled away thing." You might not think about it often, but your brain is full
of abstractions.

| Single Units | Abstraction |
|-------------|--------------|
|John, Paul, George, Ringo | The Beatles |
|Get two pieces of bread, put jam on ... | Make a peanut butter and jelly sandwich |
|Hermione, Harry, Ron | Troublesome Gryffindors |
| visit site, make userid, make password... | Sign up for Flatbook|
| get in the lift, hit "G" button, exit elevator, walk to subway... | Go home|

We create abstractions to make it easier to shorten our sentences. We'd never
get anything done if we couldn't abstract! We also use abstractions to decide
what doesn't fit or what should fit. "Mozart" doesn't belong with The Beatles,
but he does fit with "Baroque Masters."

Abstractions help us think about complex activities. Humans brought the pattern of
"abstracting work" to JavaScript. Abstractions that hold work are called
_functions_.

## Explain That Functions Are Abstractions

Functions combine series of steps under a new name. That's why they're
_abstractions_. We'll call that the _function name_. More formally:

**A function is an object that contains a sequence JavaScript
statements.  We can execute or _call_ it multiple times.**

To _call_ a function means to run the independent pieces that make it.
Synonyms to _call_ that you might see are _execute_ and _invoke_.

Let's describe a series of single, non-abstract, tasks:

```javascript
console.log("Wake Byron the poodle");
console.log("Leash Byron the poodle");
console.log("Walk to the park Byron the poodle");
console.log("Throw the fribsee for Byron the poodle");
console.log("Walk home with Byron the poodle");
console.log("Unleash Byron the poodle");
```

To abstract these single actions into a collective name, we do:

```javascript
function exerciseByronThePoodle() {
  console.log("Wake Byron the poodle");
  console.log("Leash Byron the poodle");
  console.log("Walk to the park Byron the poodle");
  console.log("Throw the fribsee for Byron the poodle");
  console.log("Walk home with Byron the poodle");
  console.log("Unleash Byron the poodle");
}
```

This code is a _function declaration_.

Here we have _abstracted_ 6 activities into 1 activity:
`exerciseByronThePoodle`.

> **ASIDE**: Abstractions themselves can be lumped together _as if_ they were
> single things.  The abstraction `dailyDogCareForByron` probably includes
> `feedByronThePoodle`, `giveWaterToByronThePoodle` etc.

## Explain How To _Call_ a Function

To execute a function you add `()` after its name. To execute the function we
just defined in JavaScript, you run: `exerciseByronThePoodle()`. When we ran
`document.querySelector()`, we were _calling_ a function. `Math.floor()` is
another function. That `()` is also known as the _invocation operator_ because
it tells JavaScript to...invoke the function.

> **LEARNING TIP**: Try defining a small function in the JavaScript console to
> test this out. You can copy the syntax provided above.

A _function_ must be _declared_ before it can be called. Calling
`exerciseByronThePoodle()` before the function has been declared causes an
error for JavaScript.

## Define "Generalization"

Looking at our abstraction, `exerciseByronThePoodle()`, it's pretty concrete, the
opposite of abstract. It's concrete because it only works for Byron the Poodle.
Our function would be more _abstract_ if it were written for _all dogs_ and it
just-so-happened that Byron the Poodle was one of the eligible things to
undergo the function's processes. The process of moving from _concrete_ to
_abstract_ is called "generalization" (or "abstraction," by some).

## Demonstrate "Generalization" By Using _Parameters_ And _Arguments_

Let's make `exerciseByronThePoodle()` more general. Looking at the
`console.log()` statements, we repeatedly refer to a dog's name and a dog's
breed. Both of these are `Strings`. If we were to write them as JavaScript
variables inside the function we might write `dogName` and `dogBreed`.

Let's use `String` interpolation to generalize the _body_ of our function

```javascript
function exerciseByronThePoodle() {
  let dogName = "Byron";
  let dogBreed = "poodle";
  console.log(`Wake ${dogName} the ${dogBreed}`);
  console.log(`Leash ${dogName} the ${dogBreed}`);
  console.log(`Walk to the park ${dogName} the ${dogBreed}`);
  console.log(`Throw the fribsee for ${dogName} the ${dogBreed}`);
  console.log(`Walk home with ${dogName} the ${dogBreed}`);
  console.log(`Unleash ${dogName} the ${dogBreed}`);
}
```

If we _call_ this function, we'll get the exact _same_ result as the original
`exerciseByronThePoodle()`.

But there are some advances here. We define the `dogName` and `dogBreed` in
only one place. That means we can change things a bit easier now by changing
these variables instead of using find-and-replace (`2 * 6 = 12`) twelve times.

Our problem now is that our function has the `dogName` and `dogBreed` locked
in. If we could make it possible to tell each _call_ of the function "Hey use
these `String`s instead" we could get more _general_.

That's the purpose of _parameters_. _Parameters_ are locally-scoped variables
that are usable ("scoped") to inside the function. In our example, our variables
`dogName` and `dogBreed` should become _parameters_.  They're defined inside of
the _function declaration's_ `()`.

```javascript
function exerciseDog(dogName, dogBreed) {
...
...
```

JavaScript will assign the _arguments_ of "Byron" and "poodle" to the
_parameters_ `dogName` and `dogBreed` when this function is called like so:

```javascript
function exerciseDog("Byron", "poodle");
```

The full _function declaration_ for `exerciseDog` is:

```javascript
function exerciseDog(dogName, dogBreed) {
  console.log(`Wake ${dogName} the ${dogBreed}`);
  console.log(`Leash ${dogName} the ${dogBreed}`);
  console.log(`Walk to the park ${dogName} the ${dogBreed}`);
  console.log(`Throw the fribsee for ${dogName} the ${dogBreed}`);
  console.log(`Walk home with ${dogName} the ${dogBreed}`);
  console.log(`Unleash ${dogName} the ${dogBreed}`);
}
```

When the function is _called_, it assigns `dogName = "Byron"` and `dogBreed =
"poodle"`. The parameters are usable inside the function body _as if_ they had
been set with `let` inside the function.

Because our function is now more _general_, we can:

```javascript
exerciseDog("Boo", "puggle");
exerciseDog("Jojo", "mutt");
exerciseDog("Emmeline", "bernedoodle");
```

If expected arguments aren't given, the parameters won't be set. The
parameters' values will be `undefined`.  This is just like non-initialized
variables; set them else they're `undefined`.  **This will not cause an error
in JavaScript**. This can lead to humorous bugs like:

```text
"Wake undefined the undefined"  // From: console.log("Wake ${dogName} the ${dogBreed}");
```

We can assign default arguments to our parameters. While it's not as attention-
grabbing as a real error, it's a helpful signal that we've run off the rails.

```javascript
function exerciseDog(dogName="ERROR the Broken Dog", dogBreed="Sick Puppy") {
...
```

In summary, we went from:

* a list of operations
* to a wrapped abstraction called a function
* to a more general version of the function

## Demonstrate _Return Values_

Sometimes it's helpful to send something _back_ to the place where the function
was _called_. It's like a "summary" of what happened in the function. In real
life, we expect the function "bake a cake" to return a "cake". Or we expect
"Visit the ATM" to return paper money. Functions in JavaScript can also return
things.  Consider:

```javascript

let weatherToday = "Rainy";

function exerciseDog(dogName, dogBreed) {
  if (weatherToday === "Rainy") {
    return `${dogName} did not exercise due to rain`;
  }
  console.log(`Wake ${dogName} the ${dogBreed}`);
  console.log(`Leash ${dogName} the ${dogBreed}`);
  console.log(`Walk to the park ${dogName} the ${dogBreed}`);
  console.log(`Throw the fribsee for ${dogName} the ${dogBreed}`);
  console.log(`Walk home with ${dogName} the ${dogBreed}`);
  console.log(`Unleash ${dogName} the ${dogBreed}`);
  return `${dogName} is happy and tired!`
}

let result = exerciseDog("Byron", "poodle");
console.log(result); // => "Byron did not exercise due to rain"
```

In JavaScript, when a function is _called_, when it encounters a `return`
statement it "returns" the value of the thing that appears to the right of the word. The thing
could be a `String`, a `Number` or an _expression_ like `1 + 1` (which returns,
`2`, sensibly enough).

When a `return` is reached in the code, no further code behavior happens.
Above, if `weatherToday` is `truthy` **the only thing that happens** is the
evaluation of the `String`.

Return values can be saved to variables. Or they can be used as inputs to other
functions.

## Conclusion

In this lesson we learned about the  idea of abstraction, both in real life and
in code. Abstractions reduce complexity by allowing us to think in groups of
activities or things instead of being fully zoomed-in all the time. JavaScript
functions are defined:

```javascript

function functionName(argument1, argument2, argument3) {
  body code goes here
}
```

Functions are "called" by entering the function's name followed by the
_invocation operator_, `()`. "Invoke" or "execute" mean the same thing.
Arguments that the function declaration expects should be passed inside of the
invocation operator.  Functions can, but are not obligated to, return _return
values_ at the end of their execution. Return values are often results of a
process, grand totals, or success / failure data.

## Resources

- MDN
  + [Functions — reusable blocks of code](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Functions)
  + [Function return values](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Return_values)
  + [Function declaration](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)
