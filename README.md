# My homepage and blog

#### Video Demo:  <URL HERE>
#### Description:

The final project for CS50 is my own homepage and blogging website. 

The journey of this project began with the **week 8 of CS50X course** with HTML, CSS and JS. I started writing the styles, from buttons to navigation bar, all from scratch, coming accross many portfolios and homepages, taking inspiration from them. I was struggling to create CS50X like left side navigation. 

**Then came week 9: Flask**. It was such a relief. I got to know about templates and learnt that developers don't keep copying navbars to each page of their website after adding a new link. 

Later I discovered the CSS Grid and used CSS Grid template area for the layout of my website. Then I wrote my own static site generator for blogs written in markdown using the [markdown-it js library](https://www.npmjs.com/package/markdown-it). I could now write blogs in markdown with some of my own syntax for tags like `<kbd>` and the static site generator would create the jinja template which later was served by the flask application. 

I was hoping to submit this as my final project but I again started to change the codebase to ReactJS and Gatsby - which is an awesome static site generator with GraphQL support.

## Structure of final project

This repository contains three directories: 
* **homepage:** The first phase of my project where I was struggling to create column layout, ultimately creating the website for phones.
* **homepage-grid:** Flask was used for serving the website with CSS Grid layout for website layout. [toHTML.js](./markdown/toHTML.js) is the static site generator for markdown files. 
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
    │   ├── comingsoon.jpg
    │   ├── comingsoon.png
    │   ├── dna.png
    │   ├── filter.png
    │   ├── linkedin.svg
    │   ├── loanenq.png
    │   ├── menu-close.svg
    │   ├── menu-open.svg
    │   ├── pp.jpeg
    │   ├── speller.png
    │   ├── todo.png
    │   └── typing-game.png
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

This one is made using flask. 

**Project structure:**
```
.: app.py, requirements.txt
├── blogs: all .md blog files here
├── markdown: toHTML.js static site generator
├── static: stylesheets and media
│   ├── favicons
│   ├── hljs: for syntax highlighting of code blocks in blogs
│   └── media: more media
│       ├── media-large: large media files
│       ├── posts: flask jinja templates generated from toHTML.js
│       │   └── hero: hero section images for blogs
│       ├── skills: icons for my skill section
│       └── square: immages after my intro in index.html
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

>**Note:** If you are using linux, you may need to replace `python` by `python` three in the above commands.

### homepage-final

This one is made in React and Gatsby. For this, you will need `npm` and `node` on your system. Install `node` for your system from [here](https://nodejs.org/en/).

**Project structure:**
```
.: gatsby-browser.js  gatsby-config.js  package.json  package-lock.json
├── src
│   ├── assets: some media files 
│   ├── components: React components
│   ├── content: content for my blogs (MD files)
│   │   └── tripathics-content
│   │       └── images: images for blogs
│   ├── data: projects data
│   ├── layouts: website layout (that CSS Grid layout)
│   ├── pages: all the website pages
│   │   └── posts: pages for blog posts
│   ├── styles: stylesheets in scss
│   └── utils: some configuration and helper functions
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

---

Thank you David J. Malan and CS50 team for this great learning experience. :pray: