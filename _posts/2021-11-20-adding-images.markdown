---
layout: post
title:  "Adding Images to the Blog"
date:   2021-11-20 23:55 -0500
categories: update 
---

To reduce the amount of images in `/assets/posts`, I want to create a new directory for every post
(if it has images) like so:
```
.
├── assets
|   ├── images (my layout images)
|   └── posts (my post images)
|       └── 2014-10-09-the-story-behind-my-website
|           ├── editing.jpg
|           └── studio.jpg
|       └── 2014-11-20-thoughts-on-serving-and-monitoring-a-feed
|           ├── feedburner-custom-domain.png
|           ├── feedburner-dashboard.png
|           └── feedly-search.png
|       └── 2014-11-04-is-linkedin-ignoring-your-open-graph-meta-tags
|           ├── butler.png
|           ├── linkedin-after.png
|           └── linkedin-before.png
```

To reduce the code needed to set up the images like this, we can add a new file to `_includes`.

{% raw %}
```
{% capture imagePath %}{{ page.date | date: "%Y-%m-%d" }}-{{ page.title | slugify }}/{{ include.name }}{% endcapture %}
{% if include.caption %}
    <figure>
        <img src="/assets/posts/{{ imagePath }}" {% if include.alt %} alt="{{ include.alt }}" {% endif %} {% if include.width %} width="{{ include.width }}" {% endif %}/>
        <figcaption>{{ include.caption }}</figcaption>
    </figure>
{% else %}
    <img src="/assets/posts/{{ imagePath }}" {% if include.alt %} alt="{{ include.alt }}" {% endif %} {% if include.width %} width="{{ include.width }}" {% endif %}/>
{% endif %}
```
{% endraw %}

Credit to [this guy's blog](https://eduardoboucas.com/blog/2014/12/07/including-and-managing-images-in-jekyll.html).
