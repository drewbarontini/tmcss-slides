Introduction
============

The name of this talk is "Thinking Modular CSS." We'll get into that in a moment, but I'd first like to talk about Dan Denney.

Musings about Dan Denney
------------------------

I'm fortunate enough that I get to work with Dan Denney. He is one of my favorite people on this planet. I'd also like to confirm that he is actually as nice as he seems. We've thrown some tough projects his way, and he doesn't even flinch. The perfect example of this is HTML emails. I'm sure everyone here knows how painful they are. This is the project we would pass to the new front-end developer. Instead of trudging through and moving on, what did Dan do? He made our HTML emails awesome, pushed the technology, and now wears the crown of "HTML King."

He's a saint, and everyone needs to know that.

I love this conference
----------------------

In all seriousness, I love this conference. I've only missed it once, and I look forward to it every year. The Denney family does a tremendous job, and I'm super pumped to be here, and to be speaking to all of you.

What is this talk about?
------------------------

So what am I hear to talk about? This talk is called, "Thinking Modular CSS". What does that mean?

I *really* want to explore the thought process behind building modular CSS systems. We've talked a lot about the "how" of things like object-oriented CSS, but we haven't really talked about the process that we take to get there.

It's something that we see with new front-end developers that we teach our system to. They understand how we structure things, what we call certain elements, but how we get there, the thought process, is the tough part to teach.

How is this going to work?
--------------------------

We'll define "modular CSS," talk about the process of crafting modular CSS, and then we'll go through a set of popular sites to actually apply this process and knowledge we've all gained.

Who am I?
---------

But first, I want to give you some information about me. As Mr. Denney said, I'm Drew Barontini.

What do I do?
-------------

I'm a front-end developer at Code School.

What is Code School?
--------------------

If you're not familiar with Code School, it is an online platform for teaching web technologies. We have interactive courses teaching technologies like Ruby on Rails, Sass, Git, Angular, iOS, and a lot of other languages and frameworks.

What am I responsible for?
--------------------------

### I maintain and lead the front-end for the .com

Our .com, codeschool.com, holds all of our courses, our users, our teams, and it allows them to track their progress and pick and choose which courses to take.

### Our course engine

I'm also responsible for our course engine, which is a separate entity from the .com, and it's what runs each course.

### Buildout of individual courses

In addition to that, I also oversee the buildout of individual courses, as well as keeping courses up-to-date.

The journey
-----------

What has been my journey into front-end development? This is a question that we ask all new hires because it's really interesting to see the various paths people have taken to the field, particularly into "front-end development."

### Band

For me, it all started when I was in a band back in High School and into College. Music is a creative field, obviously, but it was actually the abundance of design and web needs for the band that got me started.

### MySpace

MySpace was a really big thing for bands back in the day (not sure what it is now?), and we didn't have the money to pay a web designer to create a custom MySpace page, so I took a stab at it. Little did I know, I'd really find a passion in the horrid CSS I wrote for custom MySpace pages.

Side note: if anyone in here ever did custom MySpace pages, let's get together at some point and share a good cry. You will understand.

### T-shirts

Eventually, that evolved into more traditional illustration and graphic design, primarily for custom t-shirt and apparel designs. This was a really big component in the music world; custom t-shirt designs. There was a great community of designers that I learned a lot from.

However, I continued honing my HTML/CSS and JavaScript skills in college, and ultimately became interested in more advanced, traditional programming.

### Computer science

I took some computer science classes in college, and I became fascinated with programming.

### Front-end

The balance and blend of design and programming landed me right where I'm happy to be now, front-end development.

Front-end is now a specialization
---------------------------------

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

