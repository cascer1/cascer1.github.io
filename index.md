
**Hello, world!**

This site contains a (currently laughably tiny) collection of stories I've written.

---

## Posts by category

{% for category in site.categories %}
### {{category[0]}}

{% for post in category[1] %}
* [{{post.title}}]({{post.url}})
{% endfor %}

---

{% endfor %}
