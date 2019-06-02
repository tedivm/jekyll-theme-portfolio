# Portfolio Page for Github Pages

The goal of this project is to make it easy for people who want to host their portfolio to actually do so without having to jump through a ton of hoops or pay any money. I originally made this for [my own portfolio](https://projects.tedivm.com/) after realizing that all the existing portfolio themes were expensive or required extensive customization.

This project is a [Jekyll](https://jekyllrb.com/) theme, which means that it can be used to set up a free website on [Github Pages](https://pages.github.com/).

It is possible to use this theme without understanding anything about building websites. It works by using a configuration file to store all of your projects, which it then displays (including logos, descriptions, and a variety of links). This way when you want to add a new project all you have to do is add a few lines to a configuration and it will appear.

It is also possible to go beyond that and customize the project right down to the CSS. This theme is made with [Bootstrap 4](https://getbootstrap.com/) and [SCSS](https://sass-lang.com/documentation/syntax).


![alt text](https://raw.githubusercontent.com/tedivm/jekyll-theme-portfolio/master/screenshot.png)


## Getting Started

### Setup a Github Pages Site

Github has a great [Getting Started with Github Pages](https://fontawesome.com/icons/chess-pawn?style=solid) tutorial.


### Configure your Site

At this point you should have a `_config.yml` file. You can just replace it with the one below, filled out with your details.

```yaml

# This is how Jekyll knows to use this theme.
remote_theme: tedivm/jekyll-theme-portfolio


title: Your awesome title
author: Your Name
email: your-email@domain.com
description: >
  Write an awesome description for your new site here. You can edit this
  line in _config.yml. It will appear in your document head meta (for
  Google search results) and in your feed.xml site description.


# Header Links - all optional. If set these create header links.
homepage: https://your.homepage.com
twitter_username: example
github_username: example
linkedin_username: example


plugins:
 - jekyll-feed
 - jekyll-seo-tag
 - jekyll-remote-theme # Lets us test remote themes locally.

```


### Create your Portfolio Page

If you have a one page site then you should create your portfolio page at `index.html` or `index.md`, but for multipage sites you can create it anywhere you want. Either way the file only contain the following to start (if there's anything after the last three dashes remove it for now)-

```
---
layout: portfolio
---
```

This tells Jekyll to use the `portfolio` layout for the page, which lets the theme take care of the rest.

If you prefer two columns instead of three you can use the two column layout instead-

```
---
layout: portfolio_2column
---
```

If you leave any content in the file it will show up above the portfolio listings.

```
---
layout: portfolio
---
<h2> Welcome!</h2>
```


### Add your Projects

Project details are stored in `_data/projects.yaml`.


## Defining Projects

Projects are defined using the `yaml`, which is like `json` but friendly for humans to edit.

Before diving into all of the options, lets look at an example projects file. This file has a single category, named `Libraries`, with four projects underneath it. Each of those projects has a variety of configuration values (most of which are optional) that tell the theme what to display.

```yaml

- name: Libraries
  projects:
    - name: Stash
      description: This caching library supports multiple backends with a consistent frontend. It supports hierarchical keys, stampede and dogpile protection, automatic miss distribution, and more.
      github: tedious/Stash
      documentation: https://www.stashphp.com/
      packagist: tedivm/stash
      icon: fab fa-php

    - name: JShrink
      description: This library minifies javascript using 100% pure PHP, allowing it to be integrated into applications with minimal work and maximum compatibility.
      github: tedious/JShrink
      packagist: tedivm/jshrink
      icon: fab fa-php

    - name: github3apps.py
      description: This library is a wrapper around the <a href="https://github.com/sigmavirus24/github3.py">github3.py</a> library, giving it the ability to build GitHub Applications.
      github: tedivm/github3apps.py
      pypi: github3apps.py
      icon: fab fa-github

    - name: Fetch
      description: This library wraps the native PHP IMAP libraries around a modern object orientated interface.
      github: tedious/Fetch
      packagist: tedivm/fetch
      icon: fab fa-php

    - name: psad
      description: This Puppet module controls the Port Scan Active Defense program, providing active response to block port scans.
      puppet_forge: tedivm/psad
      github: tedivm/puppet-psad
      image: puppet.png

```

For a larger example you can view [tedivm's portfolio data](https://github.com/tedivm/portfolio/blob/master/_data/projects.yaml).

### Project Fields

There is only one required configuration values for each project, the `name`. If you put this and nothing else the project will get displayed using the default project icon and no description or links.

The `description` field is where you actually describe the project. You can put `html` in here if you want, which can be useful for linking to related projects.

Then there are a variety of repository options that can be used. Each of these will add an icon below the project description linking to that project in that particular repository or site-

* `homepage`
* `documentation`
* `github` - this will also add the `stars` link to the project.
* `dockerhub`
* `puppet_forge`
* `npm`
* `pypi`
* `packagist`
* `rubygems`
* `wordpress`

If there's a repository or site that isn't supported [open a ticket](https://github.com/tedivm/jekyll-theme-portfolio/issues/new?title=Please+add+project+link+support+for+X&body=Here%27s+an+example+link%3A+) and it should be simple to get it added.


### Images and Icons

Each project has a picture above it. The picture comes from either the `icon` or the `image` option of the project.

Icons come from [FontAwesome](https://fontawesome.com/icons?d=gallery&m=free). To use them you have to use the full class name, such as `fab fa-github` for [Github](https://fontawesome.com/icons/github?style=brands) or `fas fa-chess-pawn` for [the Pawn](https://fontawesome.com/icons/chess-pawn?style=solid).

Images should be supplied by you. Any images should be added to `assets/images/projects`, afterwhich they can be used in any `image` by using the filename (such as `image: puppet.png`).

You can also use `icon` and `image` at the category level. This will set the default for that category.

### Github Stars

The Github Star badges are using the [GithubStars API](https://blog.tedivm.com/open-source/2019/05/gitstars-a-github-api-for-front-end-development/). This bypasses various Github API ratelimiting issues that plague many Github Badge projects.


## Customizing

### Changing Colors

To override the existing colorscheme of the portfolio you're going to need to copy the variables file from [this theme's github page](https://raw.githubusercontent.com/tedivm/jekyll-theme-portfolio/master/_sass/_variables.scss) into `_sass/_variables.scss`. This will tell Jekyll to stop using the theme file and instead use yours.

Once there the first thing you'll likely want to change is the `$primary` color, which you should be able to fine on line 40. This variable is used for the header and the various project icons. You can set it to any of the colors defined above it (`$blue`, `$indigo`, `$pink`, etc) or to any hex code you'd like.


### Adding a FavIcon

There are all sorts of websites and tools which will help you make your favicon file. Once you have you just need to dump it into the repository as `favicon.ico` and it will start showing up.


### Using a Custom Domain

Github supports [custom domains](https://help.github.com/en/articles/using-a-custom-domain-with-github-pages), as you can see from their extensive documention.

Long story short, point the DNS for your domain to `username.github.io` as a CNAME record and then add a file named `CNAME` with that domain as the file contents.


### Adding Analytics

This theme supports two website analytics options- [Fathom](https://usefathom.com/), which is an [open source](https://github.com/usefathom/fathom) and privacy focused analytics package, or theres [Google Analytics](https://google.com/analytics). Both require a simple addition to your configuration file to use.

Fathom takes a Site ID and optionally a URL (if you're hosting it yourself instead of using their service).

```
fathom_key: DXQMN
fathom_domain: fathom.example.net
```

For Google Analytics you only need the one option.

```
google_analytics: UA-XXXXX-Y
```


## Awknowledgements

This project was forked off of the excellent [Boostrap 4 Github Pages project](https://github.com/nicolas-van/bootstrap-4-github-pages).

* A full Bootstrap 4 theme usable both on Github Pages and with a standalone Jekyll.
* Recompiles Bootstrap from SCSS files, which allows to customize Bootstrap's variables and use Bootstrap themes.
* Full support of Bootstrap's JavaScript plugins.
* Supports all features of Github Pages and Jekyll.
