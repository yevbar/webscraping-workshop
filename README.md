| name | description | author |
| :----: | :-----------: | :------: |
| Scraping a scraping workshop | A few cool hacks with web scraping | ([@yevbar](https://github.com/yevbar)) |

# WEB SCRAPING 101

Today we're going to do a few cool hacks with python and web scraping! I'm using python because it's a nice language though there's nothing stopping you from trying this out in Javascript or Assembly (though I wouldn't really recommend the latter).

Before we get to the scraping we need to understand a few things about how the internet works.

In a nutshell, the internet is just a bunch of computers giving each other high fives. When a computer goes to "https://duckduckgo.com", what's really going on is that the computer is putting its hand up to the internet and asking for a "https://duckduckgo.com". When it gets a high five back, it's getting a high five from a server that gives it some HTML code. To see what that looks like, you can go to "https://duckduckgo.com" and then inspect element. You should see something like this

![](images/inspect_element.png)

This is what web pages really look like! To get this as plain text, you can also go to a terminal and run `curl` like so

![](images/curl.png)

Though we won't need to know much networking to accomplish the tasks we're aiming for (though some knowledge on browser sessions and POST requests will come in handy for more elaborate web scraping scripts)

Starting simple, we're going to put together a script that obtains the first paragraph of a Wikipedia article as a TL;DR for some topic. To start out, we're going to install two libraries

[![imports](images/imports.png)](https://repl.it/@yevbar/Web-Scraping-Imports)

The `requests` library is what we'll use to handle the making requests and the `html` library is how we'll treat the html as a data structure rather than plain text.

Before we go about making requests, we should check to see what we're scraping for specifically. To do that, let's go to some Wikipedia article, here I'm going to the page on memes.

![](images/wikipedia.png)

What we want to obtain is this first paragraph, which sort of acts as a TL;DR for the entire topic. Opening up inspect element and hovering over a particular p tag highlights the section around that first paragraph which means we've found the specfic element we're looking for!

![](images/p_tag.png)

By pressing the arrows to the left of the tags, we can see this tree like structure of the whole paragraph

![](images/tree_like.png)

We don't need to stress over the specific tags and such in the paragraph, those are mostly for the citations. To get the text, we simply get the `text` value of the element. But to get the element in the first place, we're going to use `xpath` to navigate the XML (which in this case is the HTML) of the file, and is why we imported the `html` library earlier.

Now to get working!

[insert screenshot of repl here]

```python
import requests
from lxml import html

my_session = requests.session()
```

The first thing we're going to do is initialize a `session` object. While you could simply call the function from that class, it helps with readability and a session is needed for more elaborate web scraping.

[insert screenshot of repl here]

```python
import requests
from lxml import html

my_session = requests.session()
page = my_session.get("https://en.wikipedia.org/wiki/Meme")
```

Now we've
