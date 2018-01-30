---
layout: default
title: about
---
{% capture my_include %}{% include_relative about.md %}{% endcapture %}
{{ my_include | markdownify }}
