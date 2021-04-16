---
layout: default
---

Have a look at the Github page for more information.

You find this descriptive text in the `index.md` file, so you can _change_ it, or ~~remove~~ it completely, according to your **needs**.

[Link to another page](./another-page.html).

## Latest Posts

<div>

  {{ content }}

  <h2>Latest Posts</h2>

  <div>&nbsp;</div>

  <ul class="post-list">
    {% for post in site.posts %}
      <li>

        {% assign date_format = site.cayman-blog.date_format | default: "%b %-d, %Y" %}
        <span class="post-meta">{{ post.date | date: date_format }}</span>

        <h2>
          <a class="post-link" href="{{ post.url | absolute_url }}" title="{{ post.title }}">{{ post.title | escape }}</a>
        </h2>

        {{ post.excerpt | markdownify | truncatewords: 30 }}

      </li>
    {% endfor %}
  </ul>

</div>

### Code

```js
// Javascript code with syntax highlighting.
var fun = function lang(l) {
  dateformat.i18n = require('./lang/' + l)
  return true;
}
```

### There's a horizontal rule below this.

* * *

### Small image

![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png)

```
The final element.
```
