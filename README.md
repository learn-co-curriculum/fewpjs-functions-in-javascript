# Creating Functions in JavaScript

## Learning Goals

- State the purpose of functions
- Identify what JavaScript functions are
- Demonstrate passing behaviors into functions
- Demonstrate assigning functions to variables

## Introduction

Sometimes in life, we need to take a series of steps to complete a task. Since
life isn't scripted like a TV show or movie, anything can happen that alters
each step. We need to be able to adjust accordingly.

## State the Purpose of Functions

Functions are ways to wrap up behavior into a bit of code. Functions are one
of the key pieces of any programming language. Functions can often apply to 
everyday things. Think of functions like a list of actions to take to get a
desired outcome, for example, making recipes from a cookbook.

```js
   function makeMeASandwich(ingredients) {
       let sandwich = ingredients
       return ingredients
   }
```

## Identify What JavaScript Functions Are

A function is a group of code that can be called upon, sometimes
by a name. In other words, a function is a way to group together
some code, give this group a name, and later invoke the code using
the given name.

Functions in JavaScript are first-class data. This means that they are
treated like any other variable and we can pass them as values to other
functions, like numbers, strings, arrays, and objects. They're super useful,
especially when reducing the amount of code being written. 

For example, imagine an exercise routine: every morning, we run five miles. But
afterwards — depending on the day — we might lift weights, go for a swim, or run
an extra fuve miles.

```js
function Monday() {
  console.log('Go for a five-mile run');
  console.log('Pump iron');
}

function Tuesday() {
  console.log('Go for a five-mile run');
  console.log('Swim 40 laps');
}

function Wednesday() {
  console.log('Go for a five-mile run');
  console.log('Go for a five-mile run');
}

function Thursday() {
  console.log('Go for a five-mile run');
  console.log('Pump iron');
}

function Friday() {
  console.log('Go for a five-mile run');
  console.log('Swim 40 laps');
}
```

That's pretty tedious. We now know that functions are supposed to help us reduce
this kind of repetition. 

## Demonstrate Passing Behaviors into Functions

What if we pull all of our five-mile runs into their own function? Let's build a
more concise set of functions that generates output of an exercise routine, and
let's do the same thing for lifting weights and swimming:

```js
function runFiveMiles() {
  console.log('Go for a five-mile run');
}

function liftWeights() {
  console.log('Pump iron');
}

function swimFortyLaps() {
  console.log('Swim 40 laps');
}
```

Great! Now that we've cut down a little bit more: `Monday()` could now look like

```js
function Monday() {
  runFiveMiles();
  liftWeights();
}
```

While it is a tiny bit shorter than before, there is definitely still room for
improvement. Every day, our routine includes two activities and the first activity
is always a run. That means that the second activity can be variable. What if we
created a function that took the second activity as a parameter?

```js
function exerciseRoutine(postRunActivity) {
  runFiveMiles();
  postRunActivity();
}
```

Notice that, in `exerciseRoutine()`, the `postRunActivity` parameter is
actually a function — we call it after we call `runFiveMiles()`. Now
let's try to use this new function we created in a `Monday()` function:

```js
function Monday() {
  exerciseRoutine(liftWeights);
}
```

Notice that we aren't calling `liftWeights`. When we want to pass a
function as a value, we pass it by reference. We do this by omitting
the parentheses. We're not running the function at this point. It's
up to `exerciseRoutine()` to call the function when it is needed.

If we call `Monday()`, we'll see that we run five miles, and then we
lift weights — awesome!


**Note:** you'll often see functions used in this way referred to as "callbacks."
That's because they're _called back_ after the body of the function they're
passed to completes! Callbacks are mostly used for asynchronous operations, like 
requesting a JSON file from a server, or in the case of Node.js, accessing the
file system, a database, etc.

### Inline functions

What if, though, we want to have a one-off day of Pilates in our exercise routine?
Keep in mind that our `exerciseRoutine()` function requires a function as its
first (and only) parameter. However, that function doesn't have to be defined
beforehand! We can pass what's called an _anonymous function_ to `exerciseRoutine()`.

To start with, let's use the full function syntax we've come to know and love:

```js
exerciseRoutine(function() {
  console.log('Stretch! Work that core!');
});

// "Go for a five-mile run"
// "Stretch! Work that core!"
```

We can rewrite this to be more concise by using an arrow function:

```js
exerciseRoutine(() => {
  console.log('Stretch! Work that core!');
});

// Or even shorter:
exerciseRoutine(() => console.log('Stretch! Work that core!'));
```

Notice how neither of these functions have a name — we can't refer to it elsewhere,
we just pass it in as an argument to `exerciseRoutine()`. Functions that don't have
names are, for obvious reasons, known as **anonymous functions**.

### Returning functions

Functions can also return other functions. This is useful when we want to package up
a function and its environment, but when we don't want to call it _just yet_.

For example, let's say our morning routine involves drinking a cup of coffee,
exercising immediately, and then at some point later (depending on how we feel),
eating breakfast. What we'll have for breakfast depends on what kind of exercise
we're doing.

Let's translate this to a function:

```js
function morningRoutine(exercise) {
  var breakfast = null;

  if (exercise === liftWeights) {
    breakfast = 'protein bar';
  } else if (exercise === swimFortyLaps) {
    breakfast = 'kale smoothie';
  } else {
    breakfast = 'granola';
  }

  exerciseRoutine(exercise);

  // we could give this function a name if we wanted to,
  // but since it's only available _inside_ morningRoutine(),
  // we don't need to
  return function() {
    console.log(`Nom nom nom, this ${breakfast} is delicious!`);
  }
}
```

Now when we call `morningRoutine()`, we'll get a function back:

```js
var afterExercise = morningRoutine(liftWeights);
```

And we can call that function later:

```js
afterExercise();
```

## Demonstrate Assigning Functions to Variables

In JavaScript we can assign a function to a variable and we can call that
function by its variable name.

For example:
```js
const makeMeASandwich = function(ingredients) {
       let sandwich = ingredients
       return ingredients
   }
```
or
```js
const monday = function() {
  exerciseRoutine(liftWeights);
}
```
This technique can be used to further simplify code, pass data around, and/or
pass data around.

## Conclusion

Functions are the cornerstones of any functional programming language. Functions
can be assigned as constants, variables, placed as array elements and even set
as values of keys on an object. Most importantly, functions can be returned to
and from functions — just like any other data type! If you haven't been following
along, it's vitally important that you go back and do so. First-class functions are
one of JavaScript's most powerful features, but it takes some practice for them
to sink in.

## Resources

- [Wikipedia](https://en.wikipedia.org/wiki/First-class_function): [First-class function](https://en.wikipedia.org/wiki/First-class_function)
- [JavaScript is Sexy](http://javascriptissexy.com/understand-javascript-callback-functions-and-use-them/#more-1037): [Higher-order functions](http://javascriptissexy.com/understand-javascript-callback-functions-and-use-them/#more-1037)

<p class='util--hide'>View <a href='https://learn.co/lessons/javascript-first-class-functions'>First Class Functions</a> on Learn.co and start learning to code for free.</p>
