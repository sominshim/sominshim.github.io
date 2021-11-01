---
title: "GitHub Pages"
layout: archive
permalink: categories/github-pages
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories['GitHub Pages'] %}
<!-- {{site.categories[page.category]}} -->
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}
