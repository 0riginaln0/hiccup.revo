# hiccup.revo

hiccup.revo is an HTML rendering library. As you might guess, it is inspired by the [Hiccup](https://weavejester.github.io/hiccup/).

It renders html from a revo table.

**Table format rules:**
1. First item is always the tag name.

    `{:span}`

2. Second item is optional and represents tag attributes.

    `{:span, {class="foo"}}`
3.1 Remaining items represent the tag's child content.
3.2 If child content is not a string, it can be another nested element.

    `{:span, "Hello world", {:span, {class="foo"}, "Foooed"}}`

**CSS Shortcuts**:

Attach `!id` and `.class` directly to the tag atom.

Chain multiple classes using dots.

Defaults to a `<div>`.

```revo
{:div!hero.bg-blue "Welcome"} # Renders: <div id="hero" class="bg-blue">Welcome</div>
{:.card "Content"} # Renders: <div class="card">Content</div>
```

**Usage**
```html
html {
 :body,
 {:h1.header, "I <3 BOOKS" |> escape},
 {:p!main-paragraph, "This boxing enthusiast will go down with a single punch."},
 {:img, {src="https://cs6.pikabu.ru/post_img/2014/06/04/7/1401873068_417941350.jpg",
         alt="Boxing enthusiast meme"}}
}
```

---

# I &lt;3 BOOKS

This boxing enthusiast will go down with a single punch.

![Boxing enthusiast meme](https://cs6.pikabu.ru/post_img/2014/06/04/7/1401873068_417941350.jpg)
