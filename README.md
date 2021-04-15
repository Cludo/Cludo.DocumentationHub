## Getting started

### Development environment

#### Option 1: Hugo CLI

`hugo server -D -w`

#### Option 2: Docker

1. Open repository in WSL mode using Visual Studio Code
2. `docker-compose up`

#### Issue with file watching / change detection / live reload

[vs code solution](https://github.com/microsoft/WSL/issues/4739)

You can work around this with vs code by opening in wsl

https://docs.microsoft.com/en-us/windows/wsl/compare-versions#performance-across-os-file-systems

### Hugo how-to
 - [Book theme partials to override](https://themes.gohugo.io/hugo-book/#partials)
 - [Book theme sass files to override](https://themes.gohugo.io/hugo-book/#extra-customisation)
#### Override theme html partials

Through partial overrides, you can add html to various sections of the generated content by creating the files outlined by the link above and putting them in the appropriate folder. The Hugo engine takes care of everything else once you add the override file.

#### Override theme css

To override the theme styles, you can create the files specified at the link above (placed in the `assets` folder of the project)

#### Custom html components (via shortcodes)

Hugo allows developers to create their own shortcodes which can generate some shared html. This can be useful if you want to make modular components to be rendered throughout the site. For example, we will use this approach for creating embedded swagger modules.

Custom shortcodes can be placed in the `layouts/shortcodes` folder of the project. The name of the shortcode is the name of the html file (without `.html`).

Here's a quick example:

Create the following file: `layouts/shortcodes/myshortcode.html` 

With the following content:

```
<p>Hello, world from my custom shortcode!</p>
```

Now, reference the shortcode in one of the `content` markdown files with the following snippet:

`{{< myshortcode >}}`

You should see your custom shortcode html snippet rendered on the site. Shortcodes can take variables and contain their own template logic when needed. You can find documentation for Hugo templates [here](https://gohugo.io/templates/shortcode-templates/).