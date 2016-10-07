---
layout: post
title: "OCaml with Lablgtk"
description: "Building User Interface with Lablgtk"
date: 2016-10-04
tags: [fyp, ocaml, lablgtk]
comments: false
share: false
---

## Building User Interface with Lablgtk
<b>Lablgtk</b> is an OCaml interface for <b>Gtk</b>, which is a toolkit for writing graphical applications. In this post, we will be looking at how I can make use of <b>lablgtk</b> to write a simple application to try to understand how <b>lablgtk</b> works. 

We will following and covering the key points in this [OCaml tutorial](https://ocaml.org/learn/tutorials/introduction_to_gtk.html), which introduces the basics to writing a simple lablgtk program.

### Compiling a lablgtk program
First, we will look at how we can compile a labgtk using <i>ocamlfind</i>. The following command is an example of how we can compile a simple lablgtk application `simple.ml`:

`ocamlfind ocamlc -g -package lablgtk2 -linkpkg simple.ml -o simple`

With `ocamlfind` and `-linkpkg`, we can do away with including our path to `lablgtk2` in our compilation command. This will help to reduce the chances of encountering a compilation error or any confusion involved in providing the correct directory in which our `lablgtk` lies in.

### Dissecting simple.ml
In this section, we will look at the basics of a lablgtk program with the following program taken from the tutorial.

```ocaml
open GMain
open GdkKeysyms

let locale = GtkMain.Main.init ()

let main () =
  let window = GWindow.window ~width:320 ~height:240
                              ~title:"Simple lablgtk program" () in
  let vbox = GPack.vbox ~packing:window#add () in
  window#connect#destroy ~callback:Main.quit;

  (* Menu bar *)
  let menubar = GMenu.menu_bar ~packing:vbox#pack () in
  let factory = new GMenu.factory menubar in
  let accel_group = factory#accel_group in
  let file_menu = factory#add_submenu "File" in

  (* Button *)
  let button = GButton.button ~label:"+"
                              ~packing:vbox#add () in
  button#connect#clicked ~callback: (fun () -> prerr_endline "Ouch!");


  (* Display the windows and enter Gtk+ main loop *)
  window#add_accel_group accel_group;
  window#show ();
  Main.main ()

let () = main ()
```

After encountering countless compilation errors with other lablgtk examples, for most cases the issue arises with the lack of the following code:

```ocaml
let locale = GtkMain.Main.init ()
```

This line out code is present to initiate a <i>lablgtk</i> program. This line of code is essential for building a lablgtk program and without it we will not be able to compile and build the application.

Next, we will look at <i>widgets</i>, the button widget in particular, in <i>lablgtk</i> in the following block of code:

```ocaml
(* Button *)
let button = GButton.button ~label:"Push me!"
                          ~packing:vbox#add () in
button#connect#clicked ~callback: (fun () -> prerr_endline "Ouch!");
```

Let us focus on this line of code in particular:

```ocaml
button#connect#clicked ~callback: (fun () -> prerr_endline "Ouch!");
```

In the code, we are connecting the <i>button</i> to the <i>clicked</i> signal and then we make a <i>callback</i> to a function which prints a string whenever the button is clicked on. This block of code is important in helping us to understand how to add widgets and functionalities to our application. Referring to the <i>lablgtk</i> documentation, we can observe that, in general, most widgets are to be build in this form and from this example we can then move on to implementing other widgets to build a more robust application.

### Part of a bigger picture
The aim of my FYP is to build web UIs with OCaml which will be modelled after the MVC model that Elm uses. Why then are we learning to build applications with <i>lablgtk</i>? The aim is to first build an application with <i>lablgtk</i> and then look at how we can mirror the MVC model on OCaml to provide the same if not an almost similar model.
