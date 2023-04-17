---
layout: post
title:  "Make your site indexable on Google"
date:   2023-04-17
categories: skills
author: Chenguang Xiao
---

It confused a lots of people to make their site visible on Google search engine.
I summarize the steps to achieve it according to my experience recently.
The key points are:
+ google analytics
+ sitemap
+ google search console

## google analytics

Click the [google analytics](https://analytics.google.com/analytics) and create a analytics for your site, and you will get a code like this:

```html
<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=measurement_id"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'measurement_id');
</script>
```

This is only for a reference, always use the latest code from google analytics.

## sitemap

Sitemap is a xml file that illustrates the structure of your site.
In my case where I use jekyll to generate my site on github.io, just add 'jekyll-sitemap' plugin to jekyll in '_config.yml' file like this:

```yaml
plugins:
- jekyll-remote-theme
- jekyll-sitemap
```

Then you can find a 'sitemap.xml' file in your site root directory, and the sitemap page is on 'https://your_site/sitemap.xml'.

## google search console

finally, you need to add your site to [google search console](https://search.google.com/search-console), and verify your site ownership.

The *google analytics* code will help you to verify your site ownership.

The *sitemap* may help you in speed up the indexing process.

Hopefuly, your site will be indexed on google search engine in a few days.