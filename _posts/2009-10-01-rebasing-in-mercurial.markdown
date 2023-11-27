---
layout: post
title: Rebasing in Mercurial
author: hendrasaputra
date: 2009-10-01 10:31:32.000000000 +07:00
categories: [commentaries, code]
---
```
Q: How do you make your code history more useful?
A: The answer lies in rebasing. Rebasing is a technique made popular by git where you rewrite your not-yet-pushed patches so that they apply against the current remote <code>tip</code>, rather than against the <code>tip</code> of the repository you happened to last pull. The benefit is that your merge history shows useful merges—merges between major branches—rather than simply every single merge you did with the upstream repository.
```
via <a href="http://blog.bitquabit.com/2008/11/25/rebasing-mercurial/">blog.bitquabit.com</a>

Making your merge history more useful by rebasing. A concept adopted from Git by Mercurial. Still using Subversion? Move on boy. Still using CVS? Gosh what century are you living on.
  
