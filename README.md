# `git bisect`

`git bisect` is a tool to quickly access a bunch of commits in your repository
to interactively find out when a bug was introduced.

This repository contains a simple HTML file with lots of small changes
committed to it to demonstrate how to use `git bisect`.

Oh no, somehow the black text in the HTML is being rendered red! Follow the
instructions below to use `git bisect` to interactively traverse this
repository's commits and find out which commit introduced the red text.

## Step 1. Clone this repository

``` sh
git clone https://github.com/egillespie/bisect-demo.git
```

## Step 2. Open `index.html` in a browser

Double-click the `index.html` file or drag it to a browser window. See the red
text? That just won't do!

Let's find out when that text first changed from black to red.

## Step 3. Start bisecting commits

``` sh
git bisect start
git bisect bad
git bisect good first-html-commit
```

This starts the bisect search, marks the most recent (`HEAD`) commit as bad, and
marks the first HTML commit (which is conveniently tagged as `first-html-commit`
to avoid having to type a commit ID) as good.

Once these three commands run, you should see some output that resembles this:

~~~
Bisecting: 4 revisions left to test after this (roughly 2 steps)
[8f40c4c4dfb6708122cc7e05437f09b0dbcb5134] Background color
~~~

If you ever need to start over, run `bisect reset`.

## Step 4. Refresh the browser page

The last message in the terminal when the bisect started, "Background color" (or
something similar), is the commit message that is currently checked out and
operating on our computers.

That means if we refresh the browser window, we may not see the same light gray
background and red text color that is present in the `HEAD` commit.

## Step 5. Mark the current commit

After you refresh the browser window, ask "Is the text black?" If it is black,
then the current commit is "good" and if it's red, the current commit is "bad".

If the text is black (good), then run this command:

``` sh
git bisect good
```

If the text is red (bad), then run this command:

``` sh
git bisect bad
```

Regardless of which you choose, the bisect will mark the commit and checkout a
new commit for you to review.

## Step 6. Continue reviewing

Refresh the browser window again and then run one of the commands in Step 5 to
mark the current commit good or bad.

Repeat this step until the terminal shows you something like this:

~~~
9f9986c1192aa209817d6b099252701a312565aa is the first bad commit
commit 9f9986c1192aa209817d6b099252701a312565aa
Author: Erik Gillespie <erik.gillespie@gmail.com>
Date:   Tue Jun 18 16:57:07 2019 -0400

    More contrast

:100644 100644 108acb9114cd8e76bfd0527e993fd6592d1b72d8 e5538b2a20e7d72ef3cf9d66b1dd648d4119c84b M      index.html
~~~

## Step 7. $$$

We now know which commit introduced the red text (spoiler alert, it was
`9f9986c`)! We also know it was Erik Gillespie who made this serious mistake
(tsk tsk).

Now we can checkout this commit, see what happened in the code, why the mistake
might have happened, talk to Erik, and come up with a plan to fix the problem.

## Step 8. Exit the bisect

We're done investigating and need to stop the bisect by running the reset
command:

``` sh
git bisect reset
```

Good work, sleuth. You're a natural!
