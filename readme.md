<img src="/images/logo.svg" width="320" height="auto" alt="syntacss logo, by Guava" />

***

Syntacss is a method to create and extend CSS systems. It aims to facilitate the process of **organizing** styles, **naming** classes and **formatting** code. It features a structure that embraces the power of cascade while works towards modularity.

Using its principles, you should get a powerful architecture tailored for modularity and a natural language syntax that results in understandable classes. No matter how simple or complex the project is, Syntacss helps you get things done _right_.

It drinks from a lot of great ideas. Picture it as a simplified version of [Atomic Design](http://atomicdesign.bradfrost.com/) architecture and metaphor; as having the intuitive syntax of [Semantic UI](http://semantic-ui.com/); as a system that embraces principles and concepts of [SMACSS](https://smacss.com/), and [OOCSS](https://www.smashingmagazine.com/2011/12/an-introduction-to-object-oriented-css-oocss/)—all of that being compliant with [mdo's Code Guide](http://codeguide.co/) standards.


# Organizing
<img src="/images/structure.svg" width="360" height="164" alt="Illustration of Syntacss architecture, composed of three layers: core blocks, modules and pages" />

The architecture is made of three stylesheets layers that, together, compose the design system.

### Core blocks
<img src="/images/core-blocks.svg" width="42" height="35" alt="Core block icon by jon trillana from the Noun Project" />

The first layer, **core blocks**, contains the small foundational UI building pieces; they are a set of pre determined ingredients that will be used in the following levels, as well as define the base HTML styles.

Block | What it usually contains | _Identifier class*_
----- | ------------------------ | ----------------
`mixins`     | Utility mixins & functions used throughout files | -
`scale`      | Modular scale & measurements | –
`colors`     | Color pallette variables & color classes | `.color`
`typography` | Type scale, families, headers, paragraphs, links, lists, small, etc | `.typography` or `.type`
`inputs`     | Text inputs, labels, selects, checkboxes, etc | `.input`
`buttons`    | All sorts of buttons: default, primary, secondary, etc | `.button`
`tables`     | Tabular data and table layouting | `.table`
`globals`    | Global HTML & _modifier classes_ | –

*_Use _identifier classes_ on _core blocks_ only when needed. For example, if the project doesn't have different types of tables, then a base `table` HTML should be enough._

### Modules
<img src="/images/modules.svg" width="68" height="38" alt="Module icon" />

The second layer, **modules**, are UI patterns that can easily be reused throughout the design system. They are formed by groups of _core blocks_ functioning together as a unit. 

For example, a `dropdown` module might contain `icons`, `typography`, and `buttons` _core blocks_; a navigation bar may have `typography`, `inputs`, `buttons`, and even other _modules_ as well, like the `dropdown` mentioned above. PS: Almost everything regarding design system has a typography _core block_.

Unlike the _core blocks_, _modules_ aren't pre determined—they may change according to each project's needs. You should create new modules as they make sense to the design system.

When a _module_ has other _modules_ as children elements, it should define how the nested _modules_ are laid out, but shouldn't style them—for example, a `sidebar` _module_ that has a `tab` _module_ may lay out where the `tabs` are within the `sidebar`, but not how they should look.

### Pages
<img src="/images/pages.svg" width="68" height="38" alt="Pages icon" />

The third layer, **pages**, encompass specific styles for pages and themes. It also can be useful to tie a group of _modules_ together, forming a cohesive layout. On smaller projects, this layer can be useful to tie _core blocks_ together without worrying too much about modularity.


# Naming
Naming things in Syntacss is quite simple. First, name a class after the _core block_/_module_/_page_'s title. This will be called _identifier_ class. Then, add one or more classes that describe a characteristic of the element you're working on (how it looks like? what's its purpose?). These attributes are called _modifiers_ classes.

Take this _core block_ `.button` as an example.
```HTML
<button class="small rounded primary button"></button>
```
Here, this element has the `.button` _identifier_ class that defines what it is, and other _modifiers_ classes that tell how it looks like (`.small` and `.rounded`), and what's its role inside the design system (`.primary`). All of its styles are within `buttons.scss` file. In this case, `.button.small` may have sizing styles, `.button.rounded` border radius tweaks, and `.button.primary` a color theme for principal actions.

Another example: a `.sidebar.module`.
```HTML
<aside class="sidebar module">            <!-- module wrapper -->
  <a class="sidebar logo" href="…">       <!-- module element -->
    <img src="…" alt="…">
  </a>
  <a class="sidebar link" href="…">       <!-- core `a` + module element -->
    <span class="discover icon"></span>   <!-- core block -->
    Discover
  </a>
</aside>
```
The `.sidebar.module` above has an _identifier_ class (`.sidebar`) that is grouped with other _modifiers_ classes (`.sidebar.module` is the main wrapper; `.sidebar.logo` is a sidebar's piece). It also contains _core blocks_ like `a` and `.icon`. All of its styles are within `sidebars.scss` file.

A more complex example: a `.navigation.module`.
```HTML
<nav class="navigation module">           <!-- module wrapper -->
  <a class="navigation logo" href="…">    <!-- module element -->
    <img src="…" alt="…">
  </a>
  <a class="navigation link" href="…">    <!-- core `a` + module element -->
    <span class="discover icon"></span>   <!-- core block -->
    Discover
  </a>
  <button class="toggle button" href="…"> <!-- core block -->
    <span class="profile icon"></span>    <!-- core block -->
    Profile
  </button>
  <ul class="dropdown module">            <!-- other module -->
    <li class="dropdown item">            <!-- other module's element -->
      <a href="…">
        Edit profile
      </a>
    </li>
  </ul>
</nav>
```

Summing up: an _identifier_ class (_core block_, _module_, or _page_'s titles) plus _modifiers_ classes forms the naming scheme of an element. 

One last note about _modifiers_ classes: they can be either named after its structure (defining _how things are laid out_) or its appearance/semantic meaning (indicating _how things look like_ or _what purpose things have_).
* Examples of structure modifiers: `.sidebar.wrapper`, `.sidebar.container`, `.sidebar.row`, etc.
* Examples of appearance modifiers: `.button.big`, `.button.small`, `.button.rounded`, etc.
* Examples of semantic modifiers: `.button.active`, `.button.primary`, `.button.loading`, etc.

### Naming principles and rules
* Use of an _identifier_ class (usually without style). Eg.: `.button`, `.sidebar`, `.navigation`
* Use of `.module` or `.page` as sufixes classes to wrap a _module_/_page_'s children. Eg.: `.sidebar.module`, `.login.page`
* Use of interchangeable _modifiers_ classes to set an element's appearance/behavior. Eg.: `.button.primary`
* Use of lisp-case for naming classes. All lowercase. Eg.: `.big`, `.red`, `.box`
* Use of space in HTML to separate class modifiers. Eg.: `<div class="big red box">`
* Composed-words separated by a single hyphen or underline (never double). Eg.: `with-icon` or `with_icon`
* Use syntax from natural languages like noun/modifier relationships, word order, and plurality to intuitively link concepts. Eg.: `<button class="small rounded primary button">` or `<div class="buttons">`
* * Use `/` to visually separate different _modules_ within a same HTML element. Eg.: `<div class="big red box / narrow grid container">`

### Adjectives order
Use the proper English order of adjectives for achieving a more intuitive description of elements.
1. Quantity or number. Eg.: `.three`
2. Quality or opinion. Eg.: `.beautiful`
3. Size. Eg.: `.big`
4. Age. Eg.: `.old`
5. Shape. Eg.: `.rounded`
6. Color. Eg.: `.blue`
7. Proper adjective. Eg.: `.brazilian`, `.translucid`, `.antique`
<br/>_(Often nationality, other place of origin, or material)_
8. Purpose or qualifier. Eg.: `.tasty`

For example, a way too much described `.box.module`: 
```HTML
<div class="big rounded blue antique brazilian box module">
```

### Plurality to name groups
When elements of the same _core block_ or _module_ are grouped together, use its plural form to define a particular style within it.
For example, a group of `.buttons` might remove margins, borders, and even some positioning.
```HTML
<div class="buttons">
  <button class="small primary button"></button>
  <button class="small secondary button"></button>
</div>
```

# Formatting
> Every line of code should appear to be written by a single person, no matter the number of contributors.

Follow [mdo's Code Guide](http://codeguide.co/) standards to keep the code consistent. Things like properties ordering, values and unit format etc, are fundamental to achieve consistency.

### Less/Sass style order
When declaring styles in a file, order as follow:
1. Sass/Less variables
1. HTML styles
1. Classes
2. IDs

### Linter
Use [SCSS Lint](https://github.com/brigade/scss-lint) to help you stay on the right track. Install its [plugin](https://github.com/brigade/scss-lint#editor-integration) on your editor of choice. Also, use [this Syntacss configuration file](https://gist.github.com/sergiofontes/47ec6addc1768855b3e7b2aba992f96f) to remain compliant with [mdo's Code Guide](http://codeguide.co/) standards.

### Autoprefixer
Use [Autoprefixer](https://github.com/postcss/autoprefixer) to handle CSS vendor prefixes. In other words, you shouldn't manually write these annoying prefixes.

### Git
Keep an eye on Guava's [Git standards](https://github.com/guava/standards/blob/master/git.md) and on the following naming convention for branches.
* Use a hyphen to separate words (eg.: `name-of-branch`).
* Use a slash to separate branch prefix from branch name (eg.: `prefix/name-of-branch`).
* `master`—the main branch of design version.
* `feature/…`—adds something new.
* `fix/…`—fixes one or more bugs.
* `chore/…`—improves performance, etc.


# Further reading
- [Code Guide](http://codeguide.co/), by mdo
- [Atomic Design Methodology](http://atomicdesign.bradfrost.com/chapter-2/), by Brad Frost
- [An introduction to OOCSS](https://www.smashingmagazine.com/2011/12/an-introduction-to-object-oriented-css-oocss/), by Louis Lazaris
- [Learning from Lego: A Step Forward in Modular Web Design](http://alistapart.com/article/learning-from-lego-a-step-forward-in-modular-web-design), by Samantha Zhang
- [Depth of Applicability](https://smacss.com/book/applicability), by Jonathan Snook
- [BEM sucks](https://twitter.com/samuelfine/status/575646836251344897), by Samuel Fine
