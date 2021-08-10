---
title: "Accessing packages"
teaching: 20
exercises: 5
questions:
- "How do I use my package?"
- "How do I use someone else's package?"
- "What is the difference between installing and attaching?"
objectives:
- "Install and attach your own packages"
- "Install packages from GitHub"
- "Install packages from CRAN"
keypoints:
- "To use a package you have to install and attach it"
- "There are several ways of installing a package"
---

One of the advantages of packages is that they can be **installed**.
This allows us to use the functions contained in the package from anywhere.

There are many ways of accessing a package in order to start using it.
In this section, we will study the most common ones.
At the end, we'll describe briefly other alternatives that may be useful in some cases.
## Install a package from CRAN

[CRAN](https://cran.r-project.org/) is the official repository for R Packages.
It stands for the _Comprehensive Archive R Network_.
It is an awesome collection of high quality resources written by other R users just like you.

Installing a package from CRAN is particularly easy.
Let's imagine we need to install a package with tools for R developers.
We can start by browsing to our favorite search engine, and make a search like: _R developers tools_.
It will point us to a package called `devtools`.
The package can be installed by opening RStudio and browsing to the _Packages_ tab:

![Packages tab](../fig/packages.png)

After pressing _Install_, a window like this will appear:

![Install prompt](../fig/install.png)

We write `devtools` in the prompt, and press install.
This operation will download and install the package and the required dependencies.
Depending on the package, it may take a while, ranging from a few seconds to a few minutes.

> ## The same, but with a command
> Some people may prefer using code instead of a graphical user interface to install a package.
> Are you one of them?
> Then, you'll like to know that all the above is equivalent to typing:
> 
> ```r
> install.packages("devtools")
> ```
>
> As often happens with RStudio, you don't have to remember this command by heart.
> You can keep using the graphical user interface and **observe** what happens in the console.
> RStudio will build and execute the command for you.
{: .callout}

After installing, the new package should appear in the _Packages_ tab.
> ## Something went wrong?
> Sometimes, an installation may fail.
> If that's the case, take a look at the output message in the console.
> It will contain very useful information, and direct suggestions about how to fix the problem.
{: .callout}

> ## Can I publish my package in CRAN?
> The answer is yes, and it is easier than you may think.
> We'll go back to this in chapter FIXME.
{: .callout}

In the sections below we'll see how to install a package from other sources than CRAN.
But first, let's see how can we actually use our freshly installed package!
## Using an installed package

In order to use an installed package, you need to load it into workspace.
Typically, you'll do it via attaching the package.
This means that its functions and data will become available in your working session, so you can use them in your console and your scripts.
Additionally, the functions in your package will be added to the search path.

The easiest way to attach an installed package is by using the _Packages_ tab.
If you click on the package's name, the package's help menu will open.
If you click on the checkbox by the package's name (see figure below), the package will be attached.

![](../fig/loaded.png)

The figure above shows that the package `testthat` is installed and attached.
Other packages, such as `stringi`, `stringr` or `svglite`, are installed but not attached.
> ## What if we want to attach a package from the console?
> How would you attach an installed R package using the console?
>
> Tip: As always with RStudio, it is a good idea to look at the console while we are performing operations in the graphical user interface.
> > ## Solution
> > Use `library(<package name>)`.
> {: .solution}
{: .challenge}

> ## Using a function without attaching the package
> In some situations it can be a good idea to load individual functions from a given package, but not the package itself.
> This can be done using the syntax: `<package>::<function>`.
>
> For instance, if we want to use the function `filter` from the package `dplyr` we can call it directly as:
>
> ```r
> dplyr::filter()
> ```
> Keep in mind that for this to work, `dplyr` has to be installed.
{: .callout}

> ## To attach nor not to attach?
> If you are developing a package that depends on other packages, it is strongly recommended to call functions on the other packages using the syntax `<package>::<function>`. Conversely, it is strongly advised to not use `library(<package>)` inside a package.
> 
> Do you have any idea why?
> > ## Solution
> > The dependencies of a package can become tricky.
> > A common problem is that two packages contain two functions with the same name.
> > The more explicit the naming, the better.
> >
> > Additionally, we have to keep our potential users in mind.
> > We want our package to do its work and leave no trace behind.
> > Using `library(<package>)` inside the package will permanently alter the search path.
> {: .solution}
{: .discussion}

## Install a package from GitHub

Although CRAN is the official repository for R packages, it is not the only one you can use.
As we've seen / we'll see in chapter FIXME, GitHub, is the most popular open code repository.
We can use GitHub to find packages or to make our own packages publicly available.
Contrary to CRAN, packages in GitHub are not reviewed.
This has an advantage: you can have your package published there in no time.

Let's imagine we want to install a package from GitHub, such as https://github.com/PabRod/kinematics.
The package we installed before, `devtools`, allows us to install easily using:

```r
devtools::install_github("PabRod/kinematics")
```

In section FIXME you'll learn how to publish your package on GitHub.

> ## Why would you want to install a package from GitHub?
> Can you think of a situation where you'll rather install from GitHub than from CRAN?
> > ## Solution
> > There are two common situations where you'll want to use GitHub instead of CRAN:
> >
> > The first and most obvious one is when **the package you want doesn't exist on CRAN**.
> > This can happen for many reasons.
> > Maybe the package is still work in progress, or doesn't pass the CRAN quality checklist.
> > Or perhaps the authors just don't want to publish it on CRAN.
> >
> > The second situation is when **you need a cutting edge version of the package**.
> > R developers usually use GitHub for their everyday work, and only apply to CRAN when they have accumulated changes enough.
> > If you need a very particular version of the package, usually GitHub is the place to go.
> {: .solution}
{: .challenge}

## Install a package from source

What if the package is only available in your computer?
This is the case of the one we are building during this lesson.

The easiest way to install a package from source is by opening the package project and using the _Build_ tab:

![Build](../fig/build.png)

By pressing _Install and restart_ three things will happen:

1. The package will be, indeed, installed.
2. The R session will be restarted.
3. The package will be loaded (FIXME: check if loaded or attached).

> ## Why would you want to load a package from source
> Can you think of a situation where you'll need to install and attach a package from source?
> > ## Solution
> > The most common situation is while you are developing a package.
> > Every now and then, you'll want to re-install and re-load it to check that everything is working as expected.
> >
> > Loading from source can be also useful if you want to use a colleague's package.
> > But we warned here.
> > In the next session we'll learn a much better way of sharing packages among your colleagues using GitHub.
> {: .solution}
{: .challenge}

{% include links.md %}