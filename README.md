## Houston Startup Resources Front-End

Live version hosted at [startuphouston.com](http://www.startuphouston.com). 

Built as a static site with [Middleman](https://middlemanapp.com/), and using [Pure CSS](http://purecss.io/) with [Breakpoint](http://breakpoint-sass.com/) to assist in styling.

## Contribution

To successfully contribute to this project you will want to:

1. Know the basics of what [SCSS adds to CSS3](http://sass-lang.com/).
2. Familiarize yourself with the CSS libraries [Pure CSS](http://purecss.io/) and [Breakpoint](http://breakpoint-sass.com/).
3. Read the basics of the [Middleman Static Site Generator](https://middlemanapp.com/).
4. **Read the Project Structure section** of this README, so that you know what goes where when you make changes.

Changes are accepted via pull request. Please include screenshots that demonstrate the changes you have made.

## Installation

This project is built for **Ruby 2.3**. It should work with Ruby 2.0 or above, but this is not guaranteed. There is a `.ruby-version` and `.ruby-gemset` file, so if you use [rvm](https://rvm.io/) it should automatically pick up on this and ask you to install the correct version.

After cloning this repository and making sure you are using the correct Ruby version (and optionally gemset), install the dependencies with
```shell
$ bundle install
```

Or, if you don't have bundler by default:
```shell
$ gem install bundler --no-ri --no-rdoc
$ bundle install
```

Then start up Middleman!
```shell
$ middleman server
```

You should see something along the lines of:
```shell
== The Middleman is loading
== LiveReload accepting connections from ws://XXX.XXX.XXX.XXX:YYYYY
== View your site at "http://localhost:4567", "http://127.0.0.1:4567"
== Inspect your site configuration at "http://localhost:4567/__middleman"
```

Go check it out at [http://localhost:4567](http://localhost:4567) and you should see a site similar to what is on [www.startuphouston.com](http://www.startuphouston.com).

## Project Structure

As with all Middleman projects, the real action lives in the `source` directory. A breakdown is a follows:

- **`source/`**: The `.html` and `.html.erb` files here are built into extension-less routes. For instance, `roflcopter.html.erb` will be accessible at the URL route `/roflcopter`. The same goes for subdirectories: a directory `foo` with file `bar.html.erb` will be accessible at the route `/foo/bar`.
  - **`fonts/`**: Custom fonts in use via CSS. Please do not place webfont files in the `stylesheets` directory.
  - **`javascripts/`**: JavaScript assets. Currently mostly unused. 
  - **`layouts/`**: HTML templates for entire page layouts.
  - **`stylesheets/`**:
    - **`breakpoint/`**: Files from our [Breakpoint](http://breakpoint-sass.com/) dependency.
    - **`pages/`**: Any page which needs custom SCSS (i.e. styling for elements that is not shared across pages) should have its own unique file here, nested in the same manner as the HTML file for the page. So a page at `sources/roflcopter.html.erb` should have its styles in `sources/stylesheets/pages/roflcopter.scss`.
    - **`pure/`**: Files for our [PureCSS](http://purecss.io) dependency.
    - `_base.scss`: A file for layout-wide and site-wide styles, along with one-off convenience classes, such as `rtext`, `ltext` and `ctext` for quick text-alignment setting. Do not put raw measurements here, i.e. `px`, `rem` or colors. These belong in `_variables.scss` instead.
    - `_breakpoint.scss`: Loads the breakpoint library.
    - `_fonts.scss`: For integrating and importing custom webfonts.
    - `_mixins.scss`: Site-wide SCSS mixins.
    - `_normalize.scss`: Coerces browsers (especially older ones) to render various components consistently. [Details here](https://necolas.github.io/normalize.css/).
    - `_pages.scss`: Explicit includes of SCSS files in the `source/stylesheets/pages/` directory, which correspond to any `.html.erb` files requiring custom styling under the `source/` directory.
    - `_variables.scss`: Static values of all sorts. Named colors of our theme, default font sizes, various common distances, breakpoints and more all defined here.
    - `site.scss`: **The main CSS file** included by the site layout. For the most part this should not need changes unless additional major dependencies or subfolders are added. Most of the styles are handled via SCSS partials included herein. For instance, specific pages are included in `_pages.scss`.
  - `index.html.erb`: The landing page for the entire site.

## SCSS Guidelines

- Use `rem`s and flexbox wherever possible.

## Deployment

To deploy this project, simply have Middleman build the site:
```shell
$ middleman build
```
The `build` directory now includes the entire site, ready for deployment wherever you see fit!
