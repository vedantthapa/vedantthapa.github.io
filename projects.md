---
layout: page
title: Projects
---

<section>
    {%for post in site.posts %}
      {% unless post.next %}
        <ul>
      {% else %}
        {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
        {% capture nyear %}{{ post.next.date | date: '%Y' }}{% endcapture %}
      {% endunless %}
        <li>
          <h2>
            <a href="{{ post.url | prepend: site.baseurl | replace: '//', '/' }}">
              {{ post.title }}
            </a>
          </h2>
          <time>{{ post.date | date:"%d %b %Y" }}</time>
          <p>{{ post.content | strip_html | truncatewords:45 }}</p>
          <br>
        </li>
    {% endfor %}
    </ul>
</section>