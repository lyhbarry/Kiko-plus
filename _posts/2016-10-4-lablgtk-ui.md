---
layout: post
title: "OCaml with Lablgtk"
description: "Building User Interface with Lablgtk"
date: 2016-09-26
tags: [test]
comments: false
share: false
---

## Building User Interface with Lablgtk
<b>Lablgtk</b> is an OCaml interface for <b>Gtk</b>, which is a toolkit for writing graphical applications. In this post, we will be looking at how we can make use of <i>lablgtk</i> to write a simple application to try to understand how <i>lablgtk</i> works.

### Compiling a lablgtk program
First, we will look at how we can compile a labgtk using <i>ocamlfind</i>. The following command is an example of how we can compile a simple lablgtk application `simple.ml`:
`ocamlfind ocamlc -g -package lablgtk2 -linkpkg simple.ml -o simple`
With `ocamlfind` and `-linkpkg`, we can do away with including our path to `lablgtk2` in our compilation command. This will help to reduce the chances of encountering a compilation error or any confusion involved in providing the correct directory in which our `lablgtk` lies in.

