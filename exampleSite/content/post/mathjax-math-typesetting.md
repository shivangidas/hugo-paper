---
author: Shivangi
title: Math Typesetting using MathJax
date: 2025-06-07
description: A brief guide to setup MathJax
math: true
---

Mathematical notation in a Hugo project can be enabled by using third party JavaScript libraries.

<!--more-->

This example uses [MathJax](https://www.mathjax.org/).

1. Add following to the hugo.toml file

    ```toml
        [markup.goldmark.extensions]
        [markup.goldmark.extensions.passthrough]
            enable = true
            [markup.goldmark.extensions.passthrough.delimiters]
            block = [['\[', '\]'], ['$$', '$$']]
            inline = [['\(', '\)']]
    ```
2. Create a partial under `/layouts/partials/math.html`

    ```html
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>
    <script>
    MathJax = {
        tex: {
        displayMath: [['\\[', '\\]'], ['$$', '$$']],  // block
        inlineMath: [['\\(', '\\)'], ['$', '$']]                  // inline
        },
        loader:{
        load: ['ui/safe']
        },
    };
    </script>
    ```
3. Include the partial in your templates like so:

    ```bash
    {{ if or .Params.math .Site.Params.math }}
    {{ partialCache "math.html" . }}
    {{ end }}
    ```

4. To enable MathJax globally set the parameter `math` to `true` in a project's configuration

5. To enable MathJax on a page include the parameter `math: true` in the page frontmatter

### Examples

Inline math: $\varphi = \dfrac{1+\sqrt5}{2}= 1.6180339887…$

Another inline one: $a^*=x-b^*$

Block math:

$$
 \varphi = 1+\frac{1} {1+\frac{1} {1+\frac{1} {1+\cdots} } }
$$
