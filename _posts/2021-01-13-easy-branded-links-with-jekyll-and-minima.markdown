---
layout: post
title:  "Easy Branded Links with Jekyll & Minima"
author: Ruby Sullivan
date:   2021-01-13 21:00:00 -0500
categories: code
---

## The Problem

Having short, branded links is super useful for expanding your community
across multiple platforms. A great example of this is Twitter user
[@involutegirl][excogs]'s [gears.link][gl], [gears.link/tea][glt], and
[gears.link/discord][gld]. I wanted to have some for my Twitch channel and
Discord server, but also wanted to have the links displayed in the header
of my Jekyll page as a means of easy access for visitors on my blog. I also
wanted to come up with a solution that could easily be used by other Jekyll
users, particularly those with little to no coding experience.

## The Solution

Since my Jekyll theme, *Corundum*, is a Minima derivative, adding links to the
header is as easy as adding a `<name>.markdown` file in the root directory and
using the page layout. Therefore, all that's needed to create easy redirects
is *extending* the page layout and adding a little bit of Javascript to
perform the redirect.

### Redirect Layout

In your `_layouts` directory, add a file called `redirect.html` and add the
following code:

```
{% raw %}
# redirect.html
---
layout: page
---
{{ content }}
<script>
  window.onload = function() {
    window.location.replace("{{ page.redirect }}");
  }
</script>
{% endraw %}
```

This will create a new layout that extends the existing page layout, but adds
a bit of Javascript that will redirect to a URL specified in the front matter
of the markdown file.

### Markdown File

Next, create a `.markdown` file in the root directory for the link you want to
redirect to. I'll use Twitch for my example:

```
{% raw %}
# twitch.markdown
---
layout: redirect
title: Twitch
permalink: /twitch/
redirect: https://twitch.tv/CorundumCore
---

### Redirecting to Twitch...
{% endraw %}
```

The important parts of this code are all in the front matter.
`layout: redirect` tells Jekyll to use the `redirect.html` extension layout we
just created, which adds the necessary Javascript to perform the redirect.
`title: Twitch` tells Jekyll what we want the redirect to be listed as in our
header. `permalink: /twitch/` tells Jekyll to use the specific link we want,
rather than generating one itself. Finally, the
`redirect: https://twitch.tv/CorundumCore` is what the `redirect.html` layout
uses in the Javascript code to know which page to redirect to.

Finally, I like to add a little message (`### Redirecting to Twitch...`) to let
users with slower devices know what's up if it takes a while to perform the
redirect, so they're not just looking at a blank screen.


[excogs]: https://twitter.com/involutegirl
[gl]:     https://gears.link
[glt]:    https://gears.link/tea
[gld]:    https://gears.link/discord