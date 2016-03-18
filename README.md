## usage 

The simplest way: 

```
pandoc  text.md -s -t revealjs --template=tmp.html -o text.html
```

My personal favorite:

```
pandoc  text.md -s -t revealjs --template=tmp.html --variable theme='moon' -o text.html
```

### frequently used parameters

* `-s` output whole file (aka `--standalone`)
* `-t XXX` output format (aka `--to=XXX`)
	+ Notice: here the `XXX` should be `"revealjs"` only
* `-i` make all bullets incremental (aka `--incremental`)
* `--mathjax` enable MathJax
* `--toc` add table of contents
	* `--toc-depth=*NUMBER*` specify how depth you want in your toc
* `-N` make numbered section headings

### available themes

You can configure color theme by simply adding

> --avariable transition="_anyone_from_below_"

+ moon.css
+ solarized.css
+ beige.css
+ night.css
+ black.css *(default)*
+ serif.css
+ blood.css
+ simple.css
+ white.css
+ league.css
+ sky.css

### available transitions

You can configure transition mode by simply adding

> --avariable transition="_anyone_from_below_"

* none 
* fade 
* slide
* convex
* concave *(default)*
* zoom

## notes on markdown syntax 

### Manipulate reveal.js from markdown

#### How to add attributes into section

Sections in reveal.js will be generated for each title, regardless its level. There is a basic way to achieve so by adding `{attr=balue}`. 

For example, one can specifies the background image as  
`# title {data-background="/PATH/TO/IMAGE/"}`
