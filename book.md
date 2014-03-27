# Thinking Modular CSS

## Summary

We've talked about the "how" of writing modular CSS, but we haven't truly
explored the "why." What is the thought process behind modular CSS? How do we
make the decisions that craft a flexible CSS architecture? How do we decide
when to create new components and modules, when to refactor, what goes where,
when something is something? We'll take a practical look at that thought
process by exploring popular sites and breaking them down into their various
components.

## Tagline

Learn the "why" of modular CSS by analyzing the decisions that craft a flexible
CSS architecture.

## 1. Introduction

### Musings about Dan Denney

### I love this conference

### What is this talk about?

### Why should everyone care?

### Who am I?

I'm Drew Barontini.

### What do I do?

I'm a front-end developer for Code School.

### What is Code School?

Code School is an online platform for teaching web technologies. We have
interactive courses teaching technologies like Ruby on Rails, Sass, Git,
Angular, and iOS.

### What am I responsible for?

I maintain and lead the front-end for the .com, our course engine, and oversee
buildout of individual courses and .com features.

### What about personal stuff?

When I'm not sitting at the computer, I like to exercise, watch TV and movies,
play with my two yellow labs, Maddox and Tank, and spend time with friends and
family. As you can most likely tell from my last name, I'm Italian. This means
that my entire family has an opinion on everything, no matter the subject.

### The journey

- Band
- MySpace
- T-shirts
- Computer science
- Front-end
- It's a specialization
- CSS is easy to write, hard to write well

### Understanding my personality

Last year, Nick Walsh, a fantastic front-end developer at Envy Labs, and myself
put on a workshop at this conference. For that, Dan made cartoons of us. In
order to understand how I am (my essence), I'll explain why I look like a
janitor. Story time: I'm very OCD. I like things very clean and organized. For
Christmas a few years ago, my Mom bought me a professional-grade back-pack
vacuum to keep my house clean. I'll say that one more time: My Mom, for
Christmas, bought me a professional-grade back-pack vacuum. I hope that
slightly conveys my insanity.

## 2. Front-end is now a specialization

- It's now a "thing," a "craft"

### "Front-end Developer & Designer"

I used to call myself a "front-end developer and designer." The "and designer"
bit has slowly faded away because of how happy I am to call myself a "front-end
developer." It's a specialization that is respected and (mostly) understood by
the industry.

### Developers respect us (mostly)

Developers used to trample over the HTML and CSS, largely qualifying their
actions as "HTML and CSS is so easy, any of us can write it." Although HTML and
CSS are easy to write, they aren't easy to write well. Writing quality,
semantic markup and modular CSS is a craft. Now that the "front-end
development" field has a more solid footing, developers understand the
complexity behind the simple HTML and CSS languages.

### Easy to write, hard to write well

HTML & CSS are easy to learn and write, but they are difficult to write *well*.

- We're building complex systems now
- Markup and styles working in unison
- Ability for styles to flex and work in different situations, environments

## 3. Define "Modular CSS"

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

These three pieces lead into some very important concepts behind modular CSS.

### Separation of Concerns

"Smaller parts" is really just talking about a separation of concerns:

> Separation of concerns is a design principle for separating a computer
   program into distinct sections, such that each section addresses a separate
   concern.

[Wikipedia](http://en.wikipedia.org/wiki/Separation_of_concerns)

Essentially, we want to make sure that each of our CSS modules (chunks of
styles) are only focusing on a single concern, or pattern. Breaking your CSS
down into smaller chunks will ultimately result in more maintainable code.

Let's say we wanted to manage our media elements throughout the site. We want
to have circle avatars, so we create a `thumb` module that handles this.

```css
.thumb {
  border-radius: 50%;
  display: block;
}
```

It's a very small file, but it's set up to allow us to create variants, and we
can use this module in conjunction with other modules to build our CSS
architecture. We'll look at this more later.

### Single Responsibility Principle

> The single responsibility principle states that every class should have a
   single responsibility, and that responsibility should be entirely
   encapsulated by the class. All its services should be narrowly aligned with
   that responsibility.

[Wikipedia](http://en.wikipedia.org/wiki/Single_responsibility_principle)

This is very similar to the "separation of concerns" concept, but the important
part here is that our CSS modules should be encapsulated; meaning, they
shouldn't directly affect one another.

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

Here we have a list module that simply handles text lists. It's only
responsibility is to take a list of text, stack the items, and provide a little
spacing to those items.

Let's say that we have a navigation `list` in a `header`, and we want to vertically align that `list` to the header. Rather than create a modification to our `list` module, we can let the `header` handle how its elements are positioned. The `list` module just handles the text list and associated items.

```css
.header-item {
  transform: translateY(-50%);
  position: relative;
  top: 50%;
}
```

Now, in our markup:

```html
<header class="header">
  <nav class="header-item">
    <ul class="list">
      <li class="list-item"><a href="/">Home</a></li>
      <li class="list-item"><a href="/about">About</a></li>
      <li class="list-item"><a href="/contact">Contact</a></li>
    </ul>
  </nav>
</header>
```

Our `list` module now remains encapsulated, and the `header` handles how the elements within are positioned.

**Positioning and layout are constant struggles with modular CSS. You'll have to abstract a lot of the layout styling to a more global component to keep your modules properly encapsulated.**

### Classes

This one seems to be more commonplace these days, but it's still worth
mentioning: **It's best to stick with only using classes, avoiding IDs altogether**.
IDs are too specific, and they'll cause you unnecessary headaches. Classes flatten the 
specificity of your elements to make sure your styles are applied properly without having
to fuss with specificity.

### Establish naming conventions

It doesn't matter as much what your naming conventions are, just that you have
them. Decided with your team (or yourself) what those should be, and make sure
to stick with the system, but be open to evolving it over time. At Code School
(and Envy Labs), we use MVCSS, which is a Sass-based CSS architecture that I
created with Nick Walsh, a front-end developer at Envy Labs. To give you a
sample of some naming conventions, I'll talk about how we do things:

#### camelCase & Hyphens

- `.list`
- `.tabList`
- `.list-item`
- `.tabList-item`

#### Modifiers

We use double-hyphens (`--`) to denote a modifier, which is just like the
modifier in BEM, if you’re familiar with that system. A modifier is an
alternate set of styling on a module. Say, for example, we have a button, and
that button has its basic styling. A modifier of a button would be an alternate
styling of that base button. For example:

```css
.btn {
  background: blue;
  color: white;
  display: inline-block;
  line-height: 2.5;
  padding: 0 1em;
}
```

Our base button. And now, our modifier:

```css
.btn--b {
  background: yellow;
  color: black;
}
```

Then, in our markup:

```html
<a href="#" class="btn">Button B</a>
<a href="#" class="btn btn--b">Button B</a>
```

#### States

States are generally used for hooks that are added and removed via JavaScript; things like, `is-active`, `is-hidden`, `is-editing`, etc.

```css
.dropdown.is-active {
  display: block;
}
```

#### Context

This is a very important concept that applies to the Single Responsibility
Principle’s "encapsulation" feature. Let's say that we have a `dropdown`
module, and when that `dropdown` is inside of a parent container, it needs to
have `position: relative` on that parent container to set the positioning
context. Rather than adding `position: relative` to that parent container, thus
breaking the "Single Responsibility Principle," because our modules are no
longer encapsulated (they are directly affecting one another), we can use a
"context" class to handle this for us:

```css
.has-dropdown {
  position: relative;
}
```

```html
<div class="container has-dropdown">
  <div class="dropdown">
    <! — … — >
  </div>
</div>
```

That's a brief look at the naming conventions and structure that our team uses,
and hopefully it's a useful example that you can work off of. We borrowed a lot
of ideas from great methodologies created by insanely smart people.

- OOCSS
- BEM
- Suit
- SMACSS

Make sure you look at all these methodologies, as one might fit your way of
working the best. They are also great starting points to building your own
system.

### Avoid nesting

This tenet applies specifically to CSS preprocessors, like Sass and LESS, that
allow you  to nest your selectors. This is important to talk about because of
the popularity and widespread use of CSS preprocessors. We use and love Sass,
but there are other great options out there to pick from.

Although nesting is an attractive feature, and one touted by most "Beginner's
Guide to Sass" tutorials out there, it's something you have to be very careful
with. We generally only nest things like `:hover`, `:focus`, `::before`,
`::after`, `:last-child`, etc.

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

### Patterns

The most important part of building a modular CSS architecture is to find the
patterns in your designs, and make sure that those are what you reuse and build
from to create your system. Think in terms of patterns rather than individual
elements of a design.

