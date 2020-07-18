---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---




{% include base_path %}

{% for publication in site.publications reversed %}
  {% include archive-single.html %}
{% endfor %}
