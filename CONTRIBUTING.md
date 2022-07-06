# How to contribute

I'm really glad you're reading this, because I need volunteer developers to help this project come to fruition.

## Submitting changes

Please send your Pull Requests with a clear list of what you've done (read more about [pull requests](http://help.github.com/pull-requests/)).

Please follow my coding conventions (below) and make sure all of your commits are atomic (one feature per commit).

Always write a clear log message for your commits.

One-line messages are fine for small changes, but bigger changes should look like include a paragraph describing what changed and its impact.

## Coding conventions

Start reading my code and you'll get the hang of it. I optimize for readability:

- I indent using tabs (equal to four spaces)
- I use MVC (Model - View - Controller) : KISS name of class model, XAML for view and XAML.cs as controller.
- I ALWAYS put spaces after list items and method parameters (`[1, 2, 3]`, not `[1,2,3]`) and around operators (`x += 1`, not `x+=1`).
- For brace placement in compound statements, I use **Allman** style, and **K&R** style for try/catch blocks. (see on [wikipedia](https://en.wikipedia.org/wiki/Indentation_style#Brace_placement_in_compound_statements))
- and for all the rest, I use the Visual Studio C# recommandations.

## Optimization

- Absolute ban on using **Linq** !
- Absolute prohibition to use **WMI** !
- to be continued...

