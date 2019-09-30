
**Hello, world!**

This site contains a collection of stories I've written.

## Interesting stuff

---

* [Universal Greeting Time (UGT)](/ugt.html)

## Posts by category

---

{% for category in site.categories %}
### {{category[0]}}

{% for post in category[1] %}
* [{{post.title}}]({{post.url}})
{% endfor %}

---

{% endfor %}

## Very Important Seals

![mcafee](https://i.eliens.co/site/mcafee.jpg =175x)
![norton](https://i.eliens.co/site/norton_secure_seal.png =175x)
![trustwave](https://i.eliens.co/site/trustwave.jpg =175x)
