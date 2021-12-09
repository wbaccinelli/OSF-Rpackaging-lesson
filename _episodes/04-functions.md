---
title: "Writing our own functions"
teaching: 0
exercises: 0
questions:
- "How can I add functionality to my package"
objectives:
- "Create a custom package"
keypoints:
- "It is important to think about **what** we want our package to do (_design_) and **how** to do it (_implementation_). We also want to know **why** we need a new package (_avoid reinventing the wheel_)"
- "Functions have to be written in R files in the R folder"
---

So far, we have been playing with the example package that is built-in in `RStudio`.
It only contains a function that says `Hello, world!`.
This is extremely useful to get started, but not very interesting.
In this and the next episodes, we will create our own customized package, which in the previous episode we gave the name of `mysterycoffee`.

## `mysterycoffee`, our virtual coffee room

Our package will try to mitigate a practical problem: social isolation in remote working environments.
We want to create a software solution that simulates the random encounters at the office's coffee machine... when there is no office.
The very first step is to answer three very important questions:

> ## What will our package do?
> We already answered this.
> Our package will simulate random encounters between employees.
{: .callout}
> ## How will we do it?
> After some thinking, we figured out that we can have a function that has the following input and output:
>
> - **Input**: vector of employees' names.
> - **Output**: a two-column matrix, randomly grouping the employees' names into couples.
>
> The output table can be published, say, weekly, and each couple invited to have a videoconference-coffee chat, just as if they had randomly met at the coffee machine.
>
> So this will be our starting point.
> In the next sections we'll write an R function that does exactly this.
>
> Later on we'll see that our original design may face unexpected challenges.
> For instance, what happens if the number of employees is odd?
> 
> FIXME: a diagram / figure can be of great help here
{: .callout}

> ## Are we reinventing the wheel?
> This is also an important question worth investing some time in.
> Can solve our problem with a software solution that someone else already wrote?
>
> Well... if our problem really was to simulate random encounters, the answer is yes.
> There are already solutions for this.
> But our **real** problem is learning how to make R Packages, isn't it?
> So we'll use this problem as a pedagogical example.
{: .callout}

## Getting our hands dirty 

### First step: remove `hello.R`
The next step is to remove the file `hello.R`.
This was just an example file, and we don't need it anymore.

### Second step: edit `DESCRIPTION`
Now that we know what our package is expected to do, it is a perfect moment to edit the `DESCRIPTION` file.

> ## The `DESCRIPTION` file
> Open the `DESCRIPTION` file.
> What do you see here?
>
> Take 5 minutes to edit this file with the information it asks.
> Ignore the `License` field.
> We'll go back to that on episode FIXME.
> > ## Solution
> > After editing, your `DESCRIPTION` file should look similar to:
> >
> > ~~~
> > Package: mysterycoffee
> > Type: Package
> > Title: Simulation of random encounters between couples of persons
> > Version: 0.1.0
> > Author: Pablo Rodriguez-Sanchez
> > Maintainer: Pablo Rodriguez-Sanchez <p.rodriguez-sanchez@esciencecenter.nl>
> > Description: Simulates random encounters between couples of persons
> >     This package was inspired by the need to mitigate social isolation in remote 
> >     working environments. The idea is to simulate random encounters at the office's
> >     coffee machine... when there is no such an office.
> > License: What license is it under?
> > Encoding: UTF-8
> > LazyData: true
> > RoxygenNote: 7.1.1
> > ~~~
> > {: .source}
> {: .solution}
{: .challenge}

### Third step: create a function

We came up with the following prototype function that will do the random grouping:

~~~r
make_groups <- function(names) {
  # Shuffle the names
  names_shuffled <- sample(names)

  # Arrange it as a two-columns matrix
  names_coupled <- matrix(names_shuffled, ncol = 2)

  return(names_coupled)
}
~~~
{: .source}

Please, open an editor, copy the function above and save it as `R/functions.R`.
All the functions of the package have to be in `R` files inside the `R/` folder.

{% include links.md %}