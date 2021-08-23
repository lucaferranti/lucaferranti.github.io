+++
author = "Luca Ferranti"
shortauthor = "L. Ferranti"
jobtitle = "Project Researcher"

mintoclevel = 2
ignore = ["node_modules/", "franklin", "franklin.pub"]

hasplotly = false
hasmermaid = false

# RSS setup
website_title = "Luca Ferranti webpage"
website_descr = "Luca Ferranti webpage"
website_url   = "https://lucaferranti.github.io/"
+++

\newcommand{\callout}[1]{~~~<div class="alert alert-note"><div>~~~#1~~~</div></div>~~~}

\newcommand{\icon}[1]{~~~<i class="fas fa-~~~!#1~~~"></i>~~~}

\newcommand{\elink}[2]{~~~<a href="#2" target=_blank rel=noopener>#1</a>~~~}

\newcommand{\figenv}[3]{
~~~
<figure style="text-align:center;">
<img src="!#2" style="padding:0;#3" alt="#1"/>
<figcaption>#1</figcaption>
</figure>
~~~
}