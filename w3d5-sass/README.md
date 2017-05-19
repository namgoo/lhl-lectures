# SASS and responsive design

CSS is great(-ish), but it lacks some features we're used to find in _real_ programming variables, such as variables, modules and so on. There are a few tools created to fill in that gap, and one of the most popular ones is the [SASS css preprocessor](http://sass-lang.com).

## Getting sassy

SASS has two syntaxes: an oldschool one that uses significant whitespaces (like Python) and SCSS, which looks pretty much like CSS with additional features, the most notable being nesting, variables and partials.

This means instead of writing CSS like this:
```css
nav {
  border: 1px solid black;
}

nav ul {
  list-style: none;
  padding: 0;
  text-align: center;
}

nav a {
  text-decoration: none;
  font-weight: bold;
  color: #2184a5;
}
```

You can write this:
```scss
$link-color: #2184a5;

nav {
  border: 1px solid black;
  ul {
    list-style: none;
    padding: 0;
    text-align: center;
  }
  a {
    text-decoration: none;
    font-weight: bold;
    color: $link-color;
  }
}
```

The full SASS guide can be found [here](http://sass-lang.com/guide).

### Installation and usage

SASS was originally written in Ruby, and the official way to install it is by using the `gem` command. Luckily for us, it was also made into a library that can be used from Node with [the `node-sass` package](https://github.com/sass/node-sass). This gives you a command-line tool to compile SCSS into plain old CSS. You can then add it to your `package.json` like so:

```json
"scripts": {
  "compile-sass": "./node_modules/node-sass/bin/node-sass --watch --recursive --output public/css stylesheets",
 }
```

This will compile all SASS files in the `/stylesheets` folder and put them into the `/public/css` folder

It's also possible to integrate SASS directly with Express using the [`node-sass-middleware` package](https://github.com/sass/node-sass-middleware). If you do this, remember two things:

* This will **overwrite all CSS files inside `/public/css`** every time the server starts. You should edit the `.scss` files inside `/stylesheets` instead.
* On the other hand, the browser has no idea how to parse SCSS, so you should link the **generated `.css` files generated in `/public/css` on your HTML**.

See the [`/code`](code) folder for more details.

## Responsive design

Whether we call it Responsive Design, Adaptive Design, Progressive Design, or Mobile-first Design, they all have one thing in common: they are concerned for how a website will appear across different types of screens/devices.

The techniques used to deal with this are old, coming from an era where people wanted to print webpages and a different style-sheet would be needed to support the printer. That `@media` query would allow for a completely different set of styles to be applied IF the page was rendered on paper instead. These days, `@media` queries can be used to read the size of the display area and override CSS rules accordingly. [MDN has a great guide on media queries (as usual).](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries).

The links below contain good tutorials on responsive design concepts, but if you have to remember one thing is this: always start designing your web applications assuming the user needs to do ONE thing and that thing is the only widget that matters in your page. Everything else should be secondary.

* Responsive design basics: https://developers.google.com/web/fundamentals/design-and-ui/responsive/
* Common patterns for flexible layouts: https://developers.google.com/web/fundamentals/design-and-ui/responsive/patterns
* If your layout is super complex, consider a full FlexBox: https://css-tricks.com/snippets/css/a-guide-to-flexbox/