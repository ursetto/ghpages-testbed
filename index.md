# Github pages testbed

This is a testbed. Lorum ipsum, etc. See it on [GitHub Pages](https://ursetto.github.io/ghpages-testbed) aka [site.url]({{ site.github.url }}). During local testing, `site.url` incorrectly points to 404 URL https://github.com/pages/ursetto/ghpages-testbed, but it works fine on GitHub.

## Notes

### Basic site

GitHub Pages is on the main Settings page; scroll down to the bottom.

For a basic site without Jekyll,

- `.html` files are passed through unchanged.
- A file `/path/to/xyz.md` is available as `/path/to/xyz.html` (and also as `/path/to/xyz`).
- /path/to/xyz will serve /path/to/xyz.html. This is true whether GitHub generated the .html from an .md, or if you uploaded the .html directly.
- Jekyll is still used to generate the site.


### Jekyll site

[Setting up GH Pages with Jekyll](https://docs.github.com/en/github/working-with-github-pages/setting-up-a-github-pages-site-with-jekyll)

A Jekyll site created on GitHub Pages doesn't have a Gemfile. To test it locally, create a Gemfile in the publishing source directory (`/` or `/docs`):

```ruby
source 'https://rubygems.org'
gem "github-pages", "~> 211", group: :jekyll_plugins
```

where 211 comes from [Dependency versions](https://pages.github.com/versions/). This contains the correct version of Jekyll and every Github Pages plugin needed including themes. 

It's unclear if committing the Gemfile and/or Gemfile.lock will affect the build process on github.com. This could be tested by creating an invalid gemfile and pushing.

Install gems once:

```sh
bundle install
```

Serve site locally:

```
bundle exec jekyll serve
```

On macOS I'm using ruby@2.7 from Homebrew (with `/usr/local/opt/ruby@2/bin` at front of path) for compatibility.

### Github metadata

[Github Metadata -- using site.github](http://jekyll.github.io/github-metadata/site.github/)



### Creating a new jekyll site from scratch

Not really explored, but if you are playing around and want github-pages testing to work before creating a github repo, add the following to `_config.yml` temporarily to avoid an error during build:

```yaml
repository: 'ursetto/repo-name'
```

Official instructions to create a new site don't work well. If you create a Gemfile referring to `jekyll` as instructed and run `bundle install` and `bundle exec jekyll new .`, it will require `--force` to overwrite the current Gemfile with Jekyll's updates, and then `bundle install` won't work (missing timezone gem or something).

Instead it works to do the initial install from a common directory, then specify a path instead of `.` to `jekyll new`. It might also work to use `github-pages` in the Gemfile instead of `jekyll`.
