---
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      layout: single
      author_profile: true
      read_time: true
      comments: true
      share: true
      related: true
      header:
        teaser: /assets/images/1st-post.jpg
---


# My First Posts
## This is a test


This will be the initial post for testing and validation of theme, git updating, etc.
{% raw %}{{ site.url }}{{ site.baseurl }}/assets/images/Mountains.jpg{% endraw %}
