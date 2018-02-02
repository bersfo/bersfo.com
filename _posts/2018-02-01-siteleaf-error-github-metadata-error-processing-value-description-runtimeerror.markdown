---
title: 'SiteLeaf error - GitHub Metadata: Error processing value ''description'':
  (RuntimeError)'
date: 2018-02-01 19:27:00 -08:00
categories:
- fixes
tags:
- siteleaf
- error
- github metadata
- processing value 'description'
---

When I started to setup my siteleaf tenant I quickly ran into the following error message while generating a preview of my new blog:
![siteleaf-error.png](/uploads/siteleaf-error.png)

I found no solution in the online help system but one of the posts in the #support channel in SiteLeaf's Slack tenant had the answer:

**To fix this problem make sure that you have the url and description variables added to your _config.yml**