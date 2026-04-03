---
layout: archive
title: "Sitemap"
permalink: /sitemap/
author_profile: true
---

{% include base_path %}

A list of all the posts and pages found on the site. For you robots out there is an [XML version]({{ base_path }}/sitemap.xml) available for digesting as well.

<h2>Pages</h2>
<ul>
{% assign visible_pages = site.pages | sort: "url" %}
{% for post in visible_pages %}
  {% assign page_title = post.title | default: "Home" %}
  {% unless post.published == false or post.sitemap == false or post.url == nil or post.url == "" or post.url contains ".xml" or post.url contains ".txt" or post.url contains ".css" or post.url contains "redirects.json" %}
    {% if post.url == "/" or post.title %}
      {% if post.url == "/" %}
        {% assign page_title = "Home" %}
      {% endif %}
  <li><a href="{{ post.url | relative_url }}">{{ page_title }}</a></li>
    {% endif %}
  {% endunless %}
{% endfor %}
</ul>

{% if site.posts.size > 0 %}
<h2>Posts</h2>
<ul>
{% for post in site.posts %}
  <li><a href="{{ post.url | relative_url }}">{{ post.title }}</a></li>
{% endfor %}
</ul>
{% endif %}

{% for collection in site.collections %}
{% unless collection.output == false or collection.label == "posts" %}
  {% assign visible_count = 0 %}
  {% for post in collection.docs %}
    {% unless post.published == false or post.sitemap == false %}
      {% assign visible_count = visible_count | plus: 1 %}
    {% endunless %}
  {% endfor %}
  {% if visible_count > 0 %}
<h2>{{ collection.label | capitalize }}</h2>
<ul>
  {% for post in collection.docs %}
    {% unless post.published == false or post.sitemap == false %}
  <li><a href="{{ post.url | relative_url }}">{{ post.title }}</a></li>
    {% endunless %}
  {% endfor %}
</ul>
  {% endif %}
{% endunless %}
{% endfor %}
