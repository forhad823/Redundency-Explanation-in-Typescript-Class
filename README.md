# Redundency-Explanation-in-Typescript-Class
```ts
class Book {
  name: string;
  book: string;
  constructor(name: string, book: string) {
    this.name = name;
    this.book = book;
  }
}
```
This feels redundant at first because you are seeing the **same words repeated in 3 different roles**.

The repetition exists because each occurrence has a **different job**.

---

# 1. Class Properties

```ts
name: string;
book: string;
```

These lines tell TypeScript:

> "Every object created from this class will contain these properties."

So this defines the **shape of the object**.

Without this:

```ts
class Book {}
```

TypeScript would not know that `name` or `book` exist.

---

# 2. Constructor Parameters

```ts
constructor(name: string, book: string)
```

These are **inputs**.

They are temporary variables that exist only during object creation.

Example:

```ts
new Book("Harry", "JS Guide")
```

Here:

* `"Harry"` goes into constructor parameter `name`
* `"JS Guide"` goes into constructor parameter `book`

But constructor parameters disappear after construction finishes.

So they are NOT automatically stored in the object.

---

# 3. Assigning to the Object

```ts
this.name = name;
this.book = book;
```

This means:

> "Take the constructor input and store it inside the object itself."

* Left side:

```ts
this.name
```

means:

> property inside the object

* Right side:

```ts
name
```

means:

> temporary constructor parameter

So this line copies data from the constructor parameter into the object property.

---

# Real-Life Analogy

Imagine a hotel form.

---

## Step 1 — Hotel structure

```ts
name: string;
```

Means:

> Every guest record must have a name field.

---

## Step 2 — Customer gives info

```ts
constructor(name: string)
```

Means:

> A customer tells the receptionist their name.

---

## Step 3 — Receptionist stores it

```ts
this.name = name;
```

Means:

> Store the customer's name into the hotel database.

---

# Why JavaScript Was Designed This Way

Because JavaScript originally separated:

* object properties
* function parameters

They are fundamentally different things.

A constructor is just a function.

This:

```ts
constructor(name: string)
```

does NOT automatically mean:

```ts
this.name
```

JavaScript keeps them separate unless you explicitly assign.

That gives developers more control.

Example:

```ts
constructor(name: string) {
  this.name = name.toUpperCase();
}
```

or:

```ts
constructor(name: string) {
  if (name.length > 0) {
    this.name = name;
  }
}
```

So the assignment step allows validation, transformation, filtering, etc.

---

# Modern TypeScript Shortcut

TypeScript later introduced a shorthand to reduce redundancy:

```ts
class Book {
  constructor(
    public name: string,
    public book: string
  ) {}
}
```

This single line automatically:

* creates properties
* creates constructor parameters
* assigns values

So these 3 things:

```ts
name: string;
constructor(name: string) {
  this.name = name;
}
```

become just:

```ts
constructor(public name: string)
```

This is called a **parameter property** in TypeScript.

---

# What Actually Happens Internally

This:

```ts
constructor(public name: string)
```

is roughly converted internally into:

```ts
name: string;

constructor(name: string) {
  this.name = name;
}
```

So the redundancy is mostly for:

* clarity
* separation of responsibilities
* flexibility
* compatibility with JavaScript design principles

TypeScript simply added syntax sugar later to make it shorter.
