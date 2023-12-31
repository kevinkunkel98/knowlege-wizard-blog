---
author: Kevin Kunkel
pubDatetime: 2022-12-28T04:59:04.866Z
title: My first KDE + Arch rice
postSlug: kde-arch-rice
featured: false
draft: false
tags:
  - rice
  - theme
  - kde
ogImage: ""
description: Turning the standard KDE into a stunning Desktop
---

KDE Plasma is a highly costumizable and functional Desktop Environment that can be used to 

## Table of contents

## Installation

First of all we want to install and enable a virtual environment (venv):

```shell
pip3 install virtualenv
```

Then we need to create it in our project directory

```shell
virtualenv venv --system-site-packages
```

Then we activate it


```shell
source venv/bin/activate
```

Now install Flask

```shell
pip3 install Flask
```

> The Social Image used for Twitter is technically not called OG image. However, in this post, I'll be using the term OG image for all types of Social Images.

## Creating your first server

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return 'hello, world'
```


AstroPaper already provided a way to add an OG image to a blog post. The author can specify the OG image in the frontmatter `ogImage`. Even when the author doesn't define the OG image in the frontmatter, the default OG image will be used as a fallback (in this case `public/astropaper-og.jpg`). But the problem is that the default OG image is static, which means every blog post that does not include an OG image in the frontmatter will always use the same default OG image despite each post title/content being different from others.

## Dynamic OG Image

Generating a dynamic OG image for each post allows the author to avoid specifying an OG image for every single blog post. Besides, this will prevent the fallback OG image from being identical to all blog posts.

In AstroPaper v1.4.0, Vercel's [Satori](https://github.com/vercel/satori) package is used for dynamic OG image generation.

Dynamic OG images will be generated at build time for blog posts that

- don't include OG image in the frontmatter
- are not marked as draft.

## Anatomy of AstroPaper dynamic OG image

Dynamic OG image of AstroPaper includes _the blog post title_, _author name_ and _site title_. Author name and site title will be retrieved via `SITE.author` and `SITE.title` of **"src/config.ts"** file. The title is generated from the blog post frontmatter `title`.  
![Example Dynamic OG Image link](https://user-images.githubusercontent.com/53733092/209704501-e9c2236a-3f4d-4c67-bab3-025aebd63382.png)

## Limitations

At the time of writing this, [Satori](https://github.com/vercel/satori) is fairly new and has not reached major release yet. So, there are still some limitations to this dynamic OG image feature.

- If you have Blog posts with non-English titles, you have to set `embedFonts` option to `false` (file: `src/utils/generateOgImage.tsx`). Even after this, the OG image might not be displayed very well.
- Besides, RTL languages are not supported yet.
- [Using emoji](https://github.com/vercel/satori#emojis) in the title might be a little bit tricky.
- Sadly, this new dynamic OG image generation feature cannot be used for Twitter social images since `svg` image type is not supported for Twitter Cards.
