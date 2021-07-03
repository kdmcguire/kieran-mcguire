+++
title = "Building This Site"
date = "2021-06-24T14:54:59+01:00"
author = "Kieran"
authorTwitter = "kmcguire_dev" #do not include @
cover = "img/hugo-3.webp"
tags = ["tech", "Hugo", "JAMstack"]
keywords = ["blog", "Hugo", "Static Site Generator"]
description = "How it works!"
showFullContent = false
draft = false
+++

This blog is relatively minimal, and has only three core parts:

1. Hugo (which requires Go).
2. The "Terminal" theme for Hugo.
3. Netlify.

## What is Hugo?

[Hugo](https://gohugo.io/) is a [Static Site Generator](https://jamstack.org/glossary/ssg/). It takes structured data, templates, and content written in markdown, and turns them into a website made up of static files.

Why is this good? Well, it's quick. Very quick. Things are much simpler and much faster when your website is just a collection of static files, rather than a content management system connected to a database that has to process and think about lots of little things and moving parts in every page request.

Here's how Hugo describes itself:

> Hugo is a static HTML and CSS website generator written in Go. It is optimized for speed, ease of use, and configurability. Hugo takes a directory with content and templates and renders them into a full HTML website.
>
> Hugo relies on Markdown files with front matter for metadata, and you can run Hugo from any directory. This works well for shared hosts and other systems where you don’t have a privileged account.
>
> Hugo renders a typical website of moderate size in a fraction of a second. A good rule of thumb is that each piece of content renders in around 1 millisecond.
>
> Hugo is designed to work well for any kind of website including blogs, tumbles, and docs.

## Installing Go & Hugo

Since Hugo is built in the Go programming language, you need to install Go first if you want to use Hugo on your machine.

Both Go and Hugo have installers for different platforms that you can get from GitHub.

- [Go releases](https://github.com/golang/go/releases).
- [Hugo releases](https://github.com/gohugoio/hugo/releases).

If you're on Windows and have access to **winget**, the new package management tool, you can install Go with this command: `winget install GoLang.Go`

(Sadly Hugo is not yet available for installation with winget.)

Once Hugo is installed - and after you've explored and experimented, following their '[Quick Start](https://gohugo.io/getting-started/quick-start/)' documentation - you can start building your own site.

## Installing the Terminal theme

I was looking for something dark and simple, and the demo for this theme was imbued with references to the Mr. Robot TV show so it was pretty much a done deal.

It's made by [@panr](https://github.com/panr/) and is available on GitHub at <https://github.com/panr/hugo-theme-terminal>.

The "How to start" section of the Readme mentions a few ways of installing this theme:

1. Manually download and copy the files into your site's /themes/ folder.
2. Use `git clone`.
3. Use `git submodule`.

If I was to roughly summarize each one, I would say:

1. The **manual** method is most useful when you want to do lots of customisation, but it doesn't help you with updates from the source repository.
2. `git clone` is a commonly recommended method, but doesn't work with hosting platforms (like Netlify!) that *don't like it when you use `git clone` to bring a nested repository into your repository*. (See their note on this in their documentation about [deploying a Hugo site with a theme](https://docs.netlify.com/configure-builds/common-configurations/hugo/#hugo-themes).)
3. `git submodule` is like `git clone` with cleaner separation, but it's also more complex and more finnicky. On paper, it should have worked with Netlify but it didn't work for me.

However, I have opted for a fourth method: **Hugo modules**.

I don't understand Go or Hugo well enough to give a perfect explanation here, but Hugo modules are essentially like building blocks that can simplify how you put your site together. You list your requirements in the right place, and presto! Hugo does the ~~hard work~~ magic for you.

### Installing the Terminal theme as a Hugo module

In my site's `config.toml` file, I have these lines at the top:

```toml
# theme = ""

[module]
  [[module.imports]]
    path = "github.com/panr/hugo-theme-terminal"
```

Then, in my terminal (Windows Terminal - it's good now) I ran `hugo mod init kieran-mcguire`. This sets your site up to use Hugo modules and then fetches and installs this theme.

Then finish the rest of the `config.toml` file, following the guidance of the Hugo and Terminal theme documentation.

## Deploying to Netlify

I chose Netlify because it makes things incredibly easy for me, the developer, and their platform is very fast. I *really* want this site to be fast.

If you're logged in to Netlify and GitHub, you can give Netlify permission to access your GitHub account and create and deploy sites from your GitHub repositories. Create a site in Netlify, connect it to your GitHub repository, and it's done.

It's out-of-the-box Continuous Integration / Continuous Deployment, which is what every project should aim to start with.

## Wrapping up

That's it! Install Go (ideally with winget or another package manager), Install Hugo (manually), install the theme (as a Hugo module), and connect the repository and deploy to Netlify.

That is how you're reading this now.
