---
layout: default
---

<h2>{{ site.data.samplelist.docs_list_title }}</h2>
<ul>
   {% for item in site.data.samplelist.docs %}
      <li><a href="{{ item.url }}">{{ item.title }}</a></li>
   {% endfor %}
</ul>

# PHOTOGRAPHY

<iframe src="https://pixelfed.social/sct/embed" class="pixelfed__embed" style="max-width: 100%; border: 0" width="400" allowfullscreen="allowfullscreen"></iframe><script async defer src="https://pixelfed.social/embed.js"></script>
