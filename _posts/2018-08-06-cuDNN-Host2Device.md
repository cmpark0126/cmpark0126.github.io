---
title:  "cuDNN - Host memory에서 Device memory로 옮기는 법"
modified: 2018-08-06T17:00:00-:30:00
categories:
  - Develop
tags:
  - cuDNN
  - WICWIU
  - DeepLearning
  - Framework
---

{% include base_path %}

{% include toc title="cuDNN_Host2Memory" %}

cuDNN은 nvidia gpu를 사용할 때, 특히 딥러닝 파트를 구현할 때, 거의 필수적으로 사용되고 있는 라이브러리이다.

물론 일부 라이브러리는 cuda를 이용해서 딥러닝 알고리즘을 직접 구현하기도 하지만 (대부분의 슈퍼 개발자는 아무래도 그게 더 편하려나) 나같이 gpu 코딩 자체가 익숙하지 않은 사람들에게는 그게 쉽지 않다.


[`minimal-mistakes-jekyll`](https://rubygems.org/gems/minimal-mistakes-jekyll) can only be used with Jekyll proper. If you're hosting on GitHub Pages or using that gem the theme won't work. 3rd party themes haven't been white-listed so it's a no go for now.

Fine with all that? Great. Let's continue.

If you're migrating a site already using Minimal Mistakes and haven't customized any of the `_includes`, `_layouts`, `_sass` partials, or `assets` this should be quick and painless.

## Step 1: Remove Theme Files

Remove `_includes`, `_layouts`, `_sass`, `assets` folders and files within. You won't need these anymore as they're bundled in the theme.

If you customized any of these then leave them alone and only remove the untouched ones. If setup correctly your modified versions should act as [overrides](http://jekyllrb.com/docs/themes/#overriding-theme-defaults) to the versions bundled with the theme.

## Step 2: Update `Gemfile`

Replace `gem "github-pages` or `gem "jekyll"` with `gem "jekyll", "~> 3.3.0"`. You'll need the latest version of Jekyll[^update-jekyll] for Minimal Mistakes to work and load all of the /assets/ properly.

[^update-jekyll]: You could also run `bundle update jekyll` to update Jekyll.

Add the Minimal Mistakes theme gem:

```ruby
gem "minimal-mistakes-jekyll"
```

When finished your `Gemfile` should look something like this:

```ruby
source "https://rubygems.org"

gem "jekyll", "~> 3.3.0"
gem "minimal-mistakes-jekyll"
```

## Step 3: Run Bundler

Run `bundle install` (or `bundle update` if you're updating an existing repo) to install/update Jekyll and the theme.

## Step 4: Install the Theme

Add `theme: "minimal-mistakes-jekyll"` to your `_config.yml` file.

If you're migrating from an existing Minimal Mistakes site you shouldn't have to change anything else after this. If it's a new site consult then docs to [properly config]({{ base_path }}/docs/configuration/).

**Please Note:** Paths for image headers, overlays, teasers, [galleries]({{ base_path }}/docs/helpers/#gallery), and [feature rows]({{ base_path }}/docs/helpers/#feature-row) have changed and now require a full path. Instead of just `image: filename.jpg` you'll need to use the full path eg: `image: assets/images/filename.jpg`. The preferred location is now `assets/images` but can be placed elsewhere or external hosted. This all applies for image references in `_config.yml` and `author.yml` as well.
{: .notice--danger}

## Step 5: `jekyll new` Tweaks

If this is a new site be sure to add the following files to `_data/` and customize as you see fit. There is currently no way of bundling them in with the theme, so be sure to consult the docs on how to properly use both.

- [`_data/ui-text.yml`](https://github.com/mmistakes/minimal-mistakes/blob/master/_data/ui-text.yml) - UI text [documentation]({{ base_path }}/docs/ui-text/)
- [`_data/navigation.yml`](https://github.com/mmistakes/minimal-mistakes/blob/master/_data/navigation.yml) - navigation [documentation]({{ base_path }}/docs/navigation/)

You'll also need to:

- Replace `<site root>/index.html` with a modified [Minimal Mistakes `index.html`](https://github.com/mmistakes/minimal-mistakes/blob/master/index.html).
- Change `layout: post` in `_posts/0000-00-00-welcome-to-jekyll.markdown` to `layout: single`.
- Remove `about.md`, or at the very least change `layout: page` to `layout: single` and remove references to `icon-github.html` (or [copy to your `_includes`](https://github.com/jekyll/minima/tree/master/_includes) if using).

---

That's it! If all goes well running `bundle exec jekyll serve` should spin-up your site. If you encounter any bumps please file an issue on GitHub and make sure to indicate you're testing the pre-release Ruby gem version.

[File an issue](https://github.com/mmistakes/minimal-mistakes/issues/new){: .btn .btn--info .btn--large}

Thanks!
