---
draft: false
date: 2023-08-01
---

# How to Setup a Blog with GitHub Pages and mkdocs material

This blog is setup with [mkdocs](https://mkdocs.org) and [mkdocs-material](https://squidfunk.github.io/mkdocs-material).

I mostly just follow the mkdocs material instructions on [setting up a blog](https://squidfunk.github.io/mkdocs-material/setup/setting-up-a-blog/#built-in-blog-plugin) and [publishing to GitHub pages using GitHub Actions](https://squidfunk.github.io/mkdocs-material/publishing-your-site/#github-pages). But, I had to make some tweeks to get it to work. I explain below.

<!-- more -->

## Pipenv 

I use [pipenv](https://pipenv.pypa.io/en/latest/) to manage the dependencies. This means that I have a `Pipfile` and `Pipfile.lock` in the root of the project.

I found that only version 9.2 of mkdocs-material implements blogs, and that version is still in beta. So, to get pipenv to install the beta version we have put the following in the `Pipfile`:

```toml
[packages]
mkdocs = "*"
mkdocs-material = ">=9.2.0b2"
```

## GitHub Workflow

To get the GitHub workflow to use pipenv, I change the workflow run statement to:

```yaml
      - run: pip install pipenv
      - run: pipenv install --deploy --dev
      - run: pipenv run mkdocs gh-deploy --force
```




