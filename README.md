# BitDevs Zaria

Simple Jekyll site for hosting all of the links from meetups past and future.

## Development

You'll need [Ruby & Jekyll](https://jekyllrb.com/docs/installation/) to run the
site locally. Once they're setup:

* Clone the repository and go into the directory
* Run `bundle install`
* Run `jekyll serve`
* Go to http://localhost:4000

## Making a Post

To make a new post, make a new file in `_posts/` with a title of
`YYYY-MM-DD-title-goes-here`. At the top of the file you'll want to provide the
following information:

```md
---
layout: post # Always post
type: socratic # or whitepaper for a whitepaper series
title: "Name of the Post"
---
```

After that, it's just simple markdown. The site will auto-generate the rest.

## Changing Site Data

All site configurations are either contained in `_config.yml` or
`_data/settings.yml`. Some data is duplicated between the two due to the way
Jekyll injects variables, so be sure to update both.

Social/community links live in the `menu` list in `_data/settings.yml` — fill
in the `TODO_bitdevszaria` placeholders with your real Discord and Luma/Meetup
URLs.

## Attributions

This site was adapted from [BitDevs Nairobi](https://github.com/BitDevsNBO/bitdevsnbo.org),
which itself thanks [LeNPaul](https://github.com/LeNPaul/jekyll-starter-kit) for
the Jekyll starter kit it was forked from.
