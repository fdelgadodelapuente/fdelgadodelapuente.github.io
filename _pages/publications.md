---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---
{% if author.googlescholar %}
  <u><a href="{{https://scholar.google.com/citations?user=ZVSmRYwAAAAJ&hl}}">Google Scholar</a></u>
{% endif %}

{% include base_path %}

{% for post in site.publications reversed %}
  {% include archive-single.html %}
{% endfor %}
