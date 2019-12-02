
**Hello, world!**

This site contains stuff.

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

<a href="https://www.troyhunt.com/why-i-am-worlds-greatest-lover-and/" target="_blank">
    <img src="https://i.eliens.co/site/mcafee.jpg" height="75px" />
    <img src="https://i.eliens.co/site/norton_secure_seal.png" height="75px" />
    <img src="https://i.eliens.co/site/trustwave.jpg" height="75px" />
</a>
