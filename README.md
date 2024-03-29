# I only wrote the first paragraph
This repo supports paulsambolin.com where I write about technology and everything Do It Yourself (DIY).  The rest of this readme is from the original website template, my thanks to the original author.

test

# Chirpy

Language: English | [简体中文](https://github.com/cotes2020/jekyll-theme-chirpy/blob/master/docs/README.zh-CN.md)

[![Build Status](https://github.com/cotes2020/jekyll-theme-chirpy/workflows/build/badge.svg?branch=master&event=push)](https://github.com/cotes2020/jekyll-theme-chirpy/actions?query=branch%3Amaster+event%3Apush)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/8220b926db514f13afc3f02b7f884f4b)](https://app.codacy.com/manual/cotes2020/jekyll-theme-chirpy?utm_source=github.com&utm_medium=referral&utm_content=cotes2020/jekyll-theme-chirpy&utm_campaign=Badge_Grade_Dashboard)
[![GitHub license](https://img.shields.io/github/license/cotes2020/jekyll-theme-chirpy.svg)](https://github.com/cotes2020/jekyll-theme-chirpy/blob/master/LICENSE)
[![Gem Version](https://img.shields.io/gem/v/jekyll-theme-chirpy?color=important)](https://rubygems.org/gems/jekyll-theme-chirpy)
[![996.icu](https://img.shields.io/badge/link-996.icu-%23FF4D5B.svg)](https://996.icu)

A minimal, sidebar, responsive web design Jekyll theme that focuses on text presentation. Designed to help you record and share your knowledge easily. [Live Demo »](https://chirpy.cotes.info)

[![Devices Mockup](https://cdn.jsdelivr.net/gh/cotes2020/chirpy-images/commons/devices-mockup.png)](https://chirpy.cotes.info)

## Table of Contents

- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [Credits](#credits)
- [Supporting](#supporting)
- [License](#license)

## Features

- Pinned Posts
- Configurable theme mode
- Double-level Categories
- Last modified date for posts
- Table of Contents
- Automatically recommend related posts
- Syntax highlighting
- Mathematical expressions
- Mermaid diagram & flowchart
- Search
- Atom Feeds
- Disqus Comments
- Google Analytics
- GA Pageviews reporting (Advanced)
- SEO and Performance Optimization

## Prerequisites

Follow the [Jekyll Docs](https://jekyllrb.com/docs/installation/) to complete the installation of `Ruby`, `RubyGems`, `Jekyll` and `Bundler`.

## Installation

There are two ways to get the theme:

- Install from [RubyGems](https://rubygems.org/gems/jekyll-theme-chirpy)
- Fork from GitHub

### Install From Rubygems

Add this line to your Jekyll site's `Gemfile`:

```ruby
gem "jekyll-theme-chirpy"
```

And add this line to your Jekyll site's `_config.yml`:

```yaml
theme: jekyll-theme-chirpy
```

And then execute:

```console
$ bundle
```

Finally, copy the extra files (refer to the [starter project][starter] for the detailed file directory structure) from the theme's gem to your Jekyll site, and append all the variables of the theme's `_config.yml` to your Jekyll site.

> **Hint**: To locate the theme’s gem, execute:
>
```console
$ bundle info --path jekyll-theme-chirpy
```

Or you can [use the starter template][use-starter] to create a Jekyll site to save time copying contents from theme's gem.

### Fork From GitHub

[Fork **Chirpy**](https://github.com/cotes2020/jekyll-theme-chirpy/fork) from GitHub and clone your fork to local.

Install gem dependencies by:

```console
$ bundle
```

And then execute:

```console
$ bash tools/init.sh
```

> **Note**: If you don't plan to deploy your site on GitHub Pages, append parameter option `--no-gh` at the end of the above command.

What it does is:

1. Remove some files or directories from your repository:
    - `.travis.yml`
    - files under `_posts`
    - folder `docs`

2. If you use the `--no-gh` option, the directory `.github` will be deleted. Otherwise, setup the GitHub Action workflow by removing extension `.hook` of `.github/workflows/pages-deploy.yml.hook`, and then remove the other files and directories in folder `.github`.

3. Automatically create a commit to save the changes.

## Usage

### Configuration

Update the variables of `_config.yml` as needed. Some of them are typical options:

- `url`
- `avatar`
- `timezone`
- `theme_mode`

### Running Local Server

You may want to preview the site contents before publishing, so just run it by:

```console
$ bundle exec jekyll s
```

Or run the site on Docker with the following command:

```terminal
$ docker run -it --rm \
    --volume="$PWD:/srv/jekyll" \
    -p 4000:4000 jekyll/jekyll \
    jekyll serve
```

Open a browser and visit to _<http://localhost:4000>_.

### Deployment

Before the deployment begins, checkout the file `_config.yml` and make sure the `url` is configured correctly. Furthermore, if you prefer the [**project site**](https://help.github.com/en/github/working-with-github-pages/about-github-pages#types-of-github-pages-sites) and don't use a custom domain, or you want to visit your website with a base url on a web server other than **GitHub Pages**, remember to change the `baseurl` to your project name that starting with a slash, e.g, `/project-name`.

Now you can choose ONE of the following methods to deploy your Jekyll site.

#### Deploy on GitHub Pages

For security reasons, GitHub Pages build runs on `safe` mode, which restricts us from using plugins to generate additional page files. Therefore, we can use **GitHub Actions** to build the site, store the built site files on a new branch, and use that branch as the source of the GH Pages service.

Quickly check the files needed for GitHub Actions build:

1. Ensure your Jekyll site has the file `/.github/workflows/pages-deploy.yml`. Otherwise, create a new one and fill in the contents of the [workflow file][workflow], and the value of the `on.push.branches` should be the same as your repo's default branch name.
2. Ensuer your Jekyll site has file `/tools/test.sh` and `/tools/deploy.sh`. Otherwise, copy them from this repo to your Jekyll site.

Next, rename your repoistory to `<GH-USERNAME>.github.io` on GitHub.

And then publish your Jekyll site by:

1. Push any commit to remote to trigger the GitHub Actions workflow. Once the build is complete and successful, a new remote branch named `gh-pages` will appear to store the built site files.

2. Browse to your repo's landing page on GitHub and select the branch `gh-pages` as the [publishing source](https://docs.github.com/en/github/working-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site) throught _Settings_ → _Options_ → _GitHub Pages_:

    ![gh-pages-sources](https://cdn.jsdelivr.net/gh/cotes2020/chirpy-images/posts/20190809/gh-pages-sources.png)

3. Visit your website at the address indicated by GitHub.

#### Deploy on Other Platforms

On platforms other than GitHub, we cannot enjoy the convenience of **GitHub Actions**. Therefore, we should build the site locally (or on some other 3rd-party CI platform) and then put the site files on the server.

Go to the root of the source project, build your site by:

```console
$ JEKYLL_ENV=production bundle exec jekyll b
```

Or build the site with Docker by:

```terminal
$ docker run -it --rm \
    --env JEKYLL_ENV=production \
    --volume="$PWD:/srv/jekyll" \
    jekyll/jekyll \
    jekyll build
```

Unless you specified the output path, the generated site files will be placed in folder `_site` of the project's root directory. Now you should upload those files to your web server.

## Documentation

For more details and the better reading experience, please check out the [tutorials on demo site](https://chirpy.cotes.info/categories/tutorial/). In the meanwhile, a copy of the tutorial is also available on the [Wiki](https://github.com/cotes2020/jekyll-theme-chirpy/wiki).

## Contributing

The old saying, "Two heads are better than one." Consequently, welcome to report bugs, improve code quality or submit a new feature. For more information, see [contributing guidelines](.github/CONTRIBUTING.md).

## Credits

This theme is mainly built with [Jekyll](https://jekyllrb.com/) ecosystem, [Bootstrap](https://getbootstrap.com/), [Font Awesome](https://fontawesome.com/) and some other wonderful tools (their copyright information can be found in the relevant files).

:tada: Thanks to all the volunteers who contributed to this project, their GitHub IDs are on [this list](https://github.com/cotes2020/jekyll-theme-chirpy/graphs/contributors). Also, I won't forget those guys who submitted the issues or unmerged PR because they reported bugs, shared ideas or inspired me to write more readable documentation.

Also, thank [JetBrains][jb] for providing the open source license.

[![JB-logo](https://cdn.jsdelivr.net/gh/cotes2020/chirpy-images/commons/jetbrains.svg)][jb]

## Supporting

If you enjoy this theme or find it helpful, please consider becoming my sponsor, I'd really appreciate it! Click the button <kbd>:heart: Sponsor</kbd> at the top of the [Home Page](https://github.com/cotes2020/jekyll-theme-chirpy) and choose a link that suits you to donate; this will encourage and help me better maintain the project.

## License

This work is published under [MIT](https://github.com/cotes2020/jekyll-theme-chirpy/blob/master/LICENSE) License.

[starter]: https://github.com/cotes2020/chirpy-starter
[use-starter]: https://github.com/cotes2020/chirpy-starter/generate
[workflow]: https://github.com/cotes2020/jekyll-theme-chirpy/blob/master/.github/workflows/pages-deploy.yml.hook
[jb]: https://www.jetbrains.com/?from=jekyll-theme-chirpy

