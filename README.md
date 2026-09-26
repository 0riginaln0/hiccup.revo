# hiccup.revo

hiccup.revo is an HTML rendering library. As you might guess, it is inspired by the [Hiccup](https://weavejester.github.io/hiccup/).

It renders html from a revo table.

**Table format rules:**
1. First item is always the tag name.

    `{:span}`

1. Second item is optional and represents tag attributes.

    `{:span, {class="foo"}}`

1. Remaining items represent the tag's child content.

1. If child content is not a string, it can be another nested element.

    `{:span, "Hello world", {:span, {class="foo"}, "Foooed"}}`

**CSS Shortcuts**:

Attach `!id` and `.class` directly to the tag atom.

Chain multiple classes using dots.

Defaults to a `<div>`.

```revo
{:div!hero.bg-blue "Welcome"} # Renders: <div id="hero" class="bg-blue">Welcome</div>
{:.card "Content"} # Renders: <div class="card">Content</div>
```

**Additional features**

A tag child can be an iterator:
```
let items = {"Apple", "Banana", "Cherry"}
let res = html {:ul, iter.map(items, fn(item) {:li, item})}
# '<ul><li>Apple</li><li>Banana</li><li>Cherry</li></ul>'
```

A tag child can be added conditionally. When a child is :nil or other falsy value, it's being ignored.
```
let logged_in? = :true
html {
  :div,
  if logged_in?
    {:button, "Go to Dashboard"}
}
#'<div><button>Go to Dashboard</button></div>'

logged_in? = :false
html {
  :div,
  if logged_in?
    {:button, "Go to Dashboard"}
}
# '<div></div>'
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
