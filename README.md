# Using Object.assign

## Learning Goals

- Identify `Object.assign`
- Non-destructively assign new data with `Object.assign()`

## Introduction

In JavaScript, we have access to a global `Object` that comes with several
helpful methods ready for us to use. One of these methods is `Object.assign()`,
which allows us to combine properties from multiple `Object`s into a single
`Object`. In this lab, we're going to learn how to use `Object.assign` to do
just that.

## Identify `Object.assign()`

The first argument passed to `Object.assign()` is the first `Object` into which
all of the properties are merged. Every additional argument is an `Object` whose
properties we want to merge into the first `Object`:

```js
Object.assign(firstObject, secondObject, thirdObject, ...);
```

The return value of `Object.assign()` is the first `Object` after all of the
additional `Object`s' properties have been merged in:

```js
Object.assign({ eggs: 3 }, { flour: '1 cup' });
// => { eggs: 3, flour: "1 cup" }

Object.assign({ eggs: 3 }, { chocolateChips: '1 cup', flour: '2 cups' }, { flour: '1/2 cup' });
// { eggs: 3, chocolateChips: "1 cup", flour: "1/2 cup" }
```

Let's look at the `flour` property in the above example. **If multiple
`Object`s have a property with the same key, the last key to be defined wins
out**. Essentially, the last call to `Object.assign()` in the above snippet is
wrapping all of the following assignments into a single line of code:

```js
const recipe = { eggs: 3 };

recipe.chocolateChips = '1 cup';

recipe.flour = '2 cups';

recipe.flour = '1/2 cup';
```

## Non-Destructively Assign New Data with `Object.assign()`

A common pattern for `Object.assign()` is to provide an empty `Object` as the
first argument. That way we're providing an entirely new `Object` instead of
modifying or overwriting the properties of an existing `Object`. This pattern
allows us to rewrite the above `destructivelyUpdateObject()` function in a
non-destructive way:

```js
function nondestructivelyUpdateObject(obj, key, value) {
  return Object.assign({}, obj, { [key]: value });
}

const recipe = { eggs: 3 };

const newRecipe = nondestructivelyUpdateObject(recipe, 'chocolate', '1 cup');
// => { eggs: 3, chocolate: "1 cup" }

newRecipe;
// => { eggs: 3, chocolate: "1 cup" }

recipe;
// => { eggs: 3 }
```

It's important that we merge everything into a new, empty `Object`. Otherwise,
we would be modifying the original `Object`. In your browser's console, test
what happens if the body of the above function were `return Object.assign(obj, {
[key]: value });`. Uh oh, back to being destructive! Fortunately, we can avoid
that by following the example above.

## Conclusion

Depending on how you need to use it, `Object.assign` can be useful in both
destructive and non-destructive ways. Play around with it in your console. What
happens when you use different data types while combining objects? The results
might surprise you! 

## Resources

- [Object.assign at Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)
