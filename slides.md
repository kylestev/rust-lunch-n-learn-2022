---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: "text-center"
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: true
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  enabled: true
  persist: false
  syncAll: true
---

# Rust

Waypoint Lunch n Learn (January 2022)

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080

---

# Why Rust?

- memory efficient
- incredibly fast
- no runtime or garbage collector
- integrates with other languages well because of the above constraints
- memory and thread safety give developers confidence in their code if it compiles
- excellent developer tools
- `crate` build system + package manager*

<!-- Crate is kind of weird. It is amazing at what it does, but maybe it should be two separate tools so other build systems or package managers could be swapped in -->

---

# Getting started

1. rustup (compiler+toolchain for rust. don't install any other way)
   - https://rustup.rs/
2. [rust-analyzer vscode extension](https://rust-analyzer.github.io/manual.html#vs-code)
   - weekly progress updates: https://rust-analyzer.github.io/thisweek
   - disable the default "Rust" extension distributed by Microsoft as it will cause conflicts
   - Ferrous Systems sponsors development

---

## Things I love about Rust

- the annoying compiler (best feature)
- the Borrow Checker
- the `enum` keyword
- `std`'s `Option` enum
- `std`'s `Result` enum

<!-- 

- [Option](https://doc.rust-lang.org/rust-by-example/std/option.html)
- [Result](https://doc.rust-lang.org/rust-by-example/std/result.html)

 -->

---

## Things I hate about Rust

_this slide intentionally left blank_

<!-- - the Borrow Checker -->

---

## code organization

- modules
  - let's look at a [real code example](https://github.dev/mejrs/rs3cache/blob/master/src/lib.rs)
  - https://doc.rust-lang.org/rust-by-example/mod.html
- functions
  - https://doc.rust-lang.org/rust-by-example/fn.html
- data structures
  - `struct`
    - https://doc.rust-lang.org/rust-by-example/custom_types/structs.html
  - `enum`
    - [the best enums](https://doc.rust-lang.org/rust-by-example/custom_types/enum.html) I have seen
- traits
  - https://doc.rust-lang.org/rust-by-example/trait.html

---

## variables

    * immutable by default
        * https://doc.rust-lang.org/rust-by-example/variable_bindings/mut.html
    * scoping and shadowing
        * https://doc.rust-lang.org/rust-by-example/variable_bindings/scope.html

---

### Control Flow: `match`

```rust {monaco}
fn main() {
  let number = 13;
  // TODO ^ Try different values for `number`

  println!("Tell me about {}", number);
  match number {
    1 => println!("One!"),
    // Match several values
    2 | 3 | 5 | 7 | 11 => println!("This is a prime"),
    // TODO ^ Try adding 13 to the list of prime values
    // Match an inclusive range
    13..=19 => println!("A teen"),
    // Handle the rest of cases
    _ => println!("Ain't special"),
  }

  let boolean = true;
  // Match is an expression too
  let binary = match boolean {
    // The arms of a match must cover all the possible values
    false => 0,
    true => 1,
  };

  println!("{} -> {}", boolean, binary);
}
```

<!-- https://doc.rust-lang.org/rust-by-example/flow_control/match.html -->

---

### Control Flow: `if let`

```rust {monaco}
fn main() {
    // All have type `Option<i32>`
    let number = Some(7);
    let emoticon: Option<i32> = None;

    // The `if let` construct reads: "if `let` destructures `number` into
    // `Some(i)`, evaluate the block (`{}`).
    if let Some(i) = number {
        println!("Matched {:?}!", i);
    }

    // Provide an altered failing condition.
    let i_like_letters = false;

    if let Some(i) = emoticon {
        println!("Matched {:?}!", i);
    // Destructure failed. Evaluate an `else if` condition to see if the
    // alternate failure branch should be taken:
    } else if i_like_letters {
        println!("Didn't match a number. Let's go with a letter!");
    } else {
        // The condition evaluated false. This branch is the default:
        println!("I don't like letters. Let's go with an emoticon :)!");
    }
}
```

---

<!--
Stuff we won’t get into today
-->

---

## other neat features

- macros!
  - https://doc.rust-lang.org/rust-by-example/macros.html

- testing
  - unit tests: https://doc.rust-lang.org/rust-by-example/testing/unit_testing.html
  - Doc tests: https://doc.rust-lang.org/rust-by-example/meta/doc.html

---

# Resources

## Rust by Example

RBE is the easiest way to get started. https://doc.rust-lang.org/rust-by-example/

## Books

1. "The Book" as it is known in the community is the best reference resource
   1. https://doc.rust-lang.org/book/
   2. or buy the eBook/physical versions from https://nostarch.com/Rust2018
2. I preferred the writing style and examples in O'Reilly's _Programming Rust, 2nd Edition_
