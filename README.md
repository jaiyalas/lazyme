# lazyme

A extensional setting files for generating slides (as html5) with pandoc and reveal.js.

### features

* adding (fixed) twilight-style syntax highlight (**syntaxH.css**)
* adding minor layout adjustment  (**custom.css**)
* adding some color (**custom.css**)
    + including `<em>`, `<strong>` and `<del>`
    + introducing `.headline` for coloring `<h1>`
    + introducing `.headline_alt` for coloring `<h1>`
* providing a basic pandoc template (**lazyme.html**)
* adding pandoc variable *root* for local loading-path (**lazyme.html**)
    + default value is directing to my personal dropbox public where I leave an online copy
* adding pandoc variable *trans* for setting transition (**lazyme.html**)
    + default value is "concave"

## usage

### frequently used parameters

* `-s` output whole file (aka `--standalone`)
* `-t X` output format (aka `--to=X`)
	+ Notice: `X` should be `"revealjs"` only
* `-i` make all bullets incremental (aka `--incremental`)
* `--mathjax` enable MathJax
* `--toc` add table of contents
	* `--toc-depth=*NUMBER*` specify how depth you want in your toc
* `-N` make numbered section headings
* `-V` define variable (aka `--variable`)
    * `--X=Y` "X" is name and "Y" is value
* `--template=X` assign template file by "X"

### suggested uses

The simplest way

```{.bash}
pandoc  -s -t revealjs --template=lazyme.html input.md -o output.html
```

When you have not only one file

```{.bash}
pandoc  -s -t revealjs --template=lazyme.html *.md -o output.html
```

Personal favorite

```{.bash}
pandoc  -s -t revealjs --template=lazyme.html -V theme='moon' -V root="./" *.md -o text.html
```

#### online css/js

Sometimes uploading slides to internet will be required,
I need some way to make slides can display correctly without
uploading the whole lazyme thing.
So I make a copy of the newest lazyme files and upload them
onto my dropbox. If you don't assign the variable *root*,
pandoc will route slide to load css/js files from my dropbox.

### available transitions

You can configure transition mode by simply adding

```{.bash}
-V trans="_anyone_from_below_"
```

* none
* fade
* slide
* convex
* concave *(default)*
* zoom

### available themes

You can configure color theme by simply adding

```{.bash}
-V theme="_anyone_from_below_"
```

* Dark-style
    + moon.css
    + night.css
    + black.css *(default)*
    + blood.css
    + league.css
* Light-style
    + solarized.css
    + beige.css
    + serif.css
    + simple.css
    + white.css
    + sky.css

## hints on making slides

### how to add extra class/id for sections

This works only on level-1 or level-2 headers.

```
# title {.class-name}
## title {#id-name}
```

### how to setup background for slides

A page will be created by an lv-1 or lv-2 header,
the way to set the bg is to add `data-background`.
For example, one can set color or image as background by

```
# title {data-background="/PATH/TO/IMAGE/"}
## title {data-background="#F57"}
```

### add side note

```{.xml}
<aside class="notes">
  something you want to say
</aside>
```
