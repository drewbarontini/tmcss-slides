Thinking Modular CSS
====================

Summary
-------

We've talked about the "how" of writing modular CSS, but we haven't truly
explored the "why." What is the thought process behind modular CSS? How do we make the decisions that craft a flexible CSS architecture? How do we decide when to create new components and modules, when to refactor, what goes where, when something is something? We'll take a practical look at that thought process by exploring popular sites and breaking them down into their various components.

Tagline
-------

Learn the "why" of modular CSS by analyzing the decisions that craft a flexible
CSS architecture.

1. Introduction
---------------

The name of this talk is "Thinking Modular CSS." We'll get into that in a moment, but I'd first like to talk about Dan Denney.

### Musings about Dan Denney

I'm fortunate enough that I get to work with Dan Denney. He is one of my favorite people on this planet. I'd also like to confirm that he is actually as nice as he seems. We've thrown some tough projects his way, and he doesn't even flinch. The perfect example of this is HTML emails. I'm sure everyone here knows how painful they are. This is the project we would pass to the new front-end developer. Instead of trudging through and moving on, what did Dan do? He made our HTML emails awesome, pushed the technology, and now wears the crown of "HTML King."

He's a saint, and everyone needs to know that.

### I love this conference

In all seriousness, I love this conference. I've only missed it once, and I look forward to it every year. The Denney family does a tremendous job, and I'm super pumped to be here, and to be speaking to all of you.

### What is this talk about?

So what am I hear to talk about? This talk is called, "Thinking Modular CSS". What does that mean?

I *really* want to explore the thought process behind building modular CSS systems. We've talked a lot about the "how" of things like object-oriented CSS, but we haven't really talked about the process that we take to get there.

It's something that we see with new front-end developers that we teach our system to. They understand how we structure things, what we call certain elements, but how we get there, the thought process, is the tough part to teach.

### How is this going to work?

We'll define "modular CSS," talk about the process of crafting modular CSS, and then we'll go through a set of popular sites to actually apply this process and knowledge we've all gained.

### Who am I?

But first, I want to give you some information about me. As Mr. Denney said, I'm Drew Barontini.

### What do I do?

I'm a front-end developer at Code School.

### What is Code School?

If you're not familiar with Code School, it is an online platform for teaching web technologies. We have interactive courses teaching technologies like Ruby on Rails, Sass, Git, Angular, iOS, and a lot of other languages and frameworks.

### What am I responsible for?

#### I maintain and lead the front-end for the .com

Our .com, codeschool.com, holds all of our courses, our users, our teams, and it allows them to track their progress and pick and choose which courses to take.

#### Our course engine

I'm also responsible for our course engine, which is a separate entity from the .com, and it's what runs each course.

#### Buildout of individual courses

In addition to that, I also oversee the buildout of individual courses, as well as keeping courses up-to-date.

### The journey

What has been my journey into front-end development? This is a question that we ask all new hires because it's really interesting to see the various paths people have taken to the field, particularly into "front-end development."

#### Band

For me, it all started when I was in a band back in High School and into College. Music is a creative field, obviously, but it was actually the abundance of design and web needs for the band that got me started.

#### MySpace

MySpace was a really big thing for bands back in the day (not sure what it is now?), and we didn't have the money to pay a web designer to create a custom MySpace page, so I took a stab at it. Little did I know, I'd really find a passion in the horrid CSS I wrote for custom MySpace pages.

Side note: if anyone in here ever did custom MySpace pages, let's get together at some point and share a good cry. You will understand.

#### T-shirts

Eventually, that evolved into more traditional illustration and graphic design, primarily for custom t-shirt and apparel designs. This was a really big component in the music world; custom t-shirt designs. There was a great community of designers that I learned a lot from.

However, I continued honing my HTML/CSS and JavaScript skills in college, and ultimately became interested in more advanced, traditional programming.

#### Computer science

I took some computer science classes in college, and I became fascinated with programming.

#### Front-end

The balance and blend of design and programming landed me right where I'm happy to be now, front-end development.

2. Front-end is now a specialization
------------------------------------

"Front-end Development" truly is a specialization; it's a craft, and it's not easy. It's not just for designers who code or developers who write HTML & CSS. It's a area of focus for unique individuals with particular skill sets. I'm proud to call myself a "front-end developer."

### "Front-end Developer & Designer"

For a long time, though, I called myself a "front-end developer and designer." The "and designer" bit slowly faded away because of how happy I am to call myself a "front-end developer." It's a specialization that is respected and (mostly) understood by the industry.

### Developers respect us (mostly)

Developers used to trample over the HTML and CSS, largely qualifying their actions as "HTML and CSS is so easy, any of us can write it." Although HTML and CSS are easy to write, they aren't easy to write well. Writing quality, semantic markup and modular CSS is a craft. Preprocessors like Sass and LESS now add a more programmatic layer of abstraction to our CSS, which is more easily understood by developers.

Now that the "front-end development" field has a more solid footing, developers understand the complexity behind the simple HTML and CSS languages that we write.

### Easy to write, hard to write well

Like I said, HTML & CSS are easy to learn and write, but they are difficult to write *well*.

#### We're building complex systems now

Our styles are built out on large-scale applications that need to be performant and easily understood by a large team.

#### Ability for styles to flex and work in different situations, environments

Our styles need to be flexible so that we can add new features and pages, as well as have a solid foundation for each new site or application that we build.

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

Your CSS should be:

- Broken down into smaller parts, smaller chunks of styles
- Independently created, so you're modules can be properly encapsulated
- Have the ability to be ported from system to system with minor modifications

### Single Responsibility Principle

Those concepts are present in the "Single Responsibility Principle," which is something that I always try to adhere to.

> The single responsibility principle states that every class should have a
   single responsibility, and that responsibility should be entirely
   encapsulated by the class. All its services should be narrowly aligned with
   that responsibility.

[Wikipedia](http://en.wikipedia.org/wiki/Single_responsibility_principle)

#### Single Responsibility

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

#### Encapsulation

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

### Classes

Now let's look at some more practical applications of "Modular CSS."

This one seems to be more commonplace these days, but it's still worth
mentioning: **It's best to stick with only using classes, avoiding IDs altogether**. IDs are too specific, and they'll cause you unnecessary headaches. Classes flatten the specificity of your elements to make sure your styles are applied properly without having to fuss with specificity.

### Establish naming conventions

It doesn't matter as much what your naming conventions are, just that you have
them. Decide with your team (or yourself) what those should be, and make sure to stick with the system, but be open to evolving it over time. 

Nick Walsh, a front-end developer at Envy Labs, had this great quote that we always reference when we talk about how we write our CSS.

> This is how it is now, until we change it.
- Nick Walsh

It's very true. We constantly evaluate and evolve the system as we work on new projects, but that's what makes the system better: constant evaluation.

At Code School (and Envy Labs), we use MVCSS, which is a Sass-based CSS architecture that I created with Nick. To give you a sample of some naming conventions, I'll talk about how we do things.

*This is by no way preaching our method. This is merely an example that can help guide you to establishing your own naming conventions.*

#### camelCase & Hyphens

- `.list`
- `.tabList`
- `.list-item`
- `.tabList-item`

We use camelCase for multiple words, and we use a hyphen to separate a module from a submodule.

**Note**: For filenames, use the same naming convention: (e.g. `_list.sass`, `.tabList.sass`)

#### Modifiers

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

#### States

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

#### Context

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

### Limit nesting

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

### Avoid "magic numbers"

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

### Abstract layout and positioning

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

4. Exploring the "why"
----------------------

To make sense of the "why," the thought process behind building a modular CSS architecture, it's important to establish a process by which you can craft your styles, and constantly evaluate the system. I like to break it down into five simple steps.

1. Identify
2. Define
3. Build
4. Combine
5. Refine

### 1. Identify

Obviously the first step is to identify the patterns that you'll start with when building your modules.

#### Structure, layout (highest level)

I like to start at the highest level: the structure and layout elements. These tend to be the most reusable elements project to project.

**Example**: (`.bucket`, `.cell`, `.grid`, `.row`)

#### Common patterns (known)

Next, look for the common patterns that you continually encounter and build for each project.

**Example**: (`.card`, `.dropdown`, `.list`, `.nav`)

#### Unique patterns (unknown)

Finally, find the more unique patterns. Do you notice very specific style pattterns?

**Example**

#### Front-end Audit 

[https://github.com/drewbarontini/front-end-audit/](https://github.com/drewbarontini/front-end-audit/)

To help you document these, you can use what I call the "Front-end Audit." It's simply a document that you can use to outline and explain all of the components of your front-end architecture.

- Info
- Browser Support
- Features
- Tools
- Icons
- CSS Architecture
- Notes & Ideas
- Issues
- Log

### 2. Define

#### Responsibility

#### Name

### 3. Build

- Write the module

### 4. Combine

- Separate, encapsulated modules working together

### 5. Refine

- Refactor

5. Examples
-----------

### Dribbble

[http://dribbble.com/](http://dribbble.com/)

### Instagram

[http://instagram.com/](http://instagram.com/)

### GitHub

[http://github.com/](http://github.com/)
