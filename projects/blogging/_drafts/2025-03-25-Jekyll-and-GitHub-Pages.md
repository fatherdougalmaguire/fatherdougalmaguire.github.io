---
title: "Jekyll and GitHub pages"
layout: post
tags:
 - Jekyll
 - Blog
 - Minima
 - "GitHub Pages"
toc: false
excerpt: Having picked the SSG and hosting options,  the next step is start building something.
---
<div class="callout" style="color:black;"><img src="/assets/images/info-circle.svg" style="height: 20px; margin-top: -5px;fill: darkslateblue;padding-right: 1em;">The instructions and code within are current as of 25th March 2025.</div>

Having picked the SSG and hosting options,  the next step is start building something.

#### Which theme, disa theme

There is a large developer community that has built some very visually appealing templates or "themes" on top of Jekyll.

Samples of these can be found at [Jekyllthemes.io](https://jekyllthemes.io)

![Jekyllthemes.io](/assets/images/jekyllthemes.jpg)

Given this was going to be a learning experience,  I decided to go with the default theme [Minima](https://github.com/jekyll/minima) and tweak things.

#### Ruby Slippers

Jekyll is built using the [Ruby](https://www.ruby-lang.org/en/) language.

Code packages in Ruby are called **Gems**.

Jekyll itself is a Gem, as are the many **plugins** ( or extensions ) to Jekyll that enhance it's functionality.

Whilst not strictly required to build a blog, installing Ruby locally allows for a rapid create and test cycle on your computer.
Otherwise you are building directly on your hosting platform.

There are install instructions for [Windows](https://jekyllrb.com/docs/installation/windows/), [macOS](https://jekyllrb.com/docs/installation/macos/) and [various flavours of Linux.](https://jekyllrb.com/docs/installation/)

Once this is complete, you are almost ready to go.

You can follow the [Step by Step Tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/) on the Jekyll site to start from scratch or you can use something that already exists ( see above ).

#### GitHub au go go

As I am using GitHub pages to host my blog,  I am going to use the codebase for Minima.

A [GitHub account](https://docs.github.com/en/get-started/start-your-journey/creating-an-account-on-github) is required to host a blog on GitHub pages.

The free tier allows:

- One user site ( of the form **https://\<GitHubUsername\>.github.io** ) per account.
- Unlimited project sites ( of the form **https://\<GitHubUsername\>.github.io/project** ) per account.

I started with the user site for simplicity's sake.

GitHub ( as the name suggests ) uses [Git](https://github.com/git-guides) as it's distributed version control system.  
If you have no idea what version control system is,  it's worth spending some time perusing the guides in the link above.

In order to synchronize changes between GitHub and your computer,  at a minimum you will need to install the [Command line Git tools.](https://github.com/git-guides/install-git)
Personally,  I find a GUI to be much easier to work with so I use [GitHub Desktop](https://desktop.github.com/download/).
The choice basically comes down to personal preference.

##### Getting started

All screenshots are taken from macOS.  But the experience will be similar on Windows and Linux.

- Login to GitHub and go to the Minima GitHub repository
- Click on the Fork icon at the top

![Fork1](/assets/images/jekyll-github-1.jpg)

- Enter a repository name.  It should be of the form **<GitHubUsername\>.github.io** for a user site.

- Click on **Create Fork**

![Fork2](/assets/images/jekyll-github-2.jpg)

You'll now have a copy of the Minima code in your repository.  You'll need to clone this repository onto your computer.  
I'm going to demonstrate how it's done via GitHub Desktop.

- Click on **Code** and then **Open with GitHub Desktop**

![Fork3](/assets/images/jekyll-github-3.jpg)

GitHub Desktop prepopulates the repository name and picks a default location on your computer to store the local files.  
You can amend this location if you so desire and click **Clone**.

![Fork4](/assets/images/jekyll-github-4.jpg)

I'm not going to be pushing changes back to the main Minima repository so I'll choose the option **For my own purposes**.  
Click **Continue** to proceed.

![Fork5](/assets/images/jekyll-github-5.jpg)

You'll then see the standard GitHub desktop view.  We'll come back to this in a second.

![Fork6](/assets/images/jekyll-github-6.jpg)

Navigate to where you placed the minima source files.

![Fork7](/assets/images/jekyll-github-7.jpg)

Open the file \_**config.yml** and replace the contents with this :

```yaml
# Site-wide settings
# ------------------
#
title: Your awesome title
#
# author:
#   name: GitHub User
#   email: your-email@domain.com
#
# The `>` after `description:` means to ignore line-breaks until next key. If
#   you wish to omit the line-break after the end of text, use `>-` instead.
# description: >
#   Write an awesome description for your new site here. You can edit this line
#   in _config.yml. It will appear in your document head meta (for Google search
#   results) and in your feed.xml site description.


# Build settings
# --------------
#
# If you wish to use the gem-version of Minima with or without a Gemfile, use
#   the following setting:
theme: minima
#
# **OR** if you wish to use the theme directly from the GitHub repository by
#   bypassing a Gemfile, use the following setting instead.
#   It is best that you lock to a particular commit and update if uptream changes
#   do not affect your site adversely.
# remote_theme: jekyll/minima@d4d779a
#
# Minima requires the following plugins:
plugins:
- jekyll-feed
- jekyll-seo-tag
#
# Uncomment the following setting if you wish to disable deprecation warnings
#   from newer versions of sass converter. Adapt as required.
sass:
quiet_deps: true
silence_deprecations: [import]

# Minima-specific settings (applicable to Minima v3 and above only)
# -----------------------------------------------------------------
#
#  *All described config keys below should be nested under the top-level
#   `minima` key.*
#
minima:
#   Minima skin selection. Available skins are:
#     * classic            Default, light color scheme.
#     * dark               Dark variant of the classic skin.
#     * auto               Adaptive skin based on the classic and dark skins.
#     * solarized-light    Light variant of solarized color scheme.
#     * solarized-dark     Dark variant of solarized color scheme.
#     * solarized          Adaptive skin for solarized color scheme skins.
skin: classic
#
#   Specific pages for site navigation.
#     If you wish to link only specific pages in the site-navigation, use this
#     and list the `path` property (as represented via Liquid) of the pages in
#     the order they should be rendered.
nav_pages:
- about.md
#
#   Set to `true` to show excerpts on the homepage.
#   show_excerpts: false
#
#   Minima date format.
#     The default value is "%b %d, %Y" (e.g. Nov 14, 2023).
#     Refer to https://shopify.github.io/liquid/filters/date/ for valid values
date_format: "%b-%d-%Y"
#
#   Social Media Links.
#     Renders icons via Font Awesome Free webfonts CDN, based on ordered list of
#     entries. Valid entry keys:
#       * title    Tooltip rendered on hovering over icon.
#       * icon     Font Awesome icon id. `github` corresponds to `fa-github`.
#       * url      Full URL of social profile.
#   social_links:
#     - title: Minima Theme repository at GitHub
#       icon: github
#       url: "https://github.com/jekyll/minima"
#     - title: Jekyll at X (formerly Twitter)
#       icon: x-twitter
#       url: "https://x.com/jekyllrb"
#
#   Hide syndication feed subscription link.
#     RSS / Atom feed link is always rendered as the last item of social-links
#     list. Set below key to `true` to not have the link to feed rendered as
#     part of social-links list.
#   hide_site_feed_link: false
```







