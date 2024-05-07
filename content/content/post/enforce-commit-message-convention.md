+++
date = "2016-07-12T04:05:25-06:00"
draft = false
title = "Enforce Better Commit Messages"

+++

> "minor fix" - Lucifer

One of the common feedbacks I used to get during my early days of software development was how to communicate my changes with my colleagues with good commit messages. There's no rule out there on how to write a commit message, but there are quite a few conventions out there. Some prefer writing the changes in the past tense, some in the present tense. Some mention the ticket number in their commit message, some avoid doing that and instead stick to the scope of the changes. Some projects(that have a solo contributor), don't use an issue tracker until late in the project and have "minor changes" or "new feature" written all over the repo.

Also, I believe having a guideline takes this mental blockage off the dev from thinking about how to write a message. If you have ever found yourself backspacing a lot while writing a commit message you know what I'm talking about.

There are two steps to get rid of bikeshedding around commit messages.

1. Pick a convention
2. Enforce it

One simple way to get started on a convention is to look at the source code of various open-source projects and observe the rules they follow. I loved how [Aurelia](https://github.com/aurelia/framework) managed its commits and grouped commits in several categories and used it in some of my projects. Take a look at their [commit message guidelines.](https://github.com/DurandalProject/about/blob/master/CONTRIBUTING.md#commit)

> "feat(init): let there be light" - God

> "refactor(YEAR-2049): cleanup some genes causing cancer" - Human

To enforce a convention, [git hook](https://git-scm.com/docs/githooks) is your friend. Git has this hooking mechanism that lets you hook into the lifecycle of various events, like pulling, pushing, committing etc. In this case, we can hook into gits' `commit-msg` hook to enforce the writer of the commit to follow the convention we agreed upon. The `commit-msg` hook is a simple shell script that executes before the user's changes are committed. It receives the commit message that the user entered and may accept or reject the changes submitted by the user based on the content of the message. I use a very simple script that alerts the user every time she commits without following the conventions of Aurelia's commit message guidelines.

Copy [the script](https://gist.github.com/afm-sayem/2cb8343d92f1415e64b90e1ba7cea35e#file-commit-msg) to your projects `.git/hooks` directory(the file name has to be `commit-msg`) and try committing something with "Made a few changes" as the message and watch it get rejected. If it's still letting the commit through then make sure that the `commit-msg` script has execute permission.

If you want all your future projects to have this hook automatically in their repos, several solutions are listed in [this stackoverflow question](http://stackoverflow.com/questions/2293498/git-commit-hooks-global-settings).
