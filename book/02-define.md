Define
======

Before we dig into the thinking behind modular CSS, it's important to define
it, and talk about the tenets of modular CSS.

First off, let's talk about the definition of it:

>  Modular design is an approach that subdivides a system into smaller parts
    that can be independently created and then used in different systems to
    drive multiple functionalities.

[Wikipedia](http://en.wikipedia.org/wiki/Modular_design)

I heard three important pieces in that definition:

1. Smaller parts
2. Independently created
3. Used in different systems

Your CSS should be:

- Broken down into smaller parts, smaller chunks of styles
- Independently created, so you're modules can be properly encapsulated
- Have the ability to be ported from system to system with minor modifications

Single Responsibility Principle
-------------------------------

Those concepts are present in the "Single Responsibility Principle," which is something that I always try to adhere to.

> The single responsibility principle states that every class should have a
   single responsibility, and that responsibility should be entirely
   encapsulated by the class. All its services should be narrowly aligned with
   that responsibility.

[Wikipedia](http://en.wikipedia.org/wiki/Single_responsibility_principle)

### Single Responsibility

Firstly, our CSS modules should only have one responsibility. It's helpful, when creating your modules, to add a comment block at the top of the file that explains, in one sentence, what that module does; what is its responsibility.

```sass
// *************************************
//
//   List
//   -> Text lists
//
// *************************************
```

This comment block is using Sass, but the same idea applies to vanilla CSS. Now, we know what our module is responsible for, so we can go ahead and build it.

```css
.list {
  list-style-type: none;
  margin: 0;
  padding: 0;
}

.list-item {
  display: block;
  margin-bottom: 1em;
}
.list-item:last-child {
  margin-bottom: 0;
}
```

Here we have the list module that handles text lists. Its only responsibility is to take a list of text, stack the items, and provide a little spacing to those items.

### Encapsulation

Secondly, our CSS modules should be encapsulated; meaning, they shouldn't directly affect one another.

```html
<header class="header">
  <nav class="nav">
    <!--- ... --->
  </nav>
</header>
```

Let's say that we have a navigation (`nav`) in a `header`, and we want to float the `nav` to the right.

```css
.nav {
  float: right;
}
```

What if we don't want every `.nav` to be floated to the right? What if we have a sub-navigation that is going to be on the left side?

```css
.header .nav {
  float: right;
}
```

This works, but the problem here is that our `.header` module is telling our `.nav` module what to do. It's not adhering to the idea of encapsulation. Instead, we can let the `header` handle how its elements are positioned:

```css
.header-nav {
  float: right;
}
```

Now, in our markup:

```html
<header class="header">
  <nav class="header-nav nav">
    <!--- ... --->
  </nav>
</header>
```

Our `nav` module now remains encapsulated, and the `header` handles how its elements are positioned without talking to another module.

We can make this better by abstracting out a `float` utility class.

```css
.fr {
  float: right;
}
```

```html
<header class="header">
  <nav class="nav fr">
    <!--- ... --->
  </nav>
</header>
```

Now we've abstracted out the positioning of the `.nav`, so as to keep things encapsulated. 

*Ultimately, you should have a `grid` module that handles the layout, but this illustrates the idea of encapsulation.*

**Positioning and layout are constant struggles with modular CSS. You'll have to abstract a lot of the layout styling to a more global component to keep your modules properly encapsulated.**

Classes
-------

Now let's look at some more practical applications of "Modular CSS."

This one seems to be more commonplace these days, but it's still worth
mentioning: **It's best to stick with only using classes, avoiding IDs altogether**. IDs are too specific, and they'll cause you unnecessary headaches. Classes flatten the specificity of your elements to make sure your styles are applied properly without having to fuss with specificity.

Establish naming conventions
----------------------------

It doesn't matter as much what your naming conventions are, just that you have
them. Decide with your team (or yourself) what those should be, and make sure to stick with the system, but be open to evolving it over time. 

Nick Walsh, a front-end developer at Envy Labs, had this great quote that we always reference when we talk about how we write our CSS.

> This is how it is now, until we change it.
- Nick Walsh

It's very true. We constantly evaluate and evolve the system as we work on new projects, but that's what makes the system better: constant evaluation.

At Code School (and Envy Labs), we use MVCSS, which is a Sass-based CSS architecture that I created with Nick. To give you a sample of some naming conventions, I'll talk about how we do things.

*This is by no way preaching our method. This is merely an example that can help guide you to establishing your own naming conventions.*

### camelCase & Hyphens

- `.list`
- `.tabList`
- `.list-item`
- `.tabList-item`

We use camelCase for multiple words, and we use a hyphen to separate a module from a submodule.

**Note**: For filenames, use the same naming convention: (e.g. `_list.sass`, `.tabList.sass`)

### Modifiers

> A modifier is an alternate set of styling on a module.

We use double-hyphens (`--`) to denote a modifier. Say, for example, we have these two buttons. The button on the left is our base button, and the button on the right is an alternate button. A modifier of a button would be an alternate styling of that base button. For example:

```css
.btn {
  background: blue;
  color: white;
  display: inline-block;
  line-height: 2.5;
  padding: 0 1em;
}
```

Our base button styles. And now, our modifier:

```css
.btn--b {
  background: yellow;
  color: black;
}
```

So now we have defined our button modifier. Then, in our markup:

```html
<a href="#" class="btn">Button</a>
<a href="#" class="btn btn--b">Button B</a>
```

### States

States are generally used for hooks that are added conditionally via JavaScript; things like, `is-active`, `is-hidden`, `is-editing`, etc.

```css
.dropdown {
  display: none;
 }
 
.dropdown.is-active {
  display: block;
}
```

So, for example, we have this `.dropdown` that is hidden by default, and is shown when the `.is-active` state class is added.

### Context

This is a very important concept that applies to the Single Responsibility Principle’s "encapsulation" idea. Let's say that we have a `dropdown` module, and when that `dropdown` is inside of a parent container, it needs to have `position: relative` on that parent container to set the positioning context. Rather than adding `position: relative` to that parent container, thus breaking the "Single Responsibility Principle," because our modules are no longer encapsulated (they are directly affecting one another), we can use a "context" class to handle this for us:

```css
.has-dropdown {
  position: relative;
}
```

We define a context class using `.has-` as the prefix. Then, in our markup:

```html
<div class="container has-dropdown">
  <div class="dropdown">
    <!-- ... -->
  </div>
</div>
```

The `.container` doesn't need to know what's in it by altering its styles to accommodate the `.dropdown`. Instead, the `.dropdown` says, "Hey! I'm here, deal with it."

That's a brief look at the naming conventions and structure that our team uses, and hopefully it's a useful example that you can work off of. We borrowed a lot of ideas from great methodologies created by insanely smart people. Things like:

- OOCSS
- BEM
- Suit
- SMACSS

Make sure you look at all these methodologies, as one might fit your way of working the best. They are also great starting points to building your own system.

Limit nesting
-------------

This tenet applies specifically to CSS preprocessors, like Sass and LESS, that allow you  to nest your selectors. This is important to talk about because of the popularity and widespread use of CSS preprocessors.

*We use and love Sass,  but there are other great options out there to pick from.*

Although nesting is an attractive feature, and one touted by most "Beginner's Guide to Sass" tutorials out there, it's something you have to be very careful with.

When I used Sass for the first time on a project, I nested *everything* inside of `section.content`. It was an absolute nightmare.

```scss
section.content {
  .header {
    // ...
  }
  .main {
    // ...
  }
  .footer {
    // ...
  }
}
```

Now, we don't nest much, and when we do, it's not many levels deep.

- Example of proper Sass

We generally only nest things like `:hover`, `:focus`, `::before`, `::after`, `:last-child`, etc.

```sass
.btn
  background: blue
  color: white
  display: inline-block
  line-height: 2.5
  padding: 0 1em
  &:hover,
  &:focus
    background: green
```

Avoid "magic numbers"
---------------------

What am I talking about when I say "magic numbers"?

```css
.element {
  position: relative;
  top: -2px;
}
```

You know what this is. We all do it. These "magic numbers" are best to avoid whenever possible. You want your styles to predictable and flexible, and these "magic numbers" break that. However, when you do use them, which is sometimes unavoidable, make sure to document it.

```css
.element {
  position: relative;
  top: -2px; /* FIXME: Magic number! */
}
```

Now I have a way to search across the project and find the magic numbers whenever I do a refactor.

Abstract layout and positioning
-------------------------------

In addition to magic numbers, layout and positioning in CSS can cause you a lot of headaches when trying to keep your styles flexible. Let's look at an example.

```css
.nav {
  float: right;
  width: 50%;
}
```

This is all well and good until we have a second `.nav` block that needs to be positioned to the left, or  even centered. Ask yourself, why is this navigation block being positioned to the right at `50%`? Is it because it's in another module? Well, you'll want to use a higher-up layout module to handle this (e.g. a grid).

```html
<div class="grid">
  <div class="grid-box grid-box--1of2">
    <!--- ... --->
  </div>
  <div class="grid-box grid-box--1of2">
    <nav class="nav">
      <!--- ... --->
    </nav>
  </div>
</div>
```

This is an example of the grid we use, but the concept of a grid handing the structure is what's important here.The individual module doesn't need to control its layout; it should flex and fit in any container.

