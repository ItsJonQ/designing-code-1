# Mutability

## const vs let

We should prefer `const` over `let` because `const` offers us some protections that with discipline can allow us to have immutable data.

Variables declared with `const` are not immutable, but they are not re-assignable. You see variables that are declared with `let` can be reassigned new values. For example, `let a = 2; a = 5; a = 'a';` This means that both the value and type of `a` can change over the execution of the program. If we instead declared `a` using the `const` keyword, reassigning the variable would be an error. This means that we can guarantee that the value of `a` will not change (if it is primitive type) and that the type of `a` will not change either. 

If `a` is an object, its value can change through mutation. The following code is perfectly legal, mutable and suprising.

```
const person = { name: 'Zim' }
person.name = 'Gir'
console.log(person) // { name: 'Gir' }

const people = ['Zim', 'Gir']
people.pop()
console.log(people) // ['Zim']
```

Using `const` is a good first step, but it will take additional discipline to write in a mutable style.

## Arrays

We should aim to achieve the following when performing operations on arrays.

1. Arrays are not modified
2. Operations on arrays always return new arrays

### Adding elements to arrays 

`Array.prototype.push` and `Array.prototype.unshift` are dangerous and should be avoided. Examine the following code sample to see why.

```javascript
const list = ['b', 'c']
list.push('d')    // 4
list.unshift('a') // 4
console.log(list) // ['a', 'b', 'c', 'd']
```

These array methods add to an array by mutating it in place. As a consequence, the value of the variable `list` changes throughout execution. Moreover, these methods return suprising results. The length of the array is returned instead of the array itself.

The `Array.prototype.concat` method is an immutable technique we can use that will not change the value of `list` and will return a new array which is the result of concatenating multiple arrays together, which is an intuitive result. Better yet, we can use the `spread` operator which has the same benefits, whilst offering additional expressiveness.

```javascript
const list = ['b', 'c']
const newList = ['a', ...list, 'd']
console.log(newList) // ['a', 'b', 'c', 'd']
console.log(list)    // ['b', 'c']
```

### Removing elements from arrays

`Array.prototype.pop`, `Array.prototype.shift`, and `Array.prototype.slice` are common but dangerous ways to remove elements from an array.

```javascript
const list = ['a', 'b', 'c', 'd']
list.pop()        // 'd'
list.shift(0)     // 'a'
list.slice(0, 1)  // ['b']
console.log(list) // ['c']
```

The value of `list` changes throughout execution, but what we should note here is how the returned result of each of these methods is quite surprising. Unlike their counterpart methods which returned the length of the array, these methods return the elements that were removed.

The mutable operations for removing elements from an array require us to know the index of the elements that we want to remove. While the techniques are brittle, they also lead us to write more code and increase the complexity of our programs. For example, should we need to find the index of the elements, we need to restort to writing imperative code to search for the index of the element.

In our quest to keep data immutable, we can adopt a functional technique for removing elements from an array that gives us more flexibility in how we target elements for removal. We can utilize `Array.prototype.filter` for this.

```javascript
const list = ['a', 'b', 'c', 'd']
const newList = list.filter((element, index) => {
  return index !== 0 && !['b', 'd'].includes(element)
})
console.log(newList) // ['c']
console.log(list)    // ['a', 'b', 'c', 'd']
```

## Replacing elements in an array

The gold standard mutable technique for replacing elements in an array is to use `Array.prototype.splice`. This confusing method has an arity of n. The first argument is the index of the first element you want to remove (and the index of where you want to start inserting), the second argument is the number of elements you want to remove, and the remaining n-2 arguments are the elements you want to insert. Confusing, right?

```javascript
const list = ['a', 'b', 'c', 'd']
list.splice(1, 2, 'y', 'z') // ['b', 'c']
console.log(list) // ['a', 'y', 'z', 'd']
```

We can use `Array.prototype.map` to leave the original `list` in tact and create a new `list` with the targeting items being replaced. As with `Array.prototype.filter`, we don't even need to know the index.

```javascript
const list = ['a', 'b', 'c', 'd']
const newList = list.map((element, index) => {
  if (index === 1) {
    return 'y'
  }
  if (element === 'c') {
    return 'z'
  }
  return element
})
console.log(list)    // ['a', 'b', 'c', 'd']
console.log(newList) // ['a', 'y', 'z', 'd']
```

## Objects

Coming soon.