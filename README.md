# My homepage and blog

#### Video Demo:  https://www.youtube.com/watch?v=s9fL5LPNJfU

#### Description:

The final project for CS50 is my own homepage and blogging website.

The journey of this project began with the **week 8 of CS50X course** with HTML, CSS and JS. I started writing the styles, from buttons to navigation bar, all from scratch, coming accross many portfolios and homepages, taking inspiration from them. I was struggling to create CS50X like left side navigation.

**Then came week 9: Flask**. It was such a relief. I got to know about templates and learnt that developers don't keep copying navbars to each page of their website after adding a new link.

Later I discovered the CSS Grid and used CSS Grid template area for the layout of my website. Then I wrote my own static page generator for blogs written in markdown using the [markdown-it js library](https://www.npmjs.com/package/markdown-it). I could now write blogs in markdown with some of my own syntax for tags like `<kbd>` and the static page generator would create the jinja template which later was served by the flask application.

I was hoping to submit this as my final project but I again started to change the codebase to ReactJS and Gatsby - which is an awesome static page generator with GraphQL support.

## Structure of final project

This repository contains three directories:
* **homepage:** The first phase of my project where I was struggling to create column layout, ultimately creating the website for phones.
* **homepage-grid:** Flask was used for serving the website with CSS Grid layout for website layout. [toHTML.js](./homepage-grid/markdown/toHTML.js) is the static page generator for markdown files.
* **homepage-final:** This is the final source of my website made in ReactJS and GatsbyJS.

## How to serve locally?

First clone this repository and `cd` into the repository directory.

```shell
git clone https://github.com/tripathics/my-homepage-project
# or
git clone git@github.com:tripathics/my-homepage-project
```

```shell
cd my-homepage-project
```

### homepage

Source: https://github.com/tripathics/my-homepage-project/tree/main/homepage
This is the first version. `cd` into the `homepage` directory.

**Project structure:**

```
├── contact.html
├── galary.html
├── index.html
├── posts.html
├── projects.html
└── static
    ├── media
    │   ├── comingsoon.jpg
    │   ├── comingsoon.png
    │   ├── dna.png
    │   ├── filter.png
    │   ├── linkedin.svg
    │   ├── loanenq.png
    │   ├── menu-close.svg
    │   ├── menu-open.svg
    │   ├── pp.jpeg
    │   ├── speller.png
    │   ├── todo.png
    │   └── typing-game.png
    ├── script.js
    └── styles.css
```

```shell
cd homepage
```
Open the `index.html` file in any browser like google-chrome, firefox or safari. e.g. if you are on linux, open the index.html on google-chrome through terminal as

```shell
google-chrome-stable ./index.html
```

### homepage-grid

Source: https://github.com/tripathics/my-homepage-project/tree/main/homepage-grid
Demo: https://tripathics.github.io/homepage
This one is made using flask.

**Project structure:**
```
.: app.py, requirements.txt
├── blogs: all .md blog files here
├── markdown: toHTML.js static page generator
├── static: stylesheets and media
│   ├── favicons
│   ├── hljs: for syntax highlighting of code blocks in blogs
│   └── media: more media
│       ├── media-large: large media files
│       ├── posts: flask jinja templates generated from toHTML.js
│       │   └── hero: hero section images for blogs
│       ├── skills: icons for my skill section
│       └── square: immages after my intro in index.html
└── templates: layout template and templates for all the pages
```

```shell
cd homepage-grid
```

Install dependencies using python pip.

```shell
python -m pip install -r requirements.txt
```

Run app.py

```shell
python app.py
```
The app will run on [`localhost:5000`](http://localhost:5000) and can be accessed by opening the above link in a web browser.

>**Note:** If you are using linux, you may need to replace `python` by `python` three in the above commands.

#### How I implemented the website layout using CSS Grid

In [layout.html](homepage-grid/templates/layout.html), I have four elements: `<nav>`, `<div class="greet">`, `<main>` and `<footer>`:
```html
<body class="grid-container">
    <nav>
        ...
        the website navbar
        ...
    </nav>
    <div class="greet">
        ...
        this is where my profile picture
        and social media information goes
        ...
    </div>
    <main>
        ...
        main content goes here
        ...
    </main>
    <footer>
        ...
        footer of the website
        ...
    </footer>
</body>

```

On mobile screens, the webiste shows this arrangement from top to bottom.

In [styles.css](homepage-grid/static/styles.css):

```css
@media screen and (min-width: 925px) {
    .grid-container {
        display: grid;
        grid-template-areas:
            "nul nv"
            "grt mn"
            "ftr mn";
        grid-template-columns: minmax(21rem, 1fr) minmax(0, 2fr);
        grid-template-rows: var(--main-offset) 530px auto;
    }

    .greet {
        position: sticky;
        top: var(--nav-height);
        grid-area: grt;
        vertical-align: bottom;
        display: flex;
        flex-direction: column;
        justify-content: center;
    }

    nav {
        grid-area: nv;
    }

    main {
        --main-min-height: calc(100vh - var(--main-offset));
        grid-area: mn;
        min-height: var(--main-min-height);
        scroll-behavior: smooth;
    }

    footer {
        --footer-offset: calc(var(--main-offset) + var(--greet-height));
        position: sticky;
        top: var(--footer-offset);
        grid-area: ftr;
    }
}
```

For desktop screens (I have set width greater than 925px), the `.grid-container` class `display` property is set to `grid`.

The `grid-template-areas` defines areas in the grid container which is later assigned to the above elements for their respective positions on screen.

`grid-template-columns` allows us to define the width of columns, which are 2 in no. in this case:

    nul
    grt
    ftr

and

    nv
    mn
    mn

Width of first column is half of second column:

```css
grid-template-columns: minmax(21rem, 1fr) minmax(0, 2fr);
/* min width of first colunn is 21rem and that of second column is 0px */
```

Then the grid-areas are assigned to the above 4 elements:

grid-area|Element
:---:|:---:
nul|None
grt|`<div class="greet">`
ftr|`<footer>`
nv|`<navbar>`
mn|`<main>`

Similarly, the height of rows are also set using the `grid-template-rows` property.

In addition to that, the `<nav>` element and `<div class="greet">` have their position set to `sticky`, enabling only the `<main>` element to scroll.

The design was inspired by Jen Looper's portfolio website: [jenlooper.com](https://jenlooper.com)

#### Implementation of static page generator for MD files

I used the Node filesystem module to read markdown files as input. Then I have used the `markdown-it` npm package for compiling MD files to HTML.

`markdown-it-attrs` is used for setting attributes to markdown (like `id` tags where are later used for giving ids to headings).

`markdown-it-kbd` is used for setting custom syntax for `<kbd>` tags in MD.

I have then used some `regex` for finding titles and headings and defined `wrapper` for wrapping sections with jinja syntax.

The `regex` is also used for generating table of contents by finding each heading, getting its `id` attribute and setting the href of toc list items with that `id`. Apart from generating toc, `regex` is used to wrap the section from one heading to other heading in the `sectionWrap()` function.

The result string is later concatenated and written into the `outFile`.

### homepage-final

Source: https://github.com/tripathics/my-homepage-project/tree/main/homepage-final
Demo: https://tripathics.github.io

This one is made in React and Gatsby. For this, you will need `npm` and `node` on your system. Install `node` for your system from [here](https://nodejs.org/en/).

**Project structure:**
```
.: gatsby-browser.js  gatsby-config.js  package.json  package-lock.json
├── src
│   ├── assets: some media files
│   ├── components: React components
│   ├── content: content for my blogs (MD files)
│   │   └── tripathics-content
│   │       └── images: images for blogs
│   ├── data: projects data
│   ├── layouts: website layout (that CSS Grid layout)
│   ├── pages: all the website pages
│   │   └── posts: pages for blog posts
│   ├── styles: stylesheets in scss
│   └── utils: some configuration and helper functions
└── static: more media files
    ├── projects
    ├── skills
    └── square

```

```shell
cd homepage-final
```

Install the dependencies

```shell
npm i
```

Run the app

```shell
npm start
```

Gatsby app starts its development server at [localhost:8000](http://localhost:8000). Open this link in your web browser.


#### Why I implemented it using ReactJS and GatsbyJS

The inspiration for converting the codebase to ReactJS came from Tania Rascia: [taniarascia.com](https://taniarascia.com). I started learning ReactJS during Apr 2022 for my internship project.

ReactJS is a frontend framework for building websites. In react, we have components like HTML elements but with much more functionality like the components are dynamically rendered.

ReactJS is also great for making single page applications (SPA). And the advantage of using GatsbyJS is that it generates static site from ReactJS website and Markdown files.

---

Developing this project, I learnt
* Flask
* MarkDown
* CSS and SCSS
* React
* Gatsby
* GraphQL

Thank you David J. Malan and CS50 team for this great learning experience. :pray: