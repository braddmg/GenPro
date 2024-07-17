---
title: "Test"
layout: post
---
<!DOCTYPE html>
<html lang="" xml:lang="">
<head>

  <meta charset="utf-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge" />
  <title>3.1 HTML document | R Markdown: The Definitive Guide</title>
  <meta name="description" content="The first official book authored by the core R Markdown developers that provides a comprehensive and accurate reference to the R Markdown ecosystem. With R Markdown, you can easily create reproducible data analysis reports, presentations, dashboards, interactive applications, books, dissertations, websites, and journal articles, while enjoying the simplicity of Markdown and the great power of R and other languages." />
  <meta name="generator" content="bookdown 0.37 and GitBook 2.6.7" />

  <meta property="og:title" content="3.1 HTML document | R Markdown: The Definitive Guide" />
  <meta property="og:type" content="book" />
  <meta property="og:image" content="https://bookdown.org/yihui/rmarkdown//images/cover.png" />
  <meta property="og:description" content="The first official book authored by the core R Markdown developers that provides a comprehensive and accurate reference to the R Markdown ecosystem. With R Markdown, you can easily create reproducible data analysis reports, presentations, dashboards, interactive applications, books, dissertations, websites, and journal articles, while enjoying the simplicity of Markdown and the great power of R and other languages." />
  <meta name="github-repo" content="rstudio/rmarkdown-book" />

  <meta name="twitter:card" content="summary" />
  <meta name="twitter:title" content="3.1 HTML document | R Markdown: The Definitive Guide" />
  
  <meta name="twitter:description" content="The first official book authored by the core R Markdown developers that provides a comprehensive and accurate reference to the R Markdown ecosystem. With R Markdown, you can easily create reproducible data analysis reports, presentations, dashboards, interactive applications, books, dissertations, websites, and journal articles, while enjoying the simplicity of Markdown and the great power of R and other languages." />
  <meta name="twitter:image" content="https://bookdown.org/yihui/rmarkdown//images/cover.png" />

<meta name="author" content="Yihui Xie, J. J. Allaire, Garrett Grolemund" />


<meta name="date" content="2023-12-30" />

  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <meta name="apple-mobile-web-app-capable" content="yes" />
  <meta name="apple-mobile-web-app-status-bar-style" content="black" />
  
  
<link rel="prev" href="documents.html"/>
<link rel="next" href="notebook.html"/>
<script src="libs/jquery/jquery-3.6.0.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/fuse.js@6.4.6/dist/fuse.min.js"></script>
<link href="libs/gitbook/css/style.css" rel="stylesheet" />
<link href="libs/gitbook/css/plugin-table.css" rel="stylesheet" />
<link href="libs/gitbook/css/plugin-bookdown.css" rel="stylesheet" />
<link href="libs/gitbook/css/plugin-highlight.css" rel="stylesheet" />
<link href="libs/gitbook/css/plugin-search.css" rel="stylesheet" />
<link href="libs/gitbook/css/plugin-fontsettings.css" rel="stylesheet" />
<link href="libs/gitbook/css/plugin-clipboard.css" rel="stylesheet" />








<link href="libs/anchor-sections/anchor-sections.css" rel="stylesheet" />
<link href="libs/anchor-sections/anchor-sections-hash.css" rel="stylesheet" />
<script src="libs/anchor-sections/anchor-sections.js"></script>
<script src="libs/htmlwidgets/htmlwidgets.js"></script>
<script src="libs/sigma/sigma.min.js"></script>
<script src="libs/sigma/plugins/sigma.parsers.gexf.min.js"></script>
<script src="libs/sigma-binding/sigma.js"></script>


<style type="text/css">
pre > code.sourceCode { white-space: pre; position: relative; }
pre > code.sourceCode > span { display: inline-block; line-height: 1.25; }
pre > code.sourceCode > span:empty { height: 1.2em; }
.sourceCode { overflow: visible; }
code.sourceCode > span { color: inherit; text-decoration: inherit; }
pre.sourceCode { margin: 0; }
@media screen {
div.sourceCode { overflow: auto; }
}
@media print {
pre > code.sourceCode { white-space: pre-wrap; }
pre > code.sourceCode > span { text-indent: -5em; padding-left: 5em; }
}
pre.numberSource code
  { counter-reset: source-line 0; }
pre.numberSource code > span
  { position: relative; left: -4em; counter-increment: source-line; }
pre.numberSource code > span > a:first-child::before
  { content: counter(source-line);
    position: relative; left: -1em; text-align: right; vertical-align: baseline;
    border: none; display: inline-block;
    -webkit-touch-callout: none; -webkit-user-select: none;
    -khtml-user-select: none; -moz-user-select: none;
    -ms-user-select: none; user-select: none;
    padding: 0 4px; width: 4em;
    color: #aaaaaa;
  }
pre.numberSource { margin-left: 3em; border-left: 1px solid #aaaaaa;  padding-left: 4px; }
div.sourceCode
  {   }
@media screen {
pre > code.sourceCode > span > a:first-child::before { text-decoration: underline; }
}
code span.al { color: #ff0000; font-weight: bold; } /* Alert */
code span.an { color: #60a0b0; font-weight: bold; font-style: italic; } /* Annotation */
code span.at { color: #7d9029; } /* Attribute */
code span.bn { color: #40a070; } /* BaseN */
code span.bu { } /* BuiltIn */
code span.cf { color: #007020; font-weight: bold; } /* ControlFlow */
code span.ch { color: #4070a0; } /* Char */
code span.cn { color: #880000; } /* Constant */
code span.co { color: #60a0b0; font-style: italic; } /* Comment */
code span.cv { color: #60a0b0; font-weight: bold; font-style: italic; } /* CommentVar */
code span.do { color: #ba2121; font-style: italic; } /* Documentation */
code span.dt { color: #902000; } /* DataType */
code span.dv { color: #40a070; } /* DecVal */
code span.er { color: #ff0000; font-weight: bold; } /* Error */
code span.ex { } /* Extension */
code span.fl { color: #40a070; } /* Float */
code span.fu { color: #06287e; } /* Function */
code span.im { } /* Import */
code span.in { color: #60a0b0; font-weight: bold; font-style: italic; } /* Information */
code span.kw { color: #007020; font-weight: bold; } /* Keyword */
code span.op { color: #666666; } /* Operator */
code span.ot { color: #007020; } /* Other */
code span.pp { color: #bc7a00; } /* Preprocessor */
code span.sc { color: #4070a0; } /* SpecialChar */
code span.ss { color: #bb6688; } /* SpecialString */
code span.st { color: #4070a0; } /* String */
code span.va { color: #19177c; } /* Variable */
code span.vs { color: #4070a0; } /* VerbatimString */
code span.wa { color: #60a0b0; font-weight: bold; font-style: italic; } /* Warning */
</style>

<style type="text/css">
  
  div.hanging-indent{margin-left: 1.5em; text-indent: -1.5em;}
</style>
<style type="text/css">
/* Used with Pandoc 2.11+ new --citeproc when CSL is used */
div.csl-bib-body { }
div.csl-entry {
  clear: both;
}
.hanging div.csl-entry {
  margin-left:2em;
  text-indent:-2em;
}
div.csl-left-margin {
  min-width:2em;
  float:left;
}
div.csl-right-inline {
  margin-left:2em;
  padding-left:1em;
}
div.csl-indent {
  margin-left: 2em;
}
</style>

<link rel="stylesheet" href="css/style.css" type="text/css" />
</head>

<body>



  <div class="book without-animation with-summary font-size-2 font-family-1" data-basepath=".">

    <div class="book-summary">
      <nav role="navigation">

<ul class="summary">
<li><a href="./">R Markdown: The Definitive Guide</a></li>

<li class="divider"></li>
<li class="chapter" data-level="" data-path="index.html"><a href="index.html"><i class="fa fa-check"></i>Preface</a>
<ul>
<li class="chapter" data-level="" data-path="how-to-read-this-book.html"><a href="how-to-read-this-book.html"><i class="fa fa-check"></i>How to read this book</a></li>
<li class="chapter" data-level="" data-path="structure-of-the-book.html"><a href="structure-of-the-book.html"><i class="fa fa-check"></i>Structure of the book</a></li>
<li class="chapter" data-level="" data-path="software-info.html"><a href="software-info.html"><i class="fa fa-check"></i>Software information and conventions</a></li>
<li class="chapter" data-level="" data-path="acknowledgments.html"><a href="acknowledgments.html"><i class="fa fa-check"></i>Acknowledgments</a></li>
</ul></li>
<li class="chapter" data-level="" data-path="author.html"><a href="author.html"><i class="fa fa-check"></i>About the Authors</a>
<ul>
<li class="chapter" data-level="" data-path="yihui-xie.html"><a href="yihui-xie.html"><i class="fa fa-check"></i>Yihui Xie</a></li>
<li class="chapter" data-level="" data-path="j.j.-allaire.html"><a href="j.j.-allaire.html"><i class="fa fa-check"></i>J.J. Allaire</a></li>
<li class="chapter" data-level="" data-path="garrett-grolemund.html"><a href="garrett-grolemund.html"><i class="fa fa-check"></i>Garrett Grolemund</a></li>
</ul></li>
<li class="part"><span><b>I Get Started</b></span></li>
<li class="chapter" data-level="1" data-path="installation.html"><a href="installation.html"><i class="fa fa-check"></i><b>1</b> Installation</a></li>
<li class="chapter" data-level="2" data-path="basics.html"><a href="basics.html"><i class="fa fa-check"></i><b>2</b> Basics</a>
<ul>
<li class="chapter" data-level="2.1" data-path="basics-examples.html"><a href="basics-examples.html"><i class="fa fa-check"></i><b>2.1</b> Example applications</a>
<ul>
<li class="chapter" data-level="2.1.1" data-path="basics-examples.html"><a href="basics-examples.html#airbnbs-knowledge-repository"><i class="fa fa-check"></i><b>2.1.1</b> Airbnb’s knowledge repository</a></li>
<li class="chapter" data-level="2.1.2" data-path="basics-examples.html"><a href="basics-examples.html#homework-assignments-on-rpubs"><i class="fa fa-check"></i><b>2.1.2</b> Homework assignments on RPubs</a></li>
<li class="chapter" data-level="2.1.3" data-path="basics-examples.html"><a href="basics-examples.html#personalized-mail"><i class="fa fa-check"></i><b>2.1.3</b> Personalized mail</a></li>
<li class="chapter" data-level="2.1.4" data-path="basics-examples.html"><a href="basics-examples.html#employer-health-benefits-survey"><i class="fa fa-check"></i><b>2.1.4</b> 2017 Employer Health Benefits Survey</a></li>
<li class="chapter" data-level="2.1.5" data-path="basics-examples.html"><a href="basics-examples.html#examples-journal"><i class="fa fa-check"></i><b>2.1.5</b> Journal articles</a></li>
<li class="chapter" data-level="2.1.6" data-path="basics-examples.html"><a href="basics-examples.html#dashboards-at-eelloo"><i class="fa fa-check"></i><b>2.1.6</b> Dashboards at eelloo</a></li>
<li class="chapter" data-level="2.1.7" data-path="basics-examples.html"><a href="basics-examples.html#examples-books"><i class="fa fa-check"></i><b>2.1.7</b> Books</a></li>
<li class="chapter" data-level="2.1.8" data-path="basics-examples.html"><a href="basics-examples.html#examples-websites"><i class="fa fa-check"></i><b>2.1.8</b> Websites</a></li>
</ul></li>
<li class="chapter" data-level="2.2" data-path="compile.html"><a href="compile.html"><i class="fa fa-check"></i><b>2.2</b> Compile an R Markdown document</a></li>
<li class="chapter" data-level="2.3" data-path="cheat-sheets.html"><a href="cheat-sheets.html"><i class="fa fa-check"></i><b>2.3</b> Cheat sheets</a></li>
<li class="chapter" data-level="2.4" data-path="output-formats.html"><a href="output-formats.html"><i class="fa fa-check"></i><b>2.4</b> Output formats</a></li>
<li class="chapter" data-level="2.5" data-path="markdown-syntax.html"><a href="markdown-syntax.html"><i class="fa fa-check"></i><b>2.5</b> Markdown syntax</a>
<ul>
<li class="chapter" data-level="2.5.1" data-path="markdown-syntax.html"><a href="markdown-syntax.html#inline-formatting"><i class="fa fa-check"></i><b>2.5.1</b> Inline formatting</a></li>
<li class="chapter" data-level="2.5.2" data-path="markdown-syntax.html"><a href="markdown-syntax.html#block-level-elements"><i class="fa fa-check"></i><b>2.5.2</b> Block-level elements</a></li>
<li class="chapter" data-level="2.5.3" data-path="markdown-syntax.html"><a href="markdown-syntax.html#math-expressions"><i class="fa fa-check"></i><b>2.5.3</b> Math expressions</a></li>
</ul></li>
<li class="chapter" data-level="2.6" data-path="r-code.html"><a href="r-code.html"><i class="fa fa-check"></i><b>2.6</b> R code chunks and inline R code</a>
<ul>
<li class="chapter" data-level="2.6.1" data-path="r-code.html"><a href="r-code.html#figures"><i class="fa fa-check"></i><b>2.6.1</b> Figures</a></li>
<li class="chapter" data-level="2.6.2" data-path="r-code.html"><a href="r-code.html#tables"><i class="fa fa-check"></i><b>2.6.2</b> Tables</a></li>
</ul></li>
<li class="chapter" data-level="2.7" data-path="language-engines.html"><a href="language-engines.html"><i class="fa fa-check"></i><b>2.7</b> Other language engines</a>
<ul>
<li class="chapter" data-level="2.7.1" data-path="language-engines.html"><a href="language-engines.html#python"><i class="fa fa-check"></i><b>2.7.1</b> Python</a></li>
<li class="chapter" data-level="2.7.2" data-path="language-engines.html"><a href="language-engines.html#shell-scripts"><i class="fa fa-check"></i><b>2.7.2</b> Shell scripts</a></li>
<li class="chapter" data-level="2.7.3" data-path="language-engines.html"><a href="language-engines.html#sql"><i class="fa fa-check"></i><b>2.7.3</b> SQL</a></li>
<li class="chapter" data-level="2.7.4" data-path="language-engines.html"><a href="language-engines.html#rcpp"><i class="fa fa-check"></i><b>2.7.4</b> Rcpp</a></li>
<li class="chapter" data-level="2.7.5" data-path="language-engines.html"><a href="language-engines.html#stan"><i class="fa fa-check"></i><b>2.7.5</b> Stan</a></li>
<li class="chapter" data-level="2.7.6" data-path="language-engines.html"><a href="language-engines.html#javascript-and-css"><i class="fa fa-check"></i><b>2.7.6</b> JavaScript and CSS</a></li>
<li class="chapter" data-level="2.7.7" data-path="language-engines.html"><a href="language-engines.html#julia"><i class="fa fa-check"></i><b>2.7.7</b> Julia</a></li>
<li class="chapter" data-level="2.7.8" data-path="language-engines.html"><a href="language-engines.html#c-and-fortran"><i class="fa fa-check"></i><b>2.7.8</b> C and Fortran</a></li>
</ul></li>
<li class="chapter" data-level="2.8" data-path="interactive-documents.html"><a href="interactive-documents.html"><i class="fa fa-check"></i><b>2.8</b> Interactive documents</a>
<ul>
<li class="chapter" data-level="2.8.1" data-path="interactive-documents.html"><a href="interactive-documents.html#intro-widgets"><i class="fa fa-check"></i><b>2.8.1</b> HTML widgets</a></li>
<li class="chapter" data-level="2.8.2" data-path="interactive-documents.html"><a href="interactive-documents.html#intro-shiny"><i class="fa fa-check"></i><b>2.8.2</b> Shiny documents</a></li>
</ul></li>
</ul></li>
<li class="part"><span><b>II Output Formats</b></span></li>
<li class="chapter" data-level="3" data-path="documents.html"><a href="documents.html"><i class="fa fa-check"></i><b>3</b> Documents</a>
<ul>
<li class="chapter" data-level="3.1" data-path="html-document.html"><a href="html-document.html"><i class="fa fa-check"></i><b>3.1</b> HTML document</a>
<ul>
<li class="chapter" data-level="3.1.1" data-path="html-document.html"><a href="html-document.html#table-of-contents"><i class="fa fa-check"></i><b>3.1.1</b> Table of contents</a></li>
<li class="chapter" data-level="3.1.2" data-path="html-document.html"><a href="html-document.html#section-numbering"><i class="fa fa-check"></i><b>3.1.2</b> Section numbering</a></li>
<li class="chapter" data-level="3.1.3" data-path="html-document.html"><a href="html-document.html#tabbed-sections"><i class="fa fa-check"></i><b>3.1.3</b> Tabbed sections</a></li>
<li class="chapter" data-level="3.1.4" data-path="html-document.html"><a href="html-document.html#appearance-and-style"><i class="fa fa-check"></i><b>3.1.4</b> Appearance and style</a></li>
<li class="chapter" data-level="3.1.5" data-path="html-document.html"><a href="html-document.html#figure-options"><i class="fa fa-check"></i><b>3.1.5</b> Figure options</a></li>
<li class="chapter" data-level="3.1.6" data-path="html-document.html"><a href="html-document.html#data-frame-printing"><i class="fa fa-check"></i><b>3.1.6</b> Data frame printing</a></li>
<li class="chapter" data-level="3.1.7" data-path="html-document.html"><a href="html-document.html#code-folding"><i class="fa fa-check"></i><b>3.1.7</b> Code folding</a></li>
<li class="chapter" data-level="3.1.8" data-path="html-document.html"><a href="html-document.html#mathjax-equations"><i class="fa fa-check"></i><b>3.1.8</b> MathJax equations</a></li>
<li class="chapter" data-level="3.1.9" data-path="html-document.html"><a href="html-document.html#document-dependencies"><i class="fa fa-check"></i><b>3.1.9</b> Document dependencies</a></li>
<li class="chapter" data-level="3.1.10" data-path="html-document.html"><a href="html-document.html#advanced-customization"><i class="fa fa-check"></i><b>3.1.10</b> Advanced customization</a></li>
<li class="chapter" data-level="3.1.11" data-path="html-document.html"><a href="html-document.html#shared-options"><i class="fa fa-check"></i><b>3.1.11</b> Shared options</a></li>
<li class="chapter" data-level="3.1.12" data-path="html-document.html"><a href="html-document.html#html-fragments"><i class="fa fa-check"></i><b>3.1.12</b> HTML fragments</a></li>
</ul></li>
<li class="chapter" data-level="3.2" data-path="notebook.html"><a href="notebook.html"><i class="fa fa-check"></i><b>3.2</b> Notebook</a>
<ul>
<li class="chapter" data-level="3.2.1" data-path="notebook.html"><a href="notebook.html#using-notebooks"><i class="fa fa-check"></i><b>3.2.1</b> Using Notebooks</a></li>
<li class="chapter" data-level="3.2.2" data-path="notebook.html"><a href="notebook.html#saving-and-sharing"><i class="fa fa-check"></i><b>3.2.2</b> Saving and sharing</a></li>
<li class="chapter" data-level="3.2.3" data-path="notebook.html"><a href="notebook.html#notebook-format"><i class="fa fa-check"></i><b>3.2.3</b> Notebook format</a></li>
</ul></li>
<li class="chapter" data-level="3.3" data-path="pdf-document.html"><a href="pdf-document.html"><i class="fa fa-check"></i><b>3.3</b> PDF document</a>
<ul>
<li class="chapter" data-level="3.3.1" data-path="pdf-document.html"><a href="pdf-document.html#table-of-contents-1"><i class="fa fa-check"></i><b>3.3.1</b> Table of contents</a></li>
<li class="chapter" data-level="3.3.2" data-path="pdf-document.html"><a href="pdf-document.html#figure-options-1"><i class="fa fa-check"></i><b>3.3.2</b> Figure options</a></li>
<li class="chapter" data-level="3.3.3" data-path="pdf-document.html"><a href="pdf-document.html#data-frame-printing-1"><i class="fa fa-check"></i><b>3.3.3</b> Data frame printing</a></li>
<li class="chapter" data-level="3.3.4" data-path="pdf-document.html"><a href="pdf-document.html#syntax-highlighting"><i class="fa fa-check"></i><b>3.3.4</b> Syntax highlighting</a></li>
<li class="chapter" data-level="3.3.5" data-path="pdf-document.html"><a href="pdf-document.html#latex-options"><i class="fa fa-check"></i><b>3.3.5</b> LaTeX options</a></li>
<li class="chapter" data-level="3.3.6" data-path="pdf-document.html"><a href="pdf-document.html#latex-packages-for-citations"><i class="fa fa-check"></i><b>3.3.6</b> LaTeX packages for citations</a></li>
<li class="chapter" data-level="3.3.7" data-path="pdf-document.html"><a href="pdf-document.html#advanced-customization-1"><i class="fa fa-check"></i><b>3.3.7</b> Advanced customization</a></li>
<li class="chapter" data-level="3.3.8" data-path="pdf-document.html"><a href="pdf-document.html#other-features"><i class="fa fa-check"></i><b>3.3.8</b> Other features</a></li>
</ul></li>
<li class="chapter" data-level="3.4" data-path="word-document.html"><a href="word-document.html"><i class="fa fa-check"></i><b>3.4</b> Word document</a>
<ul>
<li class="chapter" data-level="3.4.1" data-path="word-document.html"><a href="word-document.html#other-features-1"><i class="fa fa-check"></i><b>3.4.1</b> Other features</a></li>
</ul></li>
<li class="chapter" data-level="3.5" data-path="opendocument-text-document.html"><a href="opendocument-text-document.html"><i class="fa fa-check"></i><b>3.5</b> OpenDocument Text document</a>
<ul>
<li class="chapter" data-level="3.5.1" data-path="opendocument-text-document.html"><a href="opendocument-text-document.html#other-features-2"><i class="fa fa-check"></i><b>3.5.1</b> Other features</a></li>
</ul></li>
<li class="chapter" data-level="3.6" data-path="rich-text-format-document.html"><a href="rich-text-format-document.html"><i class="fa fa-check"></i><b>3.6</b> Rich Text Format document</a>
<ul>
<li class="chapter" data-level="3.6.1" data-path="rich-text-format-document.html"><a href="rich-text-format-document.html#other-features-3"><i class="fa fa-check"></i><b>3.6.1</b> Other features</a></li>
</ul></li>
<li class="chapter" data-level="3.7" data-path="markdown-document.html"><a href="markdown-document.html"><i class="fa fa-check"></i><b>3.7</b> Markdown document</a>
<ul>
<li class="chapter" data-level="3.7.1" data-path="markdown-document.html"><a href="markdown-document.html#markdown-variants"><i class="fa fa-check"></i><b>3.7.1</b> Markdown variants</a></li>
<li class="chapter" data-level="3.7.2" data-path="markdown-document.html"><a href="markdown-document.html#other-features-4"><i class="fa fa-check"></i><b>3.7.2</b> Other features</a></li>
</ul></li>
<li class="chapter" data-level="3.8" data-path="r-package-vignette.html"><a href="r-package-vignette.html"><i class="fa fa-check"></i><b>3.8</b> R package vignette</a></li>
</ul></li>
<li class="chapter" data-level="4" data-path="presentations.html"><a href="presentations.html"><i class="fa fa-check"></i><b>4</b> Presentations</a>
<ul>
<li class="chapter" data-level="4.1" data-path="ioslides-presentation.html"><a href="ioslides-presentation.html"><i class="fa fa-check"></i><b>4.1</b> ioslides presentation</a>
<ul>
<li class="chapter" data-level="4.1.1" data-path="ioslides-presentation.html"><a href="ioslides-presentation.html#display-modes"><i class="fa fa-check"></i><b>4.1.1</b> Display modes</a></li>
<li class="chapter" data-level="4.1.2" data-path="ioslides-presentation.html"><a href="ioslides-presentation.html#incremental-bullets"><i class="fa fa-check"></i><b>4.1.2</b> Incremental bullets</a></li>
<li class="chapter" data-level="4.1.3" data-path="ioslides-presentation.html"><a href="ioslides-presentation.html#visual-appearance"><i class="fa fa-check"></i><b>4.1.3</b> Visual appearance</a></li>
<li class="chapter" data-level="4.1.4" data-path="ioslides-presentation.html"><a href="ioslides-presentation.html#code-highlighting"><i class="fa fa-check"></i><b>4.1.4</b> Code highlighting</a></li>
<li class="chapter" data-level="4.1.5" data-path="ioslides-presentation.html"><a href="ioslides-presentation.html#adding-a-logo"><i class="fa fa-check"></i><b>4.1.5</b> Adding a logo</a></li>
<li class="chapter" data-level="4.1.6" data-path="ioslides-presentation.html"><a href="ioslides-presentation.html#tables-1"><i class="fa fa-check"></i><b>4.1.6</b> Tables</a></li>
<li class="chapter" data-level="4.1.7" data-path="ioslides-presentation.html"><a href="ioslides-presentation.html#advanced-layout"><i class="fa fa-check"></i><b>4.1.7</b> Advanced layout</a></li>
<li class="chapter" data-level="4.1.8" data-path="ioslides-presentation.html"><a href="ioslides-presentation.html#text-color"><i class="fa fa-check"></i><b>4.1.8</b> Text color</a></li>
<li class="chapter" data-level="4.1.9" data-path="ioslides-presentation.html"><a href="ioslides-presentation.html#presenter-mode"><i class="fa fa-check"></i><b>4.1.9</b> Presenter mode</a></li>
<li class="chapter" data-level="4.1.10" data-path="ioslides-presentation.html"><a href="ioslides-presentation.html#printing-and-pdf-output"><i class="fa fa-check"></i><b>4.1.10</b> Printing and PDF output</a></li>
<li class="chapter" data-level="4.1.11" data-path="ioslides-presentation.html"><a href="ioslides-presentation.html#custom-templates-2"><i class="fa fa-check"></i><b>4.1.11</b> Custom templates</a></li>
<li class="chapter" data-level="4.1.12" data-path="ioslides-presentation.html"><a href="ioslides-presentation.html#other-features-5"><i class="fa fa-check"></i><b>4.1.12</b> Other features</a></li>
</ul></li>
<li class="chapter" data-level="4.2" data-path="slidy-presentation.html"><a href="slidy-presentation.html"><i class="fa fa-check"></i><b>4.2</b> Slidy presentation</a>
<ul>
<li class="chapter" data-level="4.2.1" data-path="slidy-presentation.html"><a href="slidy-presentation.html#display-modes-1"><i class="fa fa-check"></i><b>4.2.1</b> Display modes</a></li>
<li class="chapter" data-level="4.2.2" data-path="slidy-presentation.html"><a href="slidy-presentation.html#text-size"><i class="fa fa-check"></i><b>4.2.2</b> Text size</a></li>
<li class="chapter" data-level="4.2.3" data-path="slidy-presentation.html"><a href="slidy-presentation.html#footer-elements"><i class="fa fa-check"></i><b>4.2.3</b> Footer elements</a></li>
<li class="chapter" data-level="4.2.4" data-path="slidy-presentation.html"><a href="slidy-presentation.html#other-features-6"><i class="fa fa-check"></i><b>4.2.4</b> Other features</a></li>
</ul></li>
<li class="chapter" data-level="4.3" data-path="beamer-presentation.html"><a href="beamer-presentation.html"><i class="fa fa-check"></i><b>4.3</b> Beamer presentation</a>
<ul>
<li class="chapter" data-level="4.3.1" data-path="beamer-presentation.html"><a href="beamer-presentation.html#themes"><i class="fa fa-check"></i><b>4.3.1</b> Themes</a></li>
<li class="chapter" data-level="4.3.2" data-path="beamer-presentation.html"><a href="beamer-presentation.html#slide-level"><i class="fa fa-check"></i><b>4.3.2</b> Slide level</a></li>
<li class="chapter" data-level="4.3.3" data-path="beamer-presentation.html"><a href="beamer-presentation.html#other-features-7"><i class="fa fa-check"></i><b>4.3.3</b> Other features</a></li>
</ul></li>
<li class="chapter" data-level="4.4" data-path="powerpoint-presentation.html"><a href="powerpoint-presentation.html"><i class="fa fa-check"></i><b>4.4</b> PowerPoint presentation</a>
<ul>
<li class="chapter" data-level="4.4.1" data-path="powerpoint-presentation.html"><a href="powerpoint-presentation.html#ppt-templates"><i class="fa fa-check"></i><b>4.4.1</b> Custom templates</a></li>
<li class="chapter" data-level="4.4.2" data-path="powerpoint-presentation.html"><a href="powerpoint-presentation.html#other-features-8"><i class="fa fa-check"></i><b>4.4.2</b> Other features</a></li>
</ul></li>
</ul></li>
<li class="part"><span><b>III Extensions</b></span></li>
<li class="chapter" data-level="5" data-path="dashboards.html"><a href="dashboards.html"><i class="fa fa-check"></i><b>5</b> Dashboards</a>
<ul>
<li class="chapter" data-level="5.1" data-path="layout.html"><a href="layout.html"><i class="fa fa-check"></i><b>5.1</b> Layout</a>
<ul>
<li class="chapter" data-level="5.1.1" data-path="layout.html"><a href="layout.html#row-based-layouts"><i class="fa fa-check"></i><b>5.1.1</b> Row-based layouts</a></li>
<li class="chapter" data-level="5.1.2" data-path="layout.html"><a href="layout.html#attributes-on-sections"><i class="fa fa-check"></i><b>5.1.2</b> Attributes on sections</a></li>
<li class="chapter" data-level="5.1.3" data-path="layout.html"><a href="layout.html#multiple-pages"><i class="fa fa-check"></i><b>5.1.3</b> Multiple pages</a></li>
<li class="chapter" data-level="5.1.4" data-path="layout.html"><a href="layout.html#story-boards"><i class="fa fa-check"></i><b>5.1.4</b> Story boards</a></li>
</ul></li>
<li class="chapter" data-level="5.2" data-path="dashboard-components.html"><a href="dashboard-components.html"><i class="fa fa-check"></i><b>5.2</b> Components</a>
<ul>
<li class="chapter" data-level="5.2.1" data-path="dashboard-components.html"><a href="dashboard-components.html#value-boxes"><i class="fa fa-check"></i><b>5.2.1</b> Value boxes</a></li>
<li class="chapter" data-level="5.2.2" data-path="dashboard-components.html"><a href="dashboard-components.html#gauges"><i class="fa fa-check"></i><b>5.2.2</b> Gauges</a></li>
<li class="chapter" data-level="5.2.3" data-path="dashboard-components.html"><a href="dashboard-components.html#text-annotations"><i class="fa fa-check"></i><b>5.2.3</b> Text annotations</a></li>
<li class="chapter" data-level="5.2.4" data-path="dashboard-components.html"><a href="dashboard-components.html#navigation-bar"><i class="fa fa-check"></i><b>5.2.4</b> Navigation bar</a></li>
</ul></li>
<li class="chapter" data-level="5.3" data-path="shiny.html"><a href="shiny.html"><i class="fa fa-check"></i><b>5.3</b> Shiny</a>
<ul>
<li class="chapter" data-level="5.3.1" data-path="shiny.html"><a href="shiny.html#getting-started"><i class="fa fa-check"></i><b>5.3.1</b> Getting started</a></li>
<li class="chapter" data-level="5.3.2" data-path="shiny.html"><a href="shiny.html#a-shiny-dashboard-example"><i class="fa fa-check"></i><b>5.3.2</b> A Shiny dashboard example</a></li>
<li class="chapter" data-level="5.3.3" data-path="shiny.html"><a href="shiny.html#input-sidebar"><i class="fa fa-check"></i><b>5.3.3</b> Input sidebar</a></li>
<li class="chapter" data-level="5.3.4" data-path="shiny.html"><a href="shiny.html#learning-more"><i class="fa fa-check"></i><b>5.3.4</b> Learning more</a></li>
</ul></li>
</ul></li>
<li class="chapter" data-level="6" data-path="tufte-handouts.html"><a href="tufte-handouts.html"><i class="fa fa-check"></i><b>6</b> Tufte Handouts</a>
<ul>
<li class="chapter" data-level="6.1" data-path="tufte-headings.html"><a href="tufte-headings.html"><i class="fa fa-check"></i><b>6.1</b> Headings</a></li>
<li class="chapter" data-level="6.2" data-path="tufte-figures.html"><a href="tufte-figures.html"><i class="fa fa-check"></i><b>6.2</b> Figures</a>
<ul>
<li class="chapter" data-level="6.2.1" data-path="tufte-figures.html"><a href="tufte-figures.html#margin-figures"><i class="fa fa-check"></i><b>6.2.1</b> Margin figures</a></li>
<li class="chapter" data-level="6.2.2" data-path="tufte-figures.html"><a href="tufte-figures.html#arbitrary-margin-content"><i class="fa fa-check"></i><b>6.2.2</b> Arbitrary margin content</a></li>
<li class="chapter" data-level="6.2.3" data-path="tufte-figures.html"><a href="tufte-figures.html#full-width-figures"><i class="fa fa-check"></i><b>6.2.3</b> Full-width figures</a></li>
<li class="chapter" data-level="6.2.4" data-path="tufte-figures.html"><a href="tufte-figures.html#main-column-figures"><i class="fa fa-check"></i><b>6.2.4</b> Main column figures</a></li>
</ul></li>
<li class="chapter" data-level="6.3" data-path="tufte-sidenotes.html"><a href="tufte-sidenotes.html"><i class="fa fa-check"></i><b>6.3</b> Sidenotes</a></li>
<li class="chapter" data-level="6.4" data-path="tufte-references.html"><a href="tufte-references.html"><i class="fa fa-check"></i><b>6.4</b> References</a></li>
<li class="chapter" data-level="6.5" data-path="tufte-tables.html"><a href="tufte-tables.html"><i class="fa fa-check"></i><b>6.5</b> Tables</a></li>
<li class="chapter" data-level="6.6" data-path="tufte-quotes.html"><a href="tufte-quotes.html"><i class="fa fa-check"></i><b>6.6</b> Block quotes</a></li>
<li class="chapter" data-level="6.7" data-path="tufte-responsiveness.html"><a href="tufte-responsiveness.html"><i class="fa fa-check"></i><b>6.7</b> Responsiveness</a></li>
<li class="chapter" data-level="6.8" data-path="tufte-sans.html"><a href="tufte-sans.html"><i class="fa fa-check"></i><b>6.8</b> Sans-serif fonts and epigraphs</a></li>
<li class="chapter" data-level="6.9" data-path="tufte-css.html"><a href="tufte-css.html"><i class="fa fa-check"></i><b>6.9</b> Customize CSS styles</a></li>
</ul></li>
<li class="chapter" data-level="7" data-path="xaringan.html"><a href="xaringan.html"><i class="fa fa-check"></i><b>7</b> xaringan Presentations</a>
<ul>
<li class="chapter" data-level="7.1" data-path="xaringan-start.html"><a href="xaringan-start.html"><i class="fa fa-check"></i><b>7.1</b> Get started</a></li>
<li class="chapter" data-level="7.2" data-path="xaringan-key.html"><a href="xaringan-key.html"><i class="fa fa-check"></i><b>7.2</b> Keyboard shortcuts</a></li>
<li class="chapter" data-level="7.3" data-path="xaringan-format.html"><a href="xaringan-format.html"><i class="fa fa-check"></i><b>7.3</b> Slide formatting</a>
<ul>
<li class="chapter" data-level="7.3.1" data-path="xaringan-format.html"><a href="xaringan-format.html#slides-and-properties"><i class="fa fa-check"></i><b>7.3.1</b> Slides and properties</a></li>
<li class="chapter" data-level="7.3.2" data-path="xaringan-format.html"><a href="xaringan-format.html#the-title-slide"><i class="fa fa-check"></i><b>7.3.2</b> The title slide</a></li>
<li class="chapter" data-level="7.3.3" data-path="xaringan-format.html"><a href="xaringan-format.html#content-classes"><i class="fa fa-check"></i><b>7.3.3</b> Content classes</a></li>
<li class="chapter" data-level="7.3.4" data-path="xaringan-format.html"><a href="xaringan-format.html#incremental-slides"><i class="fa fa-check"></i><b>7.3.4</b> Incremental slides</a></li>
<li class="chapter" data-level="7.3.5" data-path="xaringan-format.html"><a href="xaringan-format.html#xaringan-notes"><i class="fa fa-check"></i><b>7.3.5</b> Presenter notes</a></li>
<li class="chapter" data-level="7.3.6" data-path="xaringan-format.html"><a href="xaringan-format.html#yolo-true"><i class="fa fa-check"></i><b>7.3.6</b> yolo: true</a></li>
</ul></li>
<li class="chapter" data-level="7.4" data-path="xaringan-preview.html"><a href="xaringan-preview.html"><i class="fa fa-check"></i><b>7.4</b> Build and preview slides</a></li>
<li class="chapter" data-level="7.5" data-path="css-and-themes.html"><a href="css-and-themes.html"><i class="fa fa-check"></i><b>7.5</b> CSS and themes</a></li>
<li class="chapter" data-level="7.6" data-path="some-tips.html"><a href="some-tips.html"><i class="fa fa-check"></i><b>7.6</b> Some tips</a>
<ul>
<li class="chapter" data-level="7.6.1" data-path="some-tips.html"><a href="some-tips.html#autoplay-slides"><i class="fa fa-check"></i><b>7.6.1</b> Autoplay slides</a></li>
<li class="chapter" data-level="7.6.2" data-path="some-tips.html"><a href="some-tips.html#countdown-timer"><i class="fa fa-check"></i><b>7.6.2</b> Countdown timer</a></li>
<li class="chapter" data-level="7.6.3" data-path="some-tips.html"><a href="some-tips.html#highlight-code-lines"><i class="fa fa-check"></i><b>7.6.3</b> Highlight code lines</a></li>
<li class="chapter" data-level="7.6.4" data-path="some-tips.html"><a href="some-tips.html#working-offline"><i class="fa fa-check"></i><b>7.6.4</b> Working offline</a></li>
<li class="chapter" data-level="7.6.5" data-path="some-tips.html"><a href="some-tips.html#macros"><i class="fa fa-check"></i><b>7.6.5</b> Macros</a></li>
<li class="chapter" data-level="7.6.6" data-path="some-tips.html"><a href="some-tips.html#disadvantages"><i class="fa fa-check"></i><b>7.6.6</b> Disadvantages</a></li>
</ul></li>
</ul></li>
<li class="chapter" data-level="8" data-path="revealjs.html"><a href="revealjs.html"><i class="fa fa-check"></i><b>8</b> reveal.js Presentations</a>
<ul>
<li class="chapter" data-level="8.1" data-path="display-modes-2.html"><a href="display-modes-2.html"><i class="fa fa-check"></i><b>8.1</b> Display modes</a></li>
<li class="chapter" data-level="8.2" data-path="appearance-and-style-1.html"><a href="appearance-and-style-1.html"><i class="fa fa-check"></i><b>8.2</b> Appearance and style</a>
<ul>
<li class="chapter" data-level="8.2.1" data-path="appearance-and-style-1.html"><a href="appearance-and-style-1.html#smaller-text"><i class="fa fa-check"></i><b>8.2.1</b> Smaller text</a></li>
</ul></li>
<li class="chapter" data-level="8.3" data-path="slide-transitions.html"><a href="slide-transitions.html"><i class="fa fa-check"></i><b>8.3</b> Slide transitions</a></li>
<li class="chapter" data-level="8.4" data-path="slide-backgrounds.html"><a href="slide-backgrounds.html"><i class="fa fa-check"></i><b>8.4</b> Slide backgrounds</a></li>
<li class="chapter" data-level="8.5" data-path="d-presentations.html"><a href="d-presentations.html"><i class="fa fa-check"></i><b>8.5</b> 2-D presentations</a></li>
<li class="chapter" data-level="8.6" data-path="custom-css-1.html"><a href="custom-css-1.html"><i class="fa fa-check"></i><b>8.6</b> Custom CSS</a>
<ul>
<li class="chapter" data-level="8.6.1" data-path="custom-css-1.html"><a href="custom-css-1.html#slide-ids-and-classes"><i class="fa fa-check"></i><b>8.6.1</b> Slide IDs and classes</a></li>
<li class="chapter" data-level="8.6.2" data-path="custom-css-1.html"><a href="custom-css-1.html#styling-text-spans"><i class="fa fa-check"></i><b>8.6.2</b> Styling text spans</a></li>
</ul></li>
<li class="chapter" data-level="8.7" data-path="reveal.js-options.html"><a href="reveal.js-options.html"><i class="fa fa-check"></i><b>8.7</b> reveal.js options</a></li>
<li class="chapter" data-level="8.8" data-path="reveal.js-plugins.html"><a href="reveal.js-plugins.html"><i class="fa fa-check"></i><b>8.8</b> reveal.js plugins</a></li>
<li class="chapter" data-level="8.9" data-path="other-features-9.html"><a href="other-features-9.html"><i class="fa fa-check"></i><b>8.9</b> Other features</a></li>
</ul></li>
<li class="chapter" data-level="9" data-path="community.html"><a href="community.html"><i class="fa fa-check"></i><b>9</b> Community Formats</a>
<ul>
<li class="chapter" data-level="9.1" data-path="prettydoc.html"><a href="prettydoc.html"><i class="fa fa-check"></i><b>9.1</b> Lightweight Pretty HTML Documents</a>
<ul>
<li class="chapter" data-level="9.1.1" data-path="prettydoc.html"><a href="prettydoc.html#prettydoc-usage"><i class="fa fa-check"></i><b>9.1.1</b> Usage</a></li>
<li class="chapter" data-level="9.1.2" data-path="prettydoc.html"><a href="prettydoc.html#prettydoc-vignettes"><i class="fa fa-check"></i><b>9.1.2</b> Package vignettes</a></li>
</ul></li>
<li class="chapter" data-level="9.2" data-path="rmdformats.html"><a href="rmdformats.html"><i class="fa fa-check"></i><b>9.2</b> The rmdformats package</a></li>
<li class="chapter" data-level="9.3" data-path="shower-presentations.html"><a href="shower-presentations.html"><i class="fa fa-check"></i><b>9.3</b> Shower presentations</a></li>
</ul></li>
<li class="chapter" data-level="10" data-path="websites.html"><a href="websites.html"><i class="fa fa-check"></i><b>10</b> Websites</a>
<ul>
<li class="chapter" data-level="10.1" data-path="blogdown-start.html"><a href="blogdown-start.html"><i class="fa fa-check"></i><b>10.1</b> Get started</a></li>
<li class="chapter" data-level="10.2" data-path="blogdown-directory.html"><a href="blogdown-directory.html"><i class="fa fa-check"></i><b>10.2</b> The directory structure</a></li>
<li class="chapter" data-level="10.3" data-path="blogdown-deploy.html"><a href="blogdown-deploy.html"><i class="fa fa-check"></i><b>10.3</b> Deployment</a></li>
<li class="chapter" data-level="10.4" data-path="blogdown-other.html"><a href="blogdown-other.html"><i class="fa fa-check"></i><b>10.4</b> Other site generators</a></li>
<li class="chapter" data-level="10.5" data-path="rmarkdown-site.html"><a href="rmarkdown-site.html"><i class="fa fa-check"></i><b>10.5</b> rmarkdown’s site generator</a>
<ul>
<li class="chapter" data-level="10.5.1" data-path="rmarkdown-site.html"><a href="rmarkdown-site.html#a-simple-example"><i class="fa fa-check"></i><b>10.5.1</b> A simple example</a></li>
<li class="chapter" data-level="10.5.2" data-path="rmarkdown-site.html"><a href="rmarkdown-site.html#site-authoring"><i class="fa fa-check"></i><b>10.5.2</b> Site authoring</a></li>
<li class="chapter" data-level="10.5.3" data-path="rmarkdown-site.html"><a href="rmarkdown-site.html#common-elements"><i class="fa fa-check"></i><b>10.5.3</b> Common elements</a></li>
<li class="chapter" data-level="10.5.4" data-path="rmarkdown-site.html"><a href="rmarkdown-site.html#site-navigation"><i class="fa fa-check"></i><b>10.5.4</b> Site navigation</a></li>
<li class="chapter" data-level="10.5.5" data-path="rmarkdown-site.html"><a href="rmarkdown-site.html#html-generation"><i class="fa fa-check"></i><b>10.5.5</b> HTML generation</a></li>
<li class="chapter" data-level="10.5.6" data-path="rmarkdown-site.html"><a href="rmarkdown-site.html#site-configuration"><i class="fa fa-check"></i><b>10.5.6</b> Site configuration</a></li>
<li class="chapter" data-level="10.5.7" data-path="rmarkdown-site.html"><a href="rmarkdown-site.html#publishing-websites"><i class="fa fa-check"></i><b>10.5.7</b> Publishing websites</a></li>
<li class="chapter" data-level="10.5.8" data-path="rmarkdown-site.html"><a href="rmarkdown-site.html#additional-examples"><i class="fa fa-check"></i><b>10.5.8</b> Additional examples</a></li>
<li class="chapter" data-level="10.5.9" data-path="rmarkdown-site.html"><a href="rmarkdown-site.html#custom-site-generators"><i class="fa fa-check"></i><b>10.5.9</b> Custom site generators</a></li>
</ul></li>
</ul></li>
<li class="chapter" data-level="11" data-path="pkgdown.html"><a href="pkgdown.html"><i class="fa fa-check"></i><b>11</b> HTML Documentation for R Packages</a>
<ul>
<li class="chapter" data-level="11.1" data-path="pkgdown-start.html"><a href="pkgdown-start.html"><i class="fa fa-check"></i><b>11.1</b> Get started</a></li>
<li class="chapter" data-level="11.2" data-path="pkgdown-components.html"><a href="pkgdown-components.html"><i class="fa fa-check"></i><b>11.2</b> Components</a>
<ul>
<li class="chapter" data-level="11.2.1" data-path="pkgdown-components.html"><a href="pkgdown-components.html#home-page"><i class="fa fa-check"></i><b>11.2.1</b> Home page</a></li>
<li class="chapter" data-level="11.2.2" data-path="pkgdown-components.html"><a href="pkgdown-components.html#function-reference"><i class="fa fa-check"></i><b>11.2.2</b> Function reference</a></li>
<li class="chapter" data-level="11.2.3" data-path="pkgdown-components.html"><a href="pkgdown-components.html#articles"><i class="fa fa-check"></i><b>11.2.3</b> Articles</a></li>
<li class="chapter" data-level="11.2.4" data-path="pkgdown-components.html"><a href="pkgdown-components.html#news"><i class="fa fa-check"></i><b>11.2.4</b> News</a></li>
<li class="chapter" data-level="11.2.5" data-path="pkgdown-components.html"><a href="pkgdown-components.html#navigation-bar-1"><i class="fa fa-check"></i><b>11.2.5</b> Navigation bar</a></li>
</ul></li>
</ul></li>
<li class="chapter" data-level="12" data-path="books.html"><a href="books.html"><i class="fa fa-check"></i><b>12</b> Books</a>
<ul>
<li class="chapter" data-level="12.1" data-path="bookdown-start.html"><a href="bookdown-start.html"><i class="fa fa-check"></i><b>12.1</b> Get started</a></li>
<li class="chapter" data-level="12.2" data-path="bookdown-project.html"><a href="bookdown-project.html"><i class="fa fa-check"></i><b>12.2</b> Project structure</a>
<ul>
<li class="chapter" data-level="12.2.1" data-path="bookdown-project.html"><a href="bookdown-project.html#index-file"><i class="fa fa-check"></i><b>12.2.1</b> Index file</a></li>
<li class="chapter" data-level="12.2.2" data-path="bookdown-project.html"><a href="bookdown-project.html#rmd-files"><i class="fa fa-check"></i><b>12.2.2</b> Rmd files</a></li>
<li class="chapter" data-level="12.2.3" data-path="bookdown-project.html"><a href="bookdown-project.html#bookdown.yml"><i class="fa fa-check"></i><b>12.2.3</b> <code>_bookdown.yml</code></a></li>
<li class="chapter" data-level="12.2.4" data-path="bookdown-project.html"><a href="bookdown-project.html#output.yml"><i class="fa fa-check"></i><b>12.2.4</b> <code>_output.yml</code></a></li>
</ul></li>
<li class="chapter" data-level="12.3" data-path="bookdown-markdown.html"><a href="bookdown-markdown.html"><i class="fa fa-check"></i><b>12.3</b> Markdown extensions</a>
<ul>
<li class="chapter" data-level="12.3.1" data-path="bookdown-markdown.html"><a href="bookdown-markdown.html#equations"><i class="fa fa-check"></i><b>12.3.1</b> Number and reference equations</a></li>
<li class="chapter" data-level="12.3.2" data-path="bookdown-markdown.html"><a href="bookdown-markdown.html#theorems"><i class="fa fa-check"></i><b>12.3.2</b> Theorems and proofs</a></li>
<li class="chapter" data-level="12.3.3" data-path="bookdown-markdown.html"><a href="bookdown-markdown.html#special-headers"><i class="fa fa-check"></i><b>12.3.3</b> Special headers</a></li>
<li class="chapter" data-level="12.3.4" data-path="bookdown-markdown.html"><a href="bookdown-markdown.html#text-references"><i class="fa fa-check"></i><b>12.3.4</b> Text references</a></li>
<li class="chapter" data-level="12.3.5" data-path="bookdown-markdown.html"><a href="bookdown-markdown.html#cross-referencing"><i class="fa fa-check"></i><b>12.3.5</b> Cross referencing</a></li>
</ul></li>
<li class="chapter" data-level="12.4" data-path="bookdown-output.html"><a href="bookdown-output.html"><i class="fa fa-check"></i><b>12.4</b> Output Formats</a>
<ul>
<li class="chapter" data-level="12.4.1" data-path="bookdown-output.html"><a href="bookdown-output.html#html"><i class="fa fa-check"></i><b>12.4.1</b> HTML</a></li>
<li class="chapter" data-level="12.4.2" data-path="bookdown-output.html"><a href="bookdown-output.html#latexpdf"><i class="fa fa-check"></i><b>12.4.2</b> LaTeX/PDF</a></li>
<li class="chapter" data-level="12.4.3" data-path="bookdown-output.html"><a href="bookdown-output.html#e-books"><i class="fa fa-check"></i><b>12.4.3</b> E-books</a></li>
<li class="chapter" data-level="12.4.4" data-path="bookdown-output.html"><a href="bookdown-output.html#a-single-document"><i class="fa fa-check"></i><b>12.4.4</b> A single document</a></li>
</ul></li>
<li class="chapter" data-level="12.5" data-path="bookdown-edit.html"><a href="bookdown-edit.html"><i class="fa fa-check"></i><b>12.5</b> Editing</a>
<ul>
<li class="chapter" data-level="12.5.1" data-path="bookdown-edit.html"><a href="bookdown-edit.html#build-the-book"><i class="fa fa-check"></i><b>12.5.1</b> Build the book</a></li>
<li class="chapter" data-level="12.5.2" data-path="bookdown-edit.html"><a href="bookdown-edit.html#preview-a-chapter"><i class="fa fa-check"></i><b>12.5.2</b> Preview a chapter</a></li>
<li class="chapter" data-level="12.5.3" data-path="bookdown-edit.html"><a href="bookdown-edit.html#serve-the-book"><i class="fa fa-check"></i><b>12.5.3</b> Serve the book</a></li>
<li class="chapter" data-level="12.5.4" data-path="bookdown-edit.html"><a href="bookdown-edit.html#rstudio-addins"><i class="fa fa-check"></i><b>12.5.4</b> RStudio addins</a></li>
</ul></li>
<li class="chapter" data-level="12.6" data-path="bookdown-publish.html"><a href="bookdown-publish.html"><i class="fa fa-check"></i><b>12.6</b> Publishing</a>
<ul>
<li class="chapter" data-level="12.6.1" data-path="bookdown-publish.html"><a href="bookdown-publish.html#rstudio-connect"><i class="fa fa-check"></i><b>12.6.1</b> RStudio Connect</a></li>
<li class="chapter" data-level="12.6.2" data-path="bookdown-publish.html"><a href="bookdown-publish.html#other-services"><i class="fa fa-check"></i><b>12.6.2</b> Other services</a></li>
<li class="chapter" data-level="12.6.3" data-path="bookdown-publish.html"><a href="bookdown-publish.html#publishers"><i class="fa fa-check"></i><b>12.6.3</b> Publishers</a></li>
</ul></li>
</ul></li>
<li class="chapter" data-level="13" data-path="journals.html"><a href="journals.html"><i class="fa fa-check"></i><b>13</b> Journals</a>
<ul>
<li class="chapter" data-level="13.1" data-path="rticles-start.html"><a href="rticles-start.html"><i class="fa fa-check"></i><b>13.1</b> Get started</a></li>
<li class="chapter" data-level="13.2" data-path="rticles-templates.html"><a href="rticles-templates.html"><i class="fa fa-check"></i><b>13.2</b> rticles templates</a></li>
<li class="chapter" data-level="13.3" data-path="rticles-usage.html"><a href="rticles-usage.html"><i class="fa fa-check"></i><b>13.3</b> Using a template</a></li>
<li class="chapter" data-level="13.4" data-path="rticles-latex.html"><a href="rticles-latex.html"><i class="fa fa-check"></i><b>13.4</b> LaTeX content</a></li>
<li class="chapter" data-level="13.5" data-path="rticles-bookdown.html"><a href="rticles-bookdown.html"><i class="fa fa-check"></i><b>13.5</b> Linking with bookdown</a></li>
<li class="chapter" data-level="13.6" data-path="rticles-contrib.html"><a href="rticles-contrib.html"><i class="fa fa-check"></i><b>13.6</b> Contributing templates</a></li>
</ul></li>
<li class="chapter" data-level="14" data-path="learnr.html"><a href="learnr.html"><i class="fa fa-check"></i><b>14</b> Interactive Tutorials</a>
<ul>
<li class="chapter" data-level="14.1" data-path="learnr-start.html"><a href="learnr-start.html"><i class="fa fa-check"></i><b>14.1</b> Get started</a></li>
<li class="chapter" data-level="14.2" data-path="learnr-types.html"><a href="learnr-types.html"><i class="fa fa-check"></i><b>14.2</b> Tutorial types</a></li>
<li class="chapter" data-level="14.3" data-path="learnr-exercises.html"><a href="learnr-exercises.html"><i class="fa fa-check"></i><b>14.3</b> Exercises</a>
<ul>
<li class="chapter" data-level="14.3.1" data-path="learnr-exercises.html"><a href="learnr-exercises.html#solutions"><i class="fa fa-check"></i><b>14.3.1</b> Solutions</a></li>
<li class="chapter" data-level="14.3.2" data-path="learnr-exercises.html"><a href="learnr-exercises.html#hints"><i class="fa fa-check"></i><b>14.3.2</b> Hints</a></li>
</ul></li>
<li class="chapter" data-level="14.4" data-path="learnr-quiz.html"><a href="learnr-quiz.html"><i class="fa fa-check"></i><b>14.4</b> Quiz questions</a></li>
<li class="chapter" data-level="14.5" data-path="learnr-videos.html"><a href="learnr-videos.html"><i class="fa fa-check"></i><b>14.5</b> Videos</a></li>
<li class="chapter" data-level="14.6" data-path="learnr-shiny.html"><a href="learnr-shiny.html"><i class="fa fa-check"></i><b>14.6</b> Shiny components</a></li>
<li class="chapter" data-level="14.7" data-path="learnr-nav.html"><a href="learnr-nav.html"><i class="fa fa-check"></i><b>14.7</b> Navigation and progress tracking</a></li>
</ul></li>
<li class="part"><span><b>IV Other Topics</b></span></li>
<li class="chapter" data-level="15" data-path="parameterized-reports.html"><a href="parameterized-reports.html"><i class="fa fa-check"></i><b>15</b> Parameterized reports</a>
<ul>
<li class="chapter" data-level="15.1" data-path="params-declare.html"><a href="params-declare.html"><i class="fa fa-check"></i><b>15.1</b> Declaring parameters</a></li>
<li class="chapter" data-level="15.2" data-path="params-use.html"><a href="params-use.html"><i class="fa fa-check"></i><b>15.2</b> Using parameters</a></li>
<li class="chapter" data-level="15.3" data-path="params-knit.html"><a href="params-knit.html"><i class="fa fa-check"></i><b>15.3</b> Knitting with parameters</a>
<ul>
<li class="chapter" data-level="15.3.1" data-path="params-knit.html"><a href="params-knit.html#the-knit-button"><i class="fa fa-check"></i><b>15.3.1</b> The <code>Knit</code> button</a></li>
<li class="chapter" data-level="15.3.2" data-path="params-knit.html"><a href="params-knit.html#knit-with-custom-parameters"><i class="fa fa-check"></i><b>15.3.2</b> Knit with custom parameters</a></li>
<li class="chapter" data-level="15.3.3" data-path="params-knit.html"><a href="params-knit.html#the-interactive-user-interface"><i class="fa fa-check"></i><b>15.3.3</b> The interactive user interface</a></li>
</ul></li>
<li class="chapter" data-level="15.4" data-path="params-publish.html"><a href="params-publish.html"><i class="fa fa-check"></i><b>15.4</b> Publishing</a></li>
</ul></li>
<li class="chapter" data-level="16" data-path="html-widgets.html"><a href="html-widgets.html"><i class="fa fa-check"></i><b>16</b> HTML Widgets</a>
<ul>
<li class="chapter" data-level="16.1" data-path="htmlwidgets-overview.html"><a href="htmlwidgets-overview.html"><i class="fa fa-check"></i><b>16.1</b> Overview</a></li>
<li class="chapter" data-level="16.2" data-path="htmlwidgets-sigma.html"><a href="htmlwidgets-sigma.html"><i class="fa fa-check"></i><b>16.2</b> A widget example (sigma.js)</a>
<ul>
<li class="chapter" data-level="16.2.1" data-path="htmlwidgets-sigma.html"><a href="htmlwidgets-sigma.html#file-layout"><i class="fa fa-check"></i><b>16.2.1</b> File layout</a></li>
<li class="chapter" data-level="16.2.2" data-path="htmlwidgets-sigma.html"><a href="htmlwidgets-sigma.html#dependencies"><i class="fa fa-check"></i><b>16.2.2</b> Dependencies</a></li>
<li class="chapter" data-level="16.2.3" data-path="htmlwidgets-sigma.html"><a href="htmlwidgets-sigma.html#r-binding"><i class="fa fa-check"></i><b>16.2.3</b> R binding</a></li>
<li class="chapter" data-level="16.2.4" data-path="htmlwidgets-sigma.html"><a href="htmlwidgets-sigma.html#javascript-binding"><i class="fa fa-check"></i><b>16.2.4</b> JavaScript binding</a></li>
<li class="chapter" data-level="16.2.5" data-path="htmlwidgets-sigma.html"><a href="htmlwidgets-sigma.html#demo"><i class="fa fa-check"></i><b>16.2.5</b> Demo</a></li>
</ul></li>
<li class="chapter" data-level="16.3" data-path="htmlwidgets-create.html"><a href="htmlwidgets-create.html"><i class="fa fa-check"></i><b>16.3</b> Creating your own widgets</a>
<ul>
<li class="chapter" data-level="16.3.1" data-path="htmlwidgets-create.html"><a href="htmlwidgets-create.html#requirements"><i class="fa fa-check"></i><b>16.3.1</b> Requirements</a></li>
<li class="chapter" data-level="16.3.2" data-path="htmlwidgets-create.html"><a href="htmlwidgets-create.html#scaffolding"><i class="fa fa-check"></i><b>16.3.2</b> Scaffolding</a></li>
<li class="chapter" data-level="16.3.3" data-path="htmlwidgets-create.html"><a href="htmlwidgets-create.html#other-packages"><i class="fa fa-check"></i><b>16.3.3</b> Other packages</a></li>
</ul></li>
<li class="chapter" data-level="16.4" data-path="htmlwidgets-size.html"><a href="htmlwidgets-size.html"><i class="fa fa-check"></i><b>16.4</b> Widget sizing</a>
<ul>
<li class="chapter" data-level="16.4.1" data-path="htmlwidgets-size.html"><a href="htmlwidgets-size.html#specifying-a-sizing-policy"><i class="fa fa-check"></i><b>16.4.1</b> Specifying a sizing policy</a></li>
<li class="chapter" data-level="16.4.2" data-path="htmlwidgets-size.html"><a href="htmlwidgets-size.html#javascript-resize-method"><i class="fa fa-check"></i><b>16.4.2</b> JavaScript resize method</a></li>
</ul></li>
<li class="chapter" data-level="16.5" data-path="htmlwidgets-advanced.html"><a href="htmlwidgets-advanced.html"><i class="fa fa-check"></i><b>16.5</b> Advanced topics</a>
<ul>
<li class="chapter" data-level="16.5.1" data-path="htmlwidgets-advanced.html"><a href="htmlwidgets-advanced.html#data-transformation"><i class="fa fa-check"></i><b>16.5.1</b> Data transformation</a></li>
<li class="chapter" data-level="16.5.2" data-path="htmlwidgets-advanced.html"><a href="htmlwidgets-advanced.html#passing-javascript-functions"><i class="fa fa-check"></i><b>16.5.2</b> Passing JavaScript functions</a></li>
<li class="chapter" data-level="16.5.3" data-path="htmlwidgets-advanced.html"><a href="htmlwidgets-advanced.html#custom-widget-html"><i class="fa fa-check"></i><b>16.5.3</b> Custom widget HTML</a></li>
<li class="chapter" data-level="16.5.4" data-path="htmlwidgets-advanced.html"><a href="htmlwidgets-advanced.html#create-a-widget-without-an-r-package"><i class="fa fa-check"></i><b>16.5.4</b> Create a widget without an R package</a></li>
</ul></li>
</ul></li>
<li class="chapter" data-level="17" data-path="document-templates.html"><a href="document-templates.html"><i class="fa fa-check"></i><b>17</b> Document Templates</a>
<ul>
<li class="chapter" data-level="17.1" data-path="template-structure.html"><a href="template-structure.html"><i class="fa fa-check"></i><b>17.1</b> Template structure</a></li>
<li class="chapter" data-level="17.2" data-path="template-support.html"><a href="template-support.html"><i class="fa fa-check"></i><b>17.2</b> Supporting files</a></li>
<li class="chapter" data-level="17.3" data-path="template-pandoc.html"><a href="template-pandoc.html"><i class="fa fa-check"></i><b>17.3</b> Custom Pandoc templates</a></li>
<li class="chapter" data-level="17.4" data-path="template-share.html"><a href="template-share.html"><i class="fa fa-check"></i><b>17.4</b> Sharing your templates</a></li>
</ul></li>
<li class="chapter" data-level="18" data-path="new-formats.html"><a href="new-formats.html"><i class="fa fa-check"></i><b>18</b> Creating New Formats</a>
<ul>
<li class="chapter" data-level="18.1" data-path="format-derive.html"><a href="format-derive.html"><i class="fa fa-check"></i><b>18.1</b> Deriving from built-in formats</a></li>
<li class="chapter" data-level="18.2" data-path="format-custom.html"><a href="format-custom.html"><i class="fa fa-check"></i><b>18.2</b> Fully custom formats</a></li>
<li class="chapter" data-level="18.3" data-path="format-use.html"><a href="format-use.html"><i class="fa fa-check"></i><b>18.3</b> Using a new format</a></li>
</ul></li>
<li class="chapter" data-level="19" data-path="shiny-documents.html"><a href="shiny-documents.html"><i class="fa fa-check"></i><b>19</b> Shiny Documents</a>
<ul>
<li class="chapter" data-level="19.1" data-path="shiny-start.html"><a href="shiny-start.html"><i class="fa fa-check"></i><b>19.1</b> Getting started</a></li>
<li class="chapter" data-level="19.2" data-path="shiny-deploy.html"><a href="shiny-deploy.html"><i class="fa fa-check"></i><b>19.2</b> Deployment</a>
<ul>
<li class="chapter" data-level="19.2.1" data-path="shiny-deploy.html"><a href="shiny-deploy.html#shinyapps.io"><i class="fa fa-check"></i><b>19.2.1</b> ShinyApps.io</a></li>
<li class="chapter" data-level="19.2.2" data-path="shiny-deploy.html"><a href="shiny-deploy.html#shiny-server-rstudio-connect"><i class="fa fa-check"></i><b>19.2.2</b> Shiny Server / RStudio Connect</a></li>
</ul></li>
<li class="chapter" data-level="19.3" data-path="shiny-embedded.html"><a href="shiny-embedded.html"><i class="fa fa-check"></i><b>19.3</b> Embedded Shiny apps</a>
<ul>
<li class="chapter" data-level="19.3.1" data-path="shiny-embedded.html"><a href="shiny-embedded.html#shiny-embed-inline"><i class="fa fa-check"></i><b>19.3.1</b> Inline applications</a></li>
<li class="chapter" data-level="19.3.2" data-path="shiny-embedded.html"><a href="shiny-embedded.html#external-applications"><i class="fa fa-check"></i><b>19.3.2</b> External applications</a></li>
</ul></li>
<li class="chapter" data-level="19.4" data-path="shiny-widgets.html"><a href="shiny-widgets.html"><i class="fa fa-check"></i><b>19.4</b> Shiny widgets</a>
<ul>
<li class="chapter" data-level="19.4.1" data-path="shiny-widgets.html"><a href="shiny-widgets.html#the-shinyapp-function"><i class="fa fa-check"></i><b>19.4.1</b> The <code>shinyApp()</code> function</a></li>
<li class="chapter" data-level="19.4.2" data-path="shiny-widgets.html"><a href="shiny-widgets.html#example-k-means-clustering"><i class="fa fa-check"></i><b>19.4.2</b> Example: k-Means clustering</a></li>
<li class="chapter" data-level="19.4.3" data-path="shiny-widgets.html"><a href="shiny-widgets.html#widget-size-and-layout"><i class="fa fa-check"></i><b>19.4.3</b> Widget size and layout</a></li>
</ul></li>
<li class="chapter" data-level="19.5" data-path="shiny-multiple.html"><a href="shiny-multiple.html"><i class="fa fa-check"></i><b>19.5</b> Multiple pages</a></li>
<li class="chapter" data-level="19.6" data-path="shiny-delay.html"><a href="shiny-delay.html"><i class="fa fa-check"></i><b>19.6</b> Delayed rendering</a></li>
<li class="chapter" data-level="19.7" data-path="shiny-args.html"><a href="shiny-args.html"><i class="fa fa-check"></i><b>19.7</b> Output arguments for render functions</a>
<ul>
<li class="chapter" data-level="19.7.1" data-path="shiny-args.html"><a href="shiny-args.html#a-caveat"><i class="fa fa-check"></i><b>19.7.1</b> A caveat</a></li>
</ul></li>
</ul></li>
<li class="chapter" data-level="" data-path="references.html"><a href="references.html"><i class="fa fa-check"></i>References</a></li>
<li class="divider"></li>
<li><a href="https://bookdown.org" target="_blank">Published with bookdown</a></li>

</ul>

      </nav>
    </div>

    <div class="book-body">
      <div class="body-inner">
        <div class="book-header" role="navigation">
          <h1>
            <i class="fa fa-circle-o-notch fa-spin"></i><a href="./">R Markdown: The Definitive Guide</a>
          </h1>
        </div>

        <div class="page-wrapper" tabindex="-1" role="main">
          <div class="page-inner">

            <section class="normal" id="section-">
<div id="html-document" class="section level2 hasAnchor" number="3.1">
<h2><span class="header-section-number">3.1</span> HTML document<a href="html-document.html#html-document" class="anchor-section" aria-label="Anchor link to header"></a></h2>
<p>As we just mentioned before, Markdown was originally designed for HTML output, so it may not be surprising that the HTML format has the richest features among all output formats. We recommend that you read this full section before you learn other output formats, because other formats have several features in common with the HTML document format, and we will not repeat these features in the corresponding sections.</p>
<p>To create an HTML document from R Markdown, you specify the <code>html_document</code> output format in the YAML metadata of your document:</p>
<div class="sourceCode" id="cb62"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb62-1"><a href="html-document.html#cb62-1" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span>
<span id="cb62-2"><a href="html-document.html#cb62-2" aria-hidden="true" tabindex="-1"></a><span class="fu">title</span><span class="kw">:</span><span class="at"> Habits</span></span>
<span id="cb62-3"><a href="html-document.html#cb62-3" aria-hidden="true" tabindex="-1"></a><span class="fu">author</span><span class="kw">:</span><span class="at"> John Doe</span></span>
<span id="cb62-4"><a href="html-document.html#cb62-4" aria-hidden="true" tabindex="-1"></a><span class="fu">date</span><span class="kw">:</span><span class="at"> March 22, 2005</span></span>
<span id="cb62-5"><a href="html-document.html#cb62-5" aria-hidden="true" tabindex="-1"></a><span class="fu">output</span><span class="kw">:</span><span class="at"> html_document</span></span>
<span id="cb62-6"><a href="html-document.html#cb62-6" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span></code></pre></div>
<div id="table-of-contents" class="section level3 hasAnchor" number="3.1.1">
<h3><span class="header-section-number">3.1.1</span> Table of contents<a href="html-document.html#table-of-contents" class="anchor-section" aria-label="Anchor link to header"></a></h3>
<p>You can add a table of contents (TOC) using the <code>toc</code> option and specify the depth of headers that it applies to using the <code>toc_depth</code> option. For example:</p>
<div class="sourceCode" id="cb63"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb63-1"><a href="html-document.html#cb63-1" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span>
<span id="cb63-2"><a href="html-document.html#cb63-2" aria-hidden="true" tabindex="-1"></a><span class="fu">title</span><span class="kw">:</span><span class="at"> </span><span class="st">&quot;Habits&quot;</span></span>
<span id="cb63-3"><a href="html-document.html#cb63-3" aria-hidden="true" tabindex="-1"></a><span class="fu">output</span><span class="kw">:</span></span>
<span id="cb63-4"><a href="html-document.html#cb63-4" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">html_document</span><span class="kw">:</span></span>
<span id="cb63-5"><a href="html-document.html#cb63-5" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">toc</span><span class="kw">:</span><span class="at"> </span><span class="ch">true</span></span>
<span id="cb63-6"><a href="html-document.html#cb63-6" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">toc_depth</span><span class="kw">:</span><span class="at"> </span><span class="dv">2</span></span>
<span id="cb63-7"><a href="html-document.html#cb63-7" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span></code></pre></div>
<p>If the table of contents depth is not explicitly specified, it defaults to 3 (meaning that all level 1, 2, and 3 headers will be included in the table of contents).</p>
<div id="floating-toc" class="section level4 hasAnchor" number="3.1.1.1">
<h4><span class="header-section-number">3.1.1.1</span> Floating TOC<a href="html-document.html#floating-toc" class="anchor-section" aria-label="Anchor link to header"></a></h4>
<p>You can specify the <code>toc_float</code> option to float the table of contents to the left of the main document content. The floating table of contents will always be visible even when the document is scrolled. For example:</p>
<div class="sourceCode" id="cb64"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb64-1"><a href="html-document.html#cb64-1" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span>
<span id="cb64-2"><a href="html-document.html#cb64-2" aria-hidden="true" tabindex="-1"></a><span class="fu">title</span><span class="kw">:</span><span class="at"> </span><span class="st">&quot;Habits&quot;</span></span>
<span id="cb64-3"><a href="html-document.html#cb64-3" aria-hidden="true" tabindex="-1"></a><span class="fu">output</span><span class="kw">:</span></span>
<span id="cb64-4"><a href="html-document.html#cb64-4" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">html_document</span><span class="kw">:</span></span>
<span id="cb64-5"><a href="html-document.html#cb64-5" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">toc</span><span class="kw">:</span><span class="at"> </span><span class="ch">true</span></span>
<span id="cb64-6"><a href="html-document.html#cb64-6" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">toc_float</span><span class="kw">:</span><span class="at"> </span><span class="ch">true</span></span>
<span id="cb64-7"><a href="html-document.html#cb64-7" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span></code></pre></div>
<p>You may optionally specify a list of options for the <code>toc_float</code> parameter which control its behavior. These options include:</p>
<ul>
<li><p><code>collapsed</code> (defaults to <code>TRUE</code>) controls whether the TOC appears with only the top-level (e.g., H2) headers. If collapsed initially, the TOC is automatically expanded inline when necessary.</p></li>
<li><p><code>smooth_scroll</code> (defaults to <code>TRUE</code>) controls whether page scrolls are animated when TOC items are navigated to via mouse clicks.</p></li>
</ul>
<p>For example:</p>
<div class="sourceCode" id="cb65"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb65-1"><a href="html-document.html#cb65-1" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span>
<span id="cb65-2"><a href="html-document.html#cb65-2" aria-hidden="true" tabindex="-1"></a><span class="fu">title</span><span class="kw">:</span><span class="at"> </span><span class="st">&quot;Habits&quot;</span></span>
<span id="cb65-3"><a href="html-document.html#cb65-3" aria-hidden="true" tabindex="-1"></a><span class="fu">output</span><span class="kw">:</span></span>
<span id="cb65-4"><a href="html-document.html#cb65-4" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">html_document</span><span class="kw">:</span></span>
<span id="cb65-5"><a href="html-document.html#cb65-5" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">toc</span><span class="kw">:</span><span class="at"> </span><span class="ch">true</span></span>
<span id="cb65-6"><a href="html-document.html#cb65-6" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">toc_float</span><span class="kw">:</span></span>
<span id="cb65-7"><a href="html-document.html#cb65-7" aria-hidden="true" tabindex="-1"></a><span class="at">      </span><span class="fu">collapsed</span><span class="kw">:</span><span class="at"> </span><span class="ch">false</span></span>
<span id="cb65-8"><a href="html-document.html#cb65-8" aria-hidden="true" tabindex="-1"></a><span class="at">      </span><span class="fu">smooth_scroll</span><span class="kw">:</span><span class="at"> </span><span class="ch">false</span></span>
<span id="cb65-9"><a href="html-document.html#cb65-9" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span></code></pre></div>
</div>
</div>
<div id="section-numbering" class="section level3 hasAnchor" number="3.1.2">
<h3><span class="header-section-number">3.1.2</span> Section numbering<a href="html-document.html#section-numbering" class="anchor-section" aria-label="Anchor link to header"></a></h3>
<p>You can add section numbering to headers using the <code>number_sections</code> option:</p>
<div class="sourceCode" id="cb66"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb66-1"><a href="html-document.html#cb66-1" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span>
<span id="cb66-2"><a href="html-document.html#cb66-2" aria-hidden="true" tabindex="-1"></a><span class="fu">title</span><span class="kw">:</span><span class="at"> </span><span class="st">&quot;Habits&quot;</span></span>
<span id="cb66-3"><a href="html-document.html#cb66-3" aria-hidden="true" tabindex="-1"></a><span class="fu">output</span><span class="kw">:</span></span>
<span id="cb66-4"><a href="html-document.html#cb66-4" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">html_document</span><span class="kw">:</span></span>
<span id="cb66-5"><a href="html-document.html#cb66-5" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">toc</span><span class="kw">:</span><span class="at"> </span><span class="ch">true</span></span>
<span id="cb66-6"><a href="html-document.html#cb66-6" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">number_sections</span><span class="kw">:</span><span class="at"> </span><span class="ch">true</span></span>
<span id="cb66-7"><a href="html-document.html#cb66-7" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span></code></pre></div>
<p>Note that if you do choose to use the <code>number_sections</code> option, you will likely also want to use <code>#</code> (H1) headers in your document as <code>##</code> (H2) headers will include a decimal point, because without H1 headers, you H2 headers will be numbered with <code>0.1</code>, <code>0.2</code>, and so on.</p>
</div>
<div id="tabbed-sections" class="section level3 hasAnchor" number="3.1.3">
<h3><span class="header-section-number">3.1.3</span> Tabbed sections<a href="html-document.html#tabbed-sections" class="anchor-section" aria-label="Anchor link to header"></a></h3>
<p>You can organize content using tabs by applying the <code>.tabset</code> class attribute to headers within a document. This will cause all sub-headers of the header with the <code>.tabset</code> attribute to appear within tabs rather than as standalone sections. For example:</p>
<div class="sourceCode" id="cb67"><pre class="sourceCode markdown"><code class="sourceCode markdown"><span id="cb67-1"><a href="html-document.html#cb67-1" aria-hidden="true" tabindex="-1"></a><span class="fu">## Quarterly Results {.tabset}</span></span>
<span id="cb67-2"><a href="html-document.html#cb67-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb67-3"><a href="html-document.html#cb67-3" aria-hidden="true" tabindex="-1"></a><span class="fu">### By Product</span></span>
<span id="cb67-4"><a href="html-document.html#cb67-4" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb67-5"><a href="html-document.html#cb67-5" aria-hidden="true" tabindex="-1"></a>(tab content)</span>
<span id="cb67-6"><a href="html-document.html#cb67-6" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb67-7"><a href="html-document.html#cb67-7" aria-hidden="true" tabindex="-1"></a><span class="fu">### By Region</span></span>
<span id="cb67-8"><a href="html-document.html#cb67-8" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb67-9"><a href="html-document.html#cb67-9" aria-hidden="true" tabindex="-1"></a>(tab content)</span></code></pre></div>
<p>You can also specify two additional attributes to control the appearance and behavior of the tabs. The <code>.tabset-fade</code> attribute causes the tabs to fade in and out when switching between tabs. The <code>.tabset-pills</code> attribute causes the visual appearance of the tabs to be “pill” (see Figure <a href="html-document.html#fig:tabset">3.1</a>) rather than traditional tabs. For example:</p>
<div class="sourceCode" id="cb68"><pre class="sourceCode markdown"><code class="sourceCode markdown"><span id="cb68-1"><a href="html-document.html#cb68-1" aria-hidden="true" tabindex="-1"></a><span class="fu">## Quarterly Results {.tabset .tabset-fade .tabset-pills}</span></span></code></pre></div>
<div class="figure" style="text-align: center"><span style="display:block;" id="fig:tabset"></span>
<img src="images/tabset.png" alt="Traditional tabs and pill tabs on an HTML page." width="50%" />
<p class="caption">
FIGURE 3.1: Traditional tabs and pill tabs on an HTML page.
</p>
</div>
</div>
<div id="appearance-and-style" class="section level3 hasAnchor" number="3.1.4">
<h3><span class="header-section-number">3.1.4</span> Appearance and style<a href="html-document.html#appearance-and-style" class="anchor-section" aria-label="Anchor link to header"></a></h3>
<p>There are several options that control the appearance of HTML documents:</p>
<ul>
<li><p><code>theme</code> specifies the Bootstrap theme to use for the page (themes are drawn from the <a href="https://bootswatch.com/3/">Bootswatch</a> theme library). Valid themes include default, bootstrap, cerulean, cosmo, darkly, flatly, journal, lumen, paper, readable, sandstone, simplex, spacelab, united, and yeti. Pass <code>null</code> for no theme (in this case you can use the <code>css</code> parameter to add your own styles).</p></li>
<li><p><code>highlight</code> specifies the syntax highlighting style. Supported styles include <code>default</code>, <code>tango</code>, <code>pygments</code>, <code>kate</code>, <code>monochrome</code>, <code>espresso</code>, <code>zenburn</code>, <code>haddock</code>, <code>breezedark</code>, and <code>textmate</code>. Pass <code>null</code> to prevent syntax highlighting.</p></li>
<li><p><code>smart</code> indicates whether to produce typographically correct output, converting straight quotes to curly quotes, <code>---</code> to em-dashes, <code>--</code> to en-dashes, and <code>...</code> to ellipses. Note that <code>smart</code> is enabled by default.</p></li>
</ul>
<p>For example:</p>
<div class="sourceCode" id="cb69"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb69-1"><a href="html-document.html#cb69-1" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span>
<span id="cb69-2"><a href="html-document.html#cb69-2" aria-hidden="true" tabindex="-1"></a><span class="fu">title</span><span class="kw">:</span><span class="at"> </span><span class="st">&quot;Habits&quot;</span></span>
<span id="cb69-3"><a href="html-document.html#cb69-3" aria-hidden="true" tabindex="-1"></a><span class="fu">output</span><span class="kw">:</span></span>
<span id="cb69-4"><a href="html-document.html#cb69-4" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">html_document</span><span class="kw">:</span></span>
<span id="cb69-5"><a href="html-document.html#cb69-5" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">theme</span><span class="kw">:</span><span class="at"> united</span></span>
<span id="cb69-6"><a href="html-document.html#cb69-6" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">highlight</span><span class="kw">:</span><span class="at"> tango</span></span>
<span id="cb69-7"><a href="html-document.html#cb69-7" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span></code></pre></div>
<div id="custom-css" class="section level4 hasAnchor" number="3.1.4.1">
<h4><span class="header-section-number">3.1.4.1</span> Custom CSS<a href="html-document.html#custom-css" class="anchor-section" aria-label="Anchor link to header"></a></h4>
<p>You can add your own CSS to an HTML document using the <code>css</code> option:</p>
<div class="sourceCode" id="cb70"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb70-1"><a href="html-document.html#cb70-1" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span>
<span id="cb70-2"><a href="html-document.html#cb70-2" aria-hidden="true" tabindex="-1"></a><span class="fu">title</span><span class="kw">:</span><span class="at"> </span><span class="st">&quot;Habits&quot;</span></span>
<span id="cb70-3"><a href="html-document.html#cb70-3" aria-hidden="true" tabindex="-1"></a><span class="fu">output</span><span class="kw">:</span></span>
<span id="cb70-4"><a href="html-document.html#cb70-4" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">html_document</span><span class="kw">:</span></span>
<span id="cb70-5"><a href="html-document.html#cb70-5" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">css</span><span class="kw">:</span><span class="at"> styles.css</span></span>
<span id="cb70-6"><a href="html-document.html#cb70-6" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span></code></pre></div>
<p>If you want to provide all of the styles for the document from your own CSS you set the <code>theme</code> (and potentially <code>highlight</code>) to <code>null</code>:</p>
<div class="sourceCode" id="cb71"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb71-1"><a href="html-document.html#cb71-1" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span>
<span id="cb71-2"><a href="html-document.html#cb71-2" aria-hidden="true" tabindex="-1"></a><span class="fu">title</span><span class="kw">:</span><span class="at"> </span><span class="st">&quot;Habits&quot;</span></span>
<span id="cb71-3"><a href="html-document.html#cb71-3" aria-hidden="true" tabindex="-1"></a><span class="fu">output</span><span class="kw">:</span></span>
<span id="cb71-4"><a href="html-document.html#cb71-4" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">html_document</span><span class="kw">:</span></span>
<span id="cb71-5"><a href="html-document.html#cb71-5" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">theme</span><span class="kw">:</span><span class="at"> </span><span class="ch">null</span></span>
<span id="cb71-6"><a href="html-document.html#cb71-6" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">highlight</span><span class="kw">:</span><span class="at"> </span><span class="ch">null</span></span>
<span id="cb71-7"><a href="html-document.html#cb71-7" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">css</span><span class="kw">:</span><span class="at"> styles.css</span></span>
<span id="cb71-8"><a href="html-document.html#cb71-8" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span></code></pre></div>
<p>You can also target specific sections of documents with custom CSS by adding ids or classes to section headers within your document. For example the following section header:</p>
<div class="sourceCode" id="cb72"><pre class="sourceCode markdown"><code class="sourceCode markdown"><span id="cb72-1"><a href="html-document.html#cb72-1" aria-hidden="true" tabindex="-1"></a><span class="fu">## Next Steps {#nextsteps .emphasized}</span></span></code></pre></div>
<p>Would enable you to apply CSS to all of its content using either of the following CSS selectors:</p>
<div class="sourceCode" id="cb73"><pre class="sourceCode css"><code class="sourceCode css"><span id="cb73-1"><a href="html-document.html#cb73-1" aria-hidden="true" tabindex="-1"></a><span class="pp">#nextsteps</span> {</span>
<span id="cb73-2"><a href="html-document.html#cb73-2" aria-hidden="true" tabindex="-1"></a>   <span class="kw">color</span>: <span class="cn">blue</span><span class="op">;</span></span>
<span id="cb73-3"><a href="html-document.html#cb73-3" aria-hidden="true" tabindex="-1"></a>}</span>
<span id="cb73-4"><a href="html-document.html#cb73-4" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb73-5"><a href="html-document.html#cb73-5" aria-hidden="true" tabindex="-1"></a><span class="fu">.emphasized</span> {</span>
<span id="cb73-6"><a href="html-document.html#cb73-6" aria-hidden="true" tabindex="-1"></a>   <span class="kw">font-size</span>: <span class="dv">1.2</span><span class="dt">em</span><span class="op">;</span></span>
<span id="cb73-7"><a href="html-document.html#cb73-7" aria-hidden="true" tabindex="-1"></a>}</span></code></pre></div>
</div>
</div>
<div id="figure-options" class="section level3 hasAnchor" number="3.1.5">
<h3><span class="header-section-number">3.1.5</span> Figure options<a href="html-document.html#figure-options" class="anchor-section" aria-label="Anchor link to header"></a></h3>
<p>There are a number of options that affect the output of figures within HTML documents:</p>
<ul>
<li><p><code>fig_width</code> and <code>fig_height</code> can be used to control the default figure width and height (7x5 is used by default).</p></li>
<li><p><code>fig_retina</code> specifies the scaling to perform for retina displays (defaults to 2, which currently works for all widely used retina displays). Set to <code>null</code> to prevent retina scaling.</p></li>
<li><p><code>fig_caption</code> controls whether figures are rendered with captions.</p></li>
<li><p><code>dev</code> controls the graphics device used to render figures (defaults to <code>png</code>).</p></li>
</ul>
<p>For example:</p>
<div class="sourceCode" id="cb74"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb74-1"><a href="html-document.html#cb74-1" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span>
<span id="cb74-2"><a href="html-document.html#cb74-2" aria-hidden="true" tabindex="-1"></a><span class="fu">title</span><span class="kw">:</span><span class="at"> </span><span class="st">&quot;Habits&quot;</span></span>
<span id="cb74-3"><a href="html-document.html#cb74-3" aria-hidden="true" tabindex="-1"></a><span class="fu">output</span><span class="kw">:</span></span>
<span id="cb74-4"><a href="html-document.html#cb74-4" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">html_document</span><span class="kw">:</span></span>
<span id="cb74-5"><a href="html-document.html#cb74-5" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">fig_width</span><span class="kw">:</span><span class="at"> </span><span class="dv">7</span></span>
<span id="cb74-6"><a href="html-document.html#cb74-6" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">fig_height</span><span class="kw">:</span><span class="at"> </span><span class="dv">6</span></span>
<span id="cb74-7"><a href="html-document.html#cb74-7" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">fig_caption</span><span class="kw">:</span><span class="at"> </span><span class="ch">true</span></span>
<span id="cb74-8"><a href="html-document.html#cb74-8" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span></code></pre></div>
</div>
<div id="data-frame-printing" class="section level3 hasAnchor" number="3.1.6">
<h3><span class="header-section-number">3.1.6</span> Data frame printing<a href="html-document.html#data-frame-printing" class="anchor-section" aria-label="Anchor link to header"></a></h3>
<p>You can enhance the default display of data frames via the <code>df_print</code> option. Valid values are shown in Table <a href="html-document.html#tab:df-print">3.1</a>.</p>
<table>
<caption><span id="tab:df-print">TABLE 3.1: </span> The possible values of the <code>df_print</code> option for the <code>html_document</code> format.</caption>
<thead>
<tr class="header">
<th>Option</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>default</td>
<td>Call the <code>print.data.frame</code> generic method</td>
</tr>
<tr class="even">
<td>kable</td>
<td>Use the <code>knitr::kable</code> function</td>
</tr>
<tr class="odd">
<td>tibble</td>
<td>Use the <code>tibble::print.tbl_df</code> function</td>
</tr>
<tr class="even">
<td>paged</td>
<td>Use <code>rmarkdown::paged_table</code> to create a pageable table</td>
</tr>
<tr class="odd">
<td>A custom function</td>
<td>Use the function to create the table</td>
</tr>
</tbody>
</table>
<div id="paged-printing" class="section level4 hasAnchor" number="3.1.6.1">
<h4><span class="header-section-number">3.1.6.1</span> Paged printing<a href="html-document.html#paged-printing" class="anchor-section" aria-label="Anchor link to header"></a></h4>
<p>When the <code>df_print</code> option is set to <code>paged</code>, tables are printed as HTML tables with support for pagination over rows and columns. For instance (see Figure <a href="html-document.html#fig:paged">3.2</a>):</p>
<div class="sourceCode" id="cb75"><pre class="sourceCode markdown"><code class="sourceCode markdown"><span id="cb75-1"><a href="html-document.html#cb75-1" aria-hidden="true" tabindex="-1"></a><span class="co">---</span></span>
<span id="cb75-2"><a href="html-document.html#cb75-2" aria-hidden="true" tabindex="-1"></a><span class="an">title:</span><span class="co"> &quot;Motor Trend Car Road Tests&quot;</span></span>
<span id="cb75-3"><a href="html-document.html#cb75-3" aria-hidden="true" tabindex="-1"></a><span class="an">output:</span></span>
<span id="cb75-4"><a href="html-document.html#cb75-4" aria-hidden="true" tabindex="-1"></a><span class="co">  html_document:</span></span>
<span id="cb75-5"><a href="html-document.html#cb75-5" aria-hidden="true" tabindex="-1"></a><span class="co">    df_print: paged</span></span>
<span id="cb75-6"><a href="html-document.html#cb75-6" aria-hidden="true" tabindex="-1"></a><span class="co">---</span></span>
<span id="cb75-7"><a href="html-document.html#cb75-7" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb75-8"><a href="html-document.html#cb75-8" aria-hidden="true" tabindex="-1"></a><span class="in">```{r}</span></span>
<span id="cb75-9"><a href="html-document.html#cb75-9" aria-hidden="true" tabindex="-1"></a><span class="in">mtcars</span></span>
<span id="cb75-10"><a href="html-document.html#cb75-10" aria-hidden="true" tabindex="-1"></a><span class="in">```</span></span></code></pre></div>
<div class="figure"><span style="display:block;" id="fig:paged"></span>
<img src="images/paged.png" alt="A paged table in the HTML output document." width="100%" />
<p class="caption">
FIGURE 3.2: A paged table in the HTML output document.
</p>
</div>
<p>Table <a href="html-document.html#tab:paged">3.2</a> shows the available options for paged tables.</p>
<table>
<caption><span id="tab:paged">TABLE 3.2: </span> The options for paged HTML tables.</caption>
<thead>
<tr class="header">
<th>Option</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>max.print</td>
<td>The number of rows to print.</td>
</tr>
<tr class="even">
<td>rows.print</td>
<td>The number of rows to display.</td>
</tr>
<tr class="odd">
<td>cols.print</td>
<td>The number of columns to display.</td>
</tr>
<tr class="even">
<td>cols.min.print</td>
<td>The minimum number of columns to display.</td>
</tr>
<tr class="odd">
<td>pages.print</td>
<td>The number of pages to display under page navigation.</td>
</tr>
<tr class="even">
<td>paged.print</td>
<td>When set to <code>FALSE</code> turns off paged tables.</td>
</tr>
<tr class="odd">
<td>rownames.print</td>
<td>When set to <code>FALSE</code> turns off row names.</td>
</tr>
</tbody>
</table>
<p>These options are specified in each chunk like below:</p>
<div class="sourceCode" id="cb76"><pre class="sourceCode markdown"><code class="sourceCode markdown"><span id="cb76-1"><a href="html-document.html#cb76-1" aria-hidden="true" tabindex="-1"></a><span class="in">```{r cols.print=3, rows.print=3}</span></span>
<span id="cb76-2"><a href="html-document.html#cb76-2" aria-hidden="true" tabindex="-1"></a><span class="in">mtcars</span></span>
<span id="cb76-3"><a href="html-document.html#cb76-3" aria-hidden="true" tabindex="-1"></a><span class="in">```</span></span></code></pre></div>
</div>
<div id="custom-fun-dfprint" class="section level4 hasAnchor" number="3.1.6.2">
<h4><span class="header-section-number">3.1.6.2</span> Custom function<a href="html-document.html#custom-fun-dfprint" class="anchor-section" aria-label="Anchor link to header"></a></h4>
<p>The <code>df_print</code> option can also take an arbitrary function to create the table in the output document. This function must output in the correct format according to the output used.</p>
<p>For example,</p>
<div class="sourceCode" id="cb77"><pre class="sourceCode r"><code class="sourceCode r"><span id="cb77-1"><a href="html-document.html#cb77-1" aria-hidden="true" tabindex="-1"></a>rmarkdown<span class="sc">::</span><span class="fu">html_document</span>(<span class="at">df_print =</span> knitr<span class="sc">::</span>kable)</span></code></pre></div>
<p>is the equivalent to using the method <code>"kable"</code></p>
<div class="sourceCode" id="cb78"><pre class="sourceCode r"><code class="sourceCode r"><span id="cb78-1"><a href="html-document.html#cb78-1" aria-hidden="true" tabindex="-1"></a>rmarkdown<span class="sc">::</span><span class="fu">html_document</span>(<span class="at">df_print =</span> <span class="st">&quot;kable&quot;</span>)</span></code></pre></div>
<p>To use a custom function in <code>df_print</code> within the YAML header, the tag <code>!expr</code> must be used so the R expression after it will be evaluated. See the <code>eval.expr</code> argument on the help page <code>?yaml::yaml.load</code> for details.</p>
<div class="sourceCode" id="cb79"><pre class="sourceCode markdown"><code class="sourceCode markdown"><span id="cb79-1"><a href="html-document.html#cb79-1" aria-hidden="true" tabindex="-1"></a><span class="co">---</span></span>
<span id="cb79-2"><a href="html-document.html#cb79-2" aria-hidden="true" tabindex="-1"></a><span class="an">title:</span><span class="co"> &quot;Motor Trend Car Road Tests&quot;</span></span>
<span id="cb79-3"><a href="html-document.html#cb79-3" aria-hidden="true" tabindex="-1"></a><span class="an">output:</span></span>
<span id="cb79-4"><a href="html-document.html#cb79-4" aria-hidden="true" tabindex="-1"></a><span class="co">  html_document:</span></span>
<span id="cb79-5"><a href="html-document.html#cb79-5" aria-hidden="true" tabindex="-1"></a><span class="co">    df_print: !expr pander::pander </span></span>
<span id="cb79-6"><a href="html-document.html#cb79-6" aria-hidden="true" tabindex="-1"></a><span class="co">---</span></span>
<span id="cb79-7"><a href="html-document.html#cb79-7" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb79-8"><a href="html-document.html#cb79-8" aria-hidden="true" tabindex="-1"></a><span class="in">```{r}</span></span>
<span id="cb79-9"><a href="html-document.html#cb79-9" aria-hidden="true" tabindex="-1"></a><span class="in">mtcars</span></span>
<span id="cb79-10"><a href="html-document.html#cb79-10" aria-hidden="true" tabindex="-1"></a><span class="in">```</span></span></code></pre></div>
</div>
</div>
<div id="code-folding" class="section level3 hasAnchor" number="3.1.7">
<h3><span class="header-section-number">3.1.7</span> Code folding<a href="html-document.html#code-folding" class="anchor-section" aria-label="Anchor link to header"></a></h3>
<p>When the <strong>knitr</strong> chunk option <code>echo = TRUE</code> is specified (the default behavior), the R source code within chunks is included within the rendered document. In some cases, it may be appropriate to exclude code entirely (<code>echo = FALSE</code>) but in other cases you might want the code to be available but not visible by default.</p>
<p>The <code>code_folding: hide</code> option enables you to include R code but have it hidden by default. Users can then choose to show hidden R code chunks either individually or document wide. For example:</p>
<div class="sourceCode" id="cb80"><pre class="sourceCode markdown"><code class="sourceCode markdown"><span id="cb80-1"><a href="html-document.html#cb80-1" aria-hidden="true" tabindex="-1"></a><span class="co">---</span></span>
<span id="cb80-2"><a href="html-document.html#cb80-2" aria-hidden="true" tabindex="-1"></a><span class="an">title:</span><span class="co"> &quot;Habits&quot;</span></span>
<span id="cb80-3"><a href="html-document.html#cb80-3" aria-hidden="true" tabindex="-1"></a><span class="an">output:</span></span>
<span id="cb80-4"><a href="html-document.html#cb80-4" aria-hidden="true" tabindex="-1"></a><span class="co">  html_document:</span></span>
<span id="cb80-5"><a href="html-document.html#cb80-5" aria-hidden="true" tabindex="-1"></a><span class="co">    code_folding: hide</span></span>
<span id="cb80-6"><a href="html-document.html#cb80-6" aria-hidden="true" tabindex="-1"></a><span class="co">---</span></span></code></pre></div>
<p>You can specify <code>code_folding: show</code> to still show all R code by default but then allow users to hide the code if they wish.</p>
</div>
<div id="mathjax-equations" class="section level3 hasAnchor" number="3.1.8">
<h3><span class="header-section-number">3.1.8</span> MathJax equations<a href="html-document.html#mathjax-equations" class="anchor-section" aria-label="Anchor link to header"></a></h3>
<p>By default, <a href="https://www.mathjax.org">MathJax</a> scripts are included in HTML documents for rendering LaTeX and MathML equations. You can use the <code>mathjax</code> option to control how MathJax is included:</p>
<ul>
<li><p>Specify <code>"default"</code> to use an HTTPS URL from a CDN host (currently provided by RStudio).</p></li>
<li><p>Specify <code>"local"</code> to use a local version of MathJax (which is copied into the output directory). Note that when using <code>"local"</code> you also need to set the <code>self_contained</code> option to <code>false</code>.</p></li>
<li><p>Specify an alternate URL to load MathJax from another location.</p></li>
<li><p>Specify <code>null</code> to exclude MathJax entirely.</p></li>
</ul>
<p>For example, to use a local copy of MathJax:</p>
<div class="sourceCode" id="cb81"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb81-1"><a href="html-document.html#cb81-1" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span>
<span id="cb81-2"><a href="html-document.html#cb81-2" aria-hidden="true" tabindex="-1"></a><span class="fu">title</span><span class="kw">:</span><span class="at"> </span><span class="st">&quot;Habits&quot;</span></span>
<span id="cb81-3"><a href="html-document.html#cb81-3" aria-hidden="true" tabindex="-1"></a><span class="fu">output</span><span class="kw">:</span></span>
<span id="cb81-4"><a href="html-document.html#cb81-4" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">html_document</span><span class="kw">:</span></span>
<span id="cb81-5"><a href="html-document.html#cb81-5" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">mathjax</span><span class="kw">:</span><span class="at"> local</span></span>
<span id="cb81-6"><a href="html-document.html#cb81-6" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">self_contained</span><span class="kw">:</span><span class="at"> </span><span class="ch">false</span></span>
<span id="cb81-7"><a href="html-document.html#cb81-7" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span></code></pre></div>
<p>To use a self-hosted copy of MathJax:</p>
<div class="sourceCode" id="cb82"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb82-1"><a href="html-document.html#cb82-1" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span>
<span id="cb82-2"><a href="html-document.html#cb82-2" aria-hidden="true" tabindex="-1"></a><span class="fu">title</span><span class="kw">:</span><span class="at"> </span><span class="st">&quot;Habits&quot;</span></span>
<span id="cb82-3"><a href="html-document.html#cb82-3" aria-hidden="true" tabindex="-1"></a><span class="fu">output</span><span class="kw">:</span></span>
<span id="cb82-4"><a href="html-document.html#cb82-4" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">html_document</span><span class="kw">:</span></span>
<span id="cb82-5"><a href="html-document.html#cb82-5" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">mathjax</span><span class="kw">:</span><span class="at"> </span><span class="st">&quot;http://example.com/MathJax.js&quot;</span></span>
<span id="cb82-6"><a href="html-document.html#cb82-6" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span></code></pre></div>
<p>To exclude MathJax entirely:</p>
<div class="sourceCode" id="cb83"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb83-1"><a href="html-document.html#cb83-1" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span>
<span id="cb83-2"><a href="html-document.html#cb83-2" aria-hidden="true" tabindex="-1"></a><span class="fu">title</span><span class="kw">:</span><span class="at"> </span><span class="st">&quot;Habits&quot;</span></span>
<span id="cb83-3"><a href="html-document.html#cb83-3" aria-hidden="true" tabindex="-1"></a><span class="fu">output</span><span class="kw">:</span></span>
<span id="cb83-4"><a href="html-document.html#cb83-4" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">html_document</span><span class="kw">:</span></span>
<span id="cb83-5"><a href="html-document.html#cb83-5" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">mathjax</span><span class="kw">:</span><span class="at"> </span><span class="ch">null</span></span>
<span id="cb83-6"><a href="html-document.html#cb83-6" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span></code></pre></div>
</div>
<div id="document-dependencies" class="section level3 hasAnchor" number="3.1.9">
<h3><span class="header-section-number">3.1.9</span> Document dependencies<a href="html-document.html#document-dependencies" class="anchor-section" aria-label="Anchor link to header"></a></h3>
<p>By default, R Markdown produces standalone HTML files with no external dependencies, using <code>data:</code> URIs to incorporate the contents of linked scripts, stylesheets, images, and videos. This means you can share or publish the file just like you share Office documents or PDFs. If you would rather keep dependencies in external files, you can specify <code>self_contained: false</code>. For example:</p>
<div class="sourceCode" id="cb84"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb84-1"><a href="html-document.html#cb84-1" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span>
<span id="cb84-2"><a href="html-document.html#cb84-2" aria-hidden="true" tabindex="-1"></a><span class="fu">title</span><span class="kw">:</span><span class="at"> </span><span class="st">&quot;Habits&quot;</span></span>
<span id="cb84-3"><a href="html-document.html#cb84-3" aria-hidden="true" tabindex="-1"></a><span class="fu">output</span><span class="kw">:</span></span>
<span id="cb84-4"><a href="html-document.html#cb84-4" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">html_document</span><span class="kw">:</span></span>
<span id="cb84-5"><a href="html-document.html#cb84-5" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">self_contained</span><span class="kw">:</span><span class="at"> </span><span class="ch">false</span></span>
<span id="cb84-6"><a href="html-document.html#cb84-6" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span></code></pre></div>
<p>Note that even for self-contained documents, MathJax is still loaded externally (this is necessary because of its big size). If you want to serve MathJax locally, you should specify <code>mathjax: local</code> and <code>self_contained: false</code>.</p>
<p>One common reason to keep dependencies external is for serving R Markdown documents from a website (external dependencies can be cached separately by browsers, leading to faster page load times). In the case of serving multiple R Markdown documents you may also want to consolidate dependent library files (e.g. Bootstrap, and MathJax, etc.) into a single directory shared by multiple documents. You can use the <code>lib_dir</code> option to do this. For example:</p>
<div class="sourceCode" id="cb85"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb85-1"><a href="html-document.html#cb85-1" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span>
<span id="cb85-2"><a href="html-document.html#cb85-2" aria-hidden="true" tabindex="-1"></a><span class="fu">title</span><span class="kw">:</span><span class="at"> </span><span class="st">&quot;Habits&quot;</span></span>
<span id="cb85-3"><a href="html-document.html#cb85-3" aria-hidden="true" tabindex="-1"></a><span class="fu">output</span><span class="kw">:</span></span>
<span id="cb85-4"><a href="html-document.html#cb85-4" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">html_document</span><span class="kw">:</span></span>
<span id="cb85-5"><a href="html-document.html#cb85-5" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">self_contained</span><span class="kw">:</span><span class="at"> </span><span class="ch">false</span></span>
<span id="cb85-6"><a href="html-document.html#cb85-6" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">lib_dir</span><span class="kw">:</span><span class="at"> libs</span></span>
<span id="cb85-7"><a href="html-document.html#cb85-7" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span></code></pre></div>
</div>
<div id="advanced-customization" class="section level3 hasAnchor" number="3.1.10">
<h3><span class="header-section-number">3.1.10</span> Advanced customization<a href="html-document.html#advanced-customization" class="anchor-section" aria-label="Anchor link to header"></a></h3>
<div id="keeping-markdown" class="section level4 hasAnchor" number="3.1.10.1">
<h4><span class="header-section-number">3.1.10.1</span> Keeping Markdown<a href="html-document.html#keeping-markdown" class="anchor-section" aria-label="Anchor link to header"></a></h4>
<p>When <strong>knitr</strong> processes an R Markdown input file, it creates a Markdown (<code>*.md</code>) file that is subsequently transformed into HTML by Pandoc. If you want to keep a copy of the Markdown file after rendering, you can do so using the <code>keep_md</code> option:</p>
<div class="sourceCode" id="cb86"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb86-1"><a href="html-document.html#cb86-1" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span>
<span id="cb86-2"><a href="html-document.html#cb86-2" aria-hidden="true" tabindex="-1"></a><span class="fu">title</span><span class="kw">:</span><span class="at"> </span><span class="st">&quot;Habits&quot;</span></span>
<span id="cb86-3"><a href="html-document.html#cb86-3" aria-hidden="true" tabindex="-1"></a><span class="fu">output</span><span class="kw">:</span></span>
<span id="cb86-4"><a href="html-document.html#cb86-4" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">html_document</span><span class="kw">:</span></span>
<span id="cb86-5"><a href="html-document.html#cb86-5" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">keep_md</span><span class="kw">:</span><span class="at"> </span><span class="ch">true</span></span>
<span id="cb86-6"><a href="html-document.html#cb86-6" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span></code></pre></div>
</div>
<div id="includes" class="section level4 hasAnchor" number="3.1.10.2">
<h4><span class="header-section-number">3.1.10.2</span> Includes<a href="html-document.html#includes" class="anchor-section" aria-label="Anchor link to header"></a></h4>
<p>You can do more advanced customization of output by including additional HTML content or by replacing the core Pandoc template entirely. To include content in the document header or before/after the document body, you use the <code>includes</code> option as follows:</p>
<div class="sourceCode" id="cb87"><pre class="sourceCode markdown"><code class="sourceCode markdown"><span id="cb87-1"><a href="html-document.html#cb87-1" aria-hidden="true" tabindex="-1"></a><span class="co">---</span></span>
<span id="cb87-2"><a href="html-document.html#cb87-2" aria-hidden="true" tabindex="-1"></a><span class="an">title:</span><span class="co"> &quot;Habits&quot;</span></span>
<span id="cb87-3"><a href="html-document.html#cb87-3" aria-hidden="true" tabindex="-1"></a><span class="an">output:</span></span>
<span id="cb87-4"><a href="html-document.html#cb87-4" aria-hidden="true" tabindex="-1"></a><span class="co">  html_document:</span></span>
<span id="cb87-5"><a href="html-document.html#cb87-5" aria-hidden="true" tabindex="-1"></a><span class="co">    includes:</span></span>
<span id="cb87-6"><a href="html-document.html#cb87-6" aria-hidden="true" tabindex="-1"></a><span class="co">      in_header: header.html</span></span>
<span id="cb87-7"><a href="html-document.html#cb87-7" aria-hidden="true" tabindex="-1"></a><span class="co">      before_body: doc_prefix.html</span></span>
<span id="cb87-8"><a href="html-document.html#cb87-8" aria-hidden="true" tabindex="-1"></a><span class="co">      after_body: doc_suffix.html</span></span>
<span id="cb87-9"><a href="html-document.html#cb87-9" aria-hidden="true" tabindex="-1"></a><span class="co">---</span></span></code></pre></div>
</div>
<div id="custom-templates" class="section level4 hasAnchor" number="3.1.10.3">
<h4><span class="header-section-number">3.1.10.3</span> Custom templates<a href="html-document.html#custom-templates" class="anchor-section" aria-label="Anchor link to header"></a></h4>
<p>You can also replace the underlying Pandoc template using the <code>template</code> option:</p>
<div class="sourceCode" id="cb88"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb88-1"><a href="html-document.html#cb88-1" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span>
<span id="cb88-2"><a href="html-document.html#cb88-2" aria-hidden="true" tabindex="-1"></a><span class="fu">title</span><span class="kw">:</span><span class="at"> </span><span class="st">&quot;Habits&quot;</span></span>
<span id="cb88-3"><a href="html-document.html#cb88-3" aria-hidden="true" tabindex="-1"></a><span class="fu">output</span><span class="kw">:</span></span>
<span id="cb88-4"><a href="html-document.html#cb88-4" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">html_document</span><span class="kw">:</span></span>
<span id="cb88-5"><a href="html-document.html#cb88-5" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">template</span><span class="kw">:</span><span class="at"> quarterly_report.html</span></span>
<span id="cb88-6"><a href="html-document.html#cb88-6" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span></code></pre></div>
<p>Consult the documentation on <a href="http://pandoc.org/MANUAL.html#templates">Pandoc templates</a> for additional details on templates. You can also study the <a href="https://github.com/jgm/pandoc-templates/">default HTML template <code>default.html5</code></a> as an example.</p>
</div>
<div id="markdown-extensions" class="section level4 hasAnchor" number="3.1.10.4">
<h4><span class="header-section-number">3.1.10.4</span> Markdown extensions<a href="html-document.html#markdown-extensions" class="anchor-section" aria-label="Anchor link to header"></a></h4>
<p>By default, R Markdown is defined as all Pandoc Markdown extensions with the following tweaks for backward compatibility with the old <strong>markdown</strong> package <span class="citation">(<a href="#ref-R-markdown" role="doc-biblioref">Xie, Allaire, and Horner 2023</a>)</span>:</p>
<pre><code>+autolink_bare_uris
+tex_math_single_backslash</code></pre>
<p>You can enable or disable Markdown extensions using the <code>md_extensions</code> option (you preface an option with <code>-</code> to disable and <code>+</code> to enable it). For example:</p>
<div class="sourceCode" id="cb90"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb90-1"><a href="html-document.html#cb90-1" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span>
<span id="cb90-2"><a href="html-document.html#cb90-2" aria-hidden="true" tabindex="-1"></a><span class="fu">title</span><span class="kw">:</span><span class="at"> </span><span class="st">&quot;Habits&quot;</span></span>
<span id="cb90-3"><a href="html-document.html#cb90-3" aria-hidden="true" tabindex="-1"></a><span class="fu">output</span><span class="kw">:</span></span>
<span id="cb90-4"><a href="html-document.html#cb90-4" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">html_document</span><span class="kw">:</span></span>
<span id="cb90-5"><a href="html-document.html#cb90-5" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">md_extensions</span><span class="kw">:</span><span class="at"> -autolink_bare_uris+hard_line_breaks</span></span>
<span id="cb90-6"><a href="html-document.html#cb90-6" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span></code></pre></div>
<p>The above would disable the <code>autolink_bare_uris</code> extension, and enable the <code>hard_line_breaks</code> extension.</p>
<p>For more on available markdown extensions see the <a href="http://pandoc.org/MANUAL.html#pandocs-markdown">Pandoc Markdown specification</a>.</p>
</div>
<div id="pandoc-arguments" class="section level4 hasAnchor" number="3.1.10.5">
<h4><span class="header-section-number">3.1.10.5</span> Pandoc arguments<a href="html-document.html#pandoc-arguments" class="anchor-section" aria-label="Anchor link to header"></a></h4>
<p>If there are Pandoc features that you want to use but lack equivalents in the YAML options described above, you can still use them by passing custom <code>pandoc_args</code>. For example:</p>
<div class="sourceCode" id="cb91"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb91-1"><a href="html-document.html#cb91-1" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span>
<span id="cb91-2"><a href="html-document.html#cb91-2" aria-hidden="true" tabindex="-1"></a><span class="fu">title</span><span class="kw">:</span><span class="at"> </span><span class="st">&quot;Habits&quot;</span></span>
<span id="cb91-3"><a href="html-document.html#cb91-3" aria-hidden="true" tabindex="-1"></a><span class="fu">output</span><span class="kw">:</span></span>
<span id="cb91-4"><a href="html-document.html#cb91-4" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">html_document</span><span class="kw">:</span></span>
<span id="cb91-5"><a href="html-document.html#cb91-5" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">pandoc_args</span><span class="kw">:</span><span class="at"> </span><span class="kw">[</span></span>
<span id="cb91-6"><a href="html-document.html#cb91-6" aria-hidden="true" tabindex="-1"></a><span class="at">      </span><span class="st">&quot;--title-prefix&quot;</span><span class="kw">,</span><span class="at"> </span><span class="st">&quot;Foo&quot;</span><span class="kw">,</span></span>
<span id="cb91-7"><a href="html-document.html#cb91-7" aria-hidden="true" tabindex="-1"></a><span class="at">      </span><span class="st">&quot;--id-prefix&quot;</span><span class="kw">,</span><span class="at"> </span><span class="st">&quot;Bar&quot;</span></span>
<span id="cb91-8"><a href="html-document.html#cb91-8" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="kw">]</span></span>
<span id="cb91-9"><a href="html-document.html#cb91-9" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span></code></pre></div>
<p>Documentation on all available pandoc arguments can be found in the <a href="http://pandoc.org/MANUAL.html#options">Pandoc User Guide</a>.</p>
</div>
</div>
<div id="shared-options" class="section level3 hasAnchor" number="3.1.11">
<h3><span class="header-section-number">3.1.11</span> Shared options<a href="html-document.html#shared-options" class="anchor-section" aria-label="Anchor link to header"></a></h3>
<p>If you want to specify a set of default options to be shared by multiple documents within a directory, you can include a file named <code>_output.yml</code> within the directory. Note that no YAML delimiters (<code>---</code>) or the enclosing <code>output</code> field are used in this file. For example:</p>
<div class="sourceCode" id="cb92"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb92-1"><a href="html-document.html#cb92-1" aria-hidden="true" tabindex="-1"></a><span class="fu">html_document</span><span class="kw">:</span></span>
<span id="cb92-2"><a href="html-document.html#cb92-2" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">self_contained</span><span class="kw">:</span><span class="at"> </span><span class="ch">false</span></span>
<span id="cb92-3"><a href="html-document.html#cb92-3" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">theme</span><span class="kw">:</span><span class="at"> united</span></span>
<span id="cb92-4"><a href="html-document.html#cb92-4" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">highlight</span><span class="kw">:</span><span class="at"> textmate</span></span></code></pre></div>
<p>It should not be written as:</p>
<div class="sourceCode" id="cb93"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb93-1"><a href="html-document.html#cb93-1" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span>
<span id="cb93-2"><a href="html-document.html#cb93-2" aria-hidden="true" tabindex="-1"></a><span class="fu">output</span><span class="kw">:</span></span>
<span id="cb93-3"><a href="html-document.html#cb93-3" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">html_document</span><span class="kw">:</span></span>
<span id="cb93-4"><a href="html-document.html#cb93-4" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">self_contained</span><span class="kw">:</span><span class="at"> </span><span class="ch">false</span></span>
<span id="cb93-5"><a href="html-document.html#cb93-5" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">theme</span><span class="kw">:</span><span class="at"> united</span></span>
<span id="cb93-6"><a href="html-document.html#cb93-6" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">highlight</span><span class="kw">:</span><span class="at"> textmate</span></span>
<span id="cb93-7"><a href="html-document.html#cb93-7" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span></code></pre></div>
<p>All documents located in the same directory as <code>_output.yml</code> will inherit its options. Options defined explicitly within documents will override those specified in the shared options file.</p>
</div>
<div id="html-fragments" class="section level3 hasAnchor" number="3.1.12">
<h3><span class="header-section-number">3.1.12</span> HTML fragments<a href="html-document.html#html-fragments" class="anchor-section" aria-label="Anchor link to header"></a></h3>
<p>If you want to create an HTML fragment rather than a full HTML document, you can use the <code>html_fragment</code> format. For example:</p>
<div class="sourceCode" id="cb94"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb94-1"><a href="html-document.html#cb94-1" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span>
<span id="cb94-2"><a href="html-document.html#cb94-2" aria-hidden="true" tabindex="-1"></a><span class="fu">output</span><span class="kw">:</span><span class="at"> html_fragment</span></span>
<span id="cb94-3"><a href="html-document.html#cb94-3" aria-hidden="true" tabindex="-1"></a><span class="pp">---</span></span></code></pre></div>
<p>Note that HTML fragments are not complete HTML documents. They do not contain the standard header content that HTML documents do (they only contain content in the <code>&lt;body&gt;</code> tags of normal HTML documents). They are intended for inclusion within other web pages or content management systems (like blogs). As such, they do not support features like themes or code highlighting (it is expected that the environment they are ultimately published within handles these things).</p>
</div>
</div>
<h3>References<a href="references.html#references" class="anchor-section" aria-label="Anchor link to header"></a></h3>
<div id="refs" class="references csl-bib-body hanging-indent">
<div id="ref-R-markdown" class="csl-entry">
Xie, Yihui, JJ Allaire, and Jeffrey Horner. 2023. <em>Markdown: Render Markdown with Commonmark</em>. <a href="https://github.com/rstudio/markdown">https://github.com/rstudio/markdown</a>.
</div>
</div>
            </section>

          </div>
        </div>
      </div>
<a href="documents.html" class="navigation navigation-prev " aria-label="Previous page"><i class="fa fa-angle-left"></i></a>
<a href="notebook.html" class="navigation navigation-next " aria-label="Next page"><i class="fa fa-angle-right"></i></a>
    </div>
  </div>
<script src="libs/gitbook/js/app.min.js"></script>
<script src="libs/gitbook/js/clipboard.min.js"></script>
<script src="libs/gitbook/js/plugin-search.js"></script>
<script src="libs/gitbook/js/plugin-sharing.js"></script>
<script src="libs/gitbook/js/plugin-fontsettings.js"></script>
<script src="libs/gitbook/js/plugin-bookdown.js"></script>
<script src="libs/gitbook/js/jquery.highlight.js"></script>
<script src="libs/gitbook/js/plugin-clipboard.js"></script>
<script>
gitbook.require(["gitbook"], function(gitbook) {
gitbook.start({
"sharing": {
"github": true,
"facebook": false,
"twitter": true,
"linkedin": false,
"weibo": false,
"instapaper": false,
"vk": false,
"whatsapp": false,
"all": ["facebook", "twitter", "linkedin", "weibo", "instapaper"]
},
"fontsettings": {
"theme": "white",
"family": "sans",
"size": 2
},
"edit": {
"link": "https://github.com/rstudio/rmarkdown-book/edit/main/03-documents.Rmd",
"text": "Edit"
},
"history": {
"link": null,
"text": null
},
"view": {
"link": null,
"text": null
},
"download": ["rmarkdown.pdf"],
"search": {
"engine": "fuse",
"options": null
},
"toc": {
"collapse": "none"
}
});
});
</script>

<!-- dynamically load mathjax for compatibility with self-contained -->
<script>
  (function () {
    var script = document.createElement("script");
    script.type = "text/javascript";
    var src = "true";
    if (src === "" || src === "true") src = "https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.9/latest.js?config=TeX-MML-AM_CHTML";
    if (location.protocol !== "file:")
      if (/^https?:/.test(src))
        src = src.replace(/^https?:/, '');
    script.src = src;
    document.getElementsByTagName("head")[0].appendChild(script);
  })();
</script>
</body>

</html>