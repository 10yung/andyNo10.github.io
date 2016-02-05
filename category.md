---
layout: page
title: Categories
permalink: /categories/
---
<div>
{% assign categories = site.categories | sort %}
{% for category in categories %}
 <span class="site-tag">
    <a href="#{{ category | first | slugify }}">
            {{ category[0] | replace:'-', ' ' }}
    </a>

</span>
||   
{% endfor %}
<hr>
</div>


<div id="index">

{% for category in categories.{{ category | first | slugify }} %}
<a name="{{ category[0] }}"></a><h2 style="display:inline;">{{ category[0] | replace:'-', ' ' }}</h2>
<span style="font-size:15px !important; bottom: 5px;" class="fa-stack">
  <i class="fa fa-circle fa-stack-2x"></i>
  <p class="fa-stack-1x fa-inverse">{{ category | last | size }}</p>
</span>



{% assign sorted_posts = site.posts | sort: 'title' %}

{% for post in sorted_posts %}
{%if post.categories contains category[0]%}
  <p class="post-meta">{{ post.date |  date: "%B %e, %Y" }}</p>
  <h3><a href="{{ site.url }}{{site.baseurl}}{{ post.url }}" title="{{ post.title }}">{{ post.title }} </a></h3>

{%endif%}
{% endfor %}

{% endfor %}
</div>
