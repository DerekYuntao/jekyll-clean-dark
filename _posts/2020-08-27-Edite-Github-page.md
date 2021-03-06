---
layout: post
title: "Editing a Github Page"
date: 2020-08-27
description: How to edite a GitHub blog webpage
share: true
tags:
 - Web
---

## Adjust title

In my default template of the GitHub blog, the title of a post weabpage is set to be a hyperlink. Now I don't need the title to be a hyperlink but a pure text, how should I do?

First, we need to find where to modify the code. Since this demand is associated with layouts, thus we enter directory *_layouts* and find a htmml file *post.html*. Yes, here is where to modify the code! In *post.html* we find a line of code as follows.

```html
<h1><a href="{{ page.url | relative_url }}">{{ page.title }}</a></h1>
```
"<a..>...</a>" denotes the hyperlink to page tile. The solution is simple since we just need to delete "<a..>...</a>" to make it a pure text. We can also designate the color of the text.

```html
<h1 style="color: rgb(7, 119, 224)">{{ page.title }}</h1>
```

## Adjust highlight code 

The defual font size of the highlight code is too small. How to make it larger?
Entering `assets\css` and open `syntax.scss`. 
```markdown
.highlight {
  margin-bottom: 1.5em;
  color: $foreground;
  background-color: $background;
  @include rounded(4px);
  pre {
    position: relative;
    margin: 0;
    padding: 1em;
    overflow-x: auto;
    word-wrap: normal;
    border: none;
    white-space: pre;
    background-color: rgb(77, 76, 76);
    color: #ddd !important;
    code {
      white-space: pre;
      color: #ddd;
    }
```

Add two lines to adjust font size: `font-size: .9375em;`

```markdown
.highlight {
  margin-bottom: 1.5em;
  color: $foreground;
  background-color: $background;
  @include rounded(4px);
  pre {
    position: relative;
    margin: 0;
    font-size: 14px;
    padding: 1em;
    overflow-x: auto;
    word-wrap: normal;
    border: none;
    white-space: pre;
    background-color: rgb(77, 76, 76);
    color: #ddd !important;
    code {
      white-space: pre;
      color: #ddd;
      font-size: 14px;
    }
```

Reference: <https://github.com/academicpages/academicpages.github.io/issues/59>


##  Automatically add serial number for titles

Add the following code to a new css file `auto-number-title.css`. Then add the following line to each blog file (.md) to be posted. (i.e. Add a reference from an external style sheet to the .md file)

```markdown
<link rel="stylesheet" type="text/css" href="/jekyll-clean-dark/assets/css/auto-number-title.css"/>
```

```html
h1 { counter-reset: h2counter; }
h2 { counter-reset: h3counter; }
h3 { counter-reset: h4counter; }
h4 { counter-reset: h5counter; }
h5 { counter-reset: h6counter; }
h6 { }
h2:before {
  counter-increment: h2counter;
  content: counter(h2counter) ".\0000a0\0000a0";
}
h3:before {
  counter-increment: h3counter;
  content: counter(h2counter) "."
            counter(h3counter) ".\0000a0\0000a0";
}
h4:before {
  counter-increment: h4counter;
  content: counter(h2counter) "."
            counter(h3counter) "."
            counter(h4counter) ".\0000a0\0000a0";
}
h5:before {
  counter-increment: h5counter;
  content: counter(h2counter) "."
            counter(h3counter) "."
            counter(h4counter) "."
            counter(h5counter) ".\0000a0\0000a0";
}
h6:before {
  counter-increment: h6counter;
  content: counter(h2counter) "."
            counter(h3counter) "."
            counter(h4counter) "."
            counter(h5counter) "."
            counter(h6counter) ".\0000a0\0000a0";
}
```
Reference: <https://yanwei.github.io/misc/markdown-auto-number-title.html>


## Add page view to the blog

<http://ibruce.info/2015/04/04/busuanzi/>

简简单单给个人博客增加访问统计
<https://longzeping.github.io/2018/08/03/%E7%AE%80%E7%AE%80%E5%8D%95%E5%8D%95%E7%BB%99%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%E5%A2%9E%E5%8A%A0%E8%AE%BF%E9%97%AE%E7%BB%9F%E8%AE%A1/>


**Appendix**

    font-size: .625em;            = 10px 
    font-size: .6875em;           = 11px 
    font-size: .75em;             = 12px 
    font-size: .8125em;           = 13px 
    font-size: .875em;            = 14px
    font-size: .9375em;           = 15px
    font-size: 1.0625em;          = 17px
    font-size: 1.125em;           = 18px     
    font-size: 1.188em;           = 19px      
    font-size: 1.25em;            = 20px   
        
    font-size: 1.313em;           = 21px        
    font-size: 1.375em;           = 22px         
    font-size: 1.438em;           = 23px         
    font-size: 1.5em;             = 24px
    font-size: 1.563em;           = 25px         
    font-size: 1.625em;           = 26px          
    font-size: 1.688em;           = 27px         
    font-size: 1.75em;            = 28px         
    font-size: 1.813em;           = 29px          
    font-size: 1.875em;           = 30px  

Last update: 12/04/2020
Last update: 02/15/2021

<link rel="stylesheet" type="text/css" href="/jekyll-clean-dark/assets/css/auto-number-title.css"/>