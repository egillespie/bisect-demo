# `git bisect`

`git bisect` is a tool to quickly access a bunch of commits in your repository to interactively find out when a bug was introduced.

This repository contains a simple HTML file with lots of small changes
committed to it to demonstrate how to use `git bisect`.

Oh no, somehow the black text in the HTML is being rendered red! Follow the instructions below to use `git bisect` to interactively traverse this repository's commits and find out which commit introduced the red text.

## Step 1. Clone this repository

``` sh
git clone https://github.com/egillespie/bisect-demo.git
```

## Step 2. Open `index.html` in a browser

Double-click the `index.html` file or drag it to a browser window. See the red text? That just won't do!

Let's find out when that text first changed from black to red.

