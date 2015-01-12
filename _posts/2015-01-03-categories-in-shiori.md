---
title: "Categories in Shiori"
categories: [shiori, html, bootstrap, category with spaces]
---

## Overview
It's nice to categorize your posts so you can browse related posts more easily.

1. We use a plugin to generate category pages. The categories will be placed in <code>/categories/&lt;category_name&gt;</code>.
2. We define <code>category_links</code> and <code>category_link</code> filters to create links to category pages.

## Example
The list of categories for a post in the header above is generated like this:

~~~~~~~~~~~~
{{ "{% if page.categories != empty" }} %}
<p class="text-muted">Filed under {{ "{{ page.categories | category_links" }}}}</p>
{{ "{% endif" }} %}
~~~~~~~~~~~~

You can link to a single existing category page, for example,

~~~~~~~~~~~~
<a href="{{ "{{ 'html' | category_link " }}}}">HTML</a>
~~~~~~~~~~~~

will produce this link: <a href="{{ 'html' | category_link }}">HTML</a>.

We can make a list of all categories like this:

~~~~~~~~~~~~
<ul>
{{ "{% assign sorted_categories = site.categories | sort" }} %}
{{ "{% for category in sorted_categories" }} %}
<li><a href="{{ "{{ category | first | category_link" }}}}">{{ "{{ category | first | capitalize" }}}}</a></li>
{{ "{% endfor" }} %}
</ul>
~~~~~~~~~~~~

<ul>
{% assign sorted_categories = site.categories | sort %}
{% for category in sorted_categories %}
<li><a href="{{ category | first | category_link }}">{{ category | first | capitalize }}</a></li>
{% endfor %}
</ul>

## Limitation
* Because we use Jekyll plugin, this doesn't work automatically with Github Pages. You need to generate the site and push that to your <code>gh-pages</code> branch instead.
* Categories seem to be case-insensitive, so it might be hard to style them consistently.
* Categories with symbols might not work properly. Please modify the <code>slugify_category</code> method in <code>_plugins/generate_categories.rb</code> for yourself.
