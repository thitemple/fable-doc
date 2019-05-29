---
title: Overview and let
---

# Overview and `let`

F# is a statically typed language and as such it has some primitive types as we'll soon see. We can explicitly declare the type of a value (as we'll also see) but mostly we'll rely on the compiler to infer the types.

But everything starts with...

## The `let` keyword

`let` is the F# keyword used to bind any value to a name, it's used to bind the so called primitive types such as a `string` or an `integer`, to bind to a function or more complex structures such as arrays or records.

Here's how you can bind a string to an identifier named `x`:

```fsharp
let x = "some text"
```

The above snippet would be consider a constant in some other languages such as JavaScript. In F# there's no `var` or `const` there's only `let` and since in F# every value is immutable by default, that snippet is the equivalent of a constant.

Note that `let` in F# is different than `let` in JavaScript and this we'll be mentioned later on this page.

We're going to see more on functions later but here's how you can bind a function to an identifier named `add`:

```fsharp
let add x y =
    x + y
```

In the above snippet a function that adds two integers is being bound to an identifier named `add` and them two values are being bound to the identifiers `x` and `y`.

## Shadowing

In F#, bindings are immutable by default which means that normally one _can't_ reassign a value to a named binding, rather, if you try to do so using `let` what will happen is that you'll shadow an existing binding.

For instance, in the following example:

```fsharp
let x = "the answer"
let x = 42
```

In this case `x` is not being redefined nor its type is being changed from a `string` to an `int`, instead there are two different bindings with the same name `x` to different values. Of course, this example is not very useful because one binding is happening right after the other, but consider the following:

```fsharp
let printName name =
    let stripLastName name =
        if (String.exists (fun c -> c = ' ') name) then
            name.Split([|' '|]).[0]
        else
            name
    printfn "%s" name // Will print "John Doe"
    printfn "%s" (stripLastName name)

printName "John Doe" // Will print "John"
```

Don't worry too much if you don't fully grasp the above code, the main goal of that snippet is to demonstrate that the function `printName` expects an argument named `name` and in its body it defines another function `stripLastName` that also expects an argument `name`. Inside the scope of `stripLastName` the `name` argument is creating a new binding and thus shadowing the `name` argument received on the `printName` function. And that can be asserted by the two prints at the end of the `printName` function.

## Comparing with JavaScript

The main differences that the `let` keyword in F# has from the same keyword in JavaScript are:

- In JavaScript one would use `let` to define a named variable, an its value can be reassigned which is not the case in F#.
- In JavaScript `let` is scope bound, so one can declare a new variable with an already used name as long as it is in a different scope, in F# that can be done within the same scope.

### References

- [let Bindings](https://docs.microsoft.com/en-us/dotnet/fsharp/language-reference/functions/let-bindings)
