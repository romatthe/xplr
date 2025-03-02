# Sum Type

> This section isn't specific to xplr. However, since xplr configuration makes
> heavy use of this particular data type, even though it isn't available in
> most of the mainstream programming languages (yet), making it a wild or
> unfamiliar concept for many, it's worth doing a quick introduction here.
>
> If you're already familiar with [Sum Type / Tagged Union][1] (e.g. Rust's
> enum), you can skip ahead.

While reading this doc, you'll come across some data types like [Layout][2],
[Color][4], [Message][3] etc. that says something like "x is a sum type that
can be any of the following", and then you'll see a list of strings and/or lua
tables just below.

Yes, they are actually sum types, i.e. they can be any of the given set of
tagged variants listed there.

Notice the word "be". Unlike classes or structs (aka product types), they can't
"have" values, they can only "be" the value, or rather, be one of the possible
set of values.

Also notice the word "tagged". Unlike the single variant `null`, or the dual
variant `boolean` types, the variants of sum types are tagged (i.e. named), and
may further have, or be, value or values of any data type.

A simple example of a sum type is an enum. Many programming languages have
them, but only a few modern programming languages allow nesting other types
into a sum type.

```rust
enum Result {
    Ok,
    Err,
}
```

Here, `Result` can be one of two possible set of values: `Ok` and `Err`, just
like `boolean`, but unlike `boolean`, being tagged allows `Result` to have more
than two variants if required, by changing the definition.

e.g.

```rust
enum Result {
    Ok,
    Err,
    Pending,
}
```

We'd document it here as:

> Result is a sum type that can be one of the following:
>
> - "Ok"
> - "Err"
> - "Pending"

But some languages (like Rust, Haskell, Elm etc.) go even further, allowing us
to associate each branch of the enum with further nested types like:

```rust
enum Result {
    Ok(bool),
    Err(Error),
    Pending,
}
```

Here, as we can see, unlike the first example, some of `Result`'s possible
variants can have further nested types associated with them. Note that `Error`
here can be either a sum type (e.g. enum), or a product type (e.g.
class/struct), but whatever it is, it will only exist when `Result` is `Err`.

We'd document it here as:

> Result is a sum type that can be one of the following:
>
> - { Ok = bool }
> - { Err = Error }
> - "Pending"

And then we'd go on documenting whatever `Error` is.

So, there you go. This is exactly what sum types are - glorified enums that can
have nested types in each branch.

---

If you're still confused about something, or if you found an error in this
explaination, feel free to [discuss together][5].

[1]: https://en.wikipedia.org/wiki/Tagged_union
[2]: layout.md
[3]: message.md
[4]: style.md#color
[5]: community.md
