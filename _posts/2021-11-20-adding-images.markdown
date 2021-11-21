---
layout: post
title:  "Adding Images to the Blog"
date:   2021-11-20 23:55 -0500
categories: update 
---

Credit to [Eduardo Bouças](https://eduardoboucas.com/blog/2014/12/07/including-and-managing-images-in-jekyll.html) for the idea.

To reduce the amount of images in `/assets/posts`, I want to create a new directory for every post (if it has images) like so:
```
.
├── assets
|   ├── images (my layout images)
|   └── posts (my post images)
|       └── 2021-11-20-adding-images-to-the-blog
|           ├── test-image.png
|       └── 2021-11-22-example-post-1
|           └── cool-image.png
```

To reduce the code needed to set up the images like this, we can add a new file at `_includes/image.html`.

{% raw %}
```
{% capture imagePath %}{{ page.date | date: "%Y-%m-%d" }}-{{ page.title | slugify }}/{{ include.name }}{% endcapture %}
<img src="/assets/posts/{{ imagePath }}" {% if include.alt %} alt="{{ include.alt }}" {% endif %} {% if include.width %} width="{{ include.width }}" {% endif %}/>
```
{% endraw %}

Now images can be imported like so:

{% raw %}
```
{% include image.html name="image-name.png" alt="Alt text for my image" %}
```
{% endraw %}

{% include image.html name="test-image.png" alt="A picture of a frog" %}

