Process
=======

To make sense of the "why," the thought process behind building a modular CSS architecture, it's important to establish a process by which you can craft your styles, and constantly evaluate the system. I like to break it down into five simple steps.

1. Identify
2. Define
3. Build
4. Combine
5. Refine

---

1. Identify
-----------

Obviously the first step is to identify the patterns that you'll start with when building your modules.

### Structure, layout (highest level)

I like to start at the highest level: the structure and layout elements. These tend to be the most reusable elements project to project.

**Example**: (`.bucket`, `.cell`, `.grid`, `.row`)

### Common patterns (known)

Next, look for the common patterns that you continually encounter and build for each project.

**Example**: (`.card`, `.dropdown`, `.list`, `.nav`)

### Unique patterns (unknown)

Finally, find the more unique patterns. Do you notice very specific style pattterns?

**Example**

### Front-end Audit

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

---

2. Define
---------

### Responsibility

### Name

3. Build
--------

- Write the module

4. Combine
----------

- Separate, encapsulated modules working together

5. Refine
---------

- Refactor

