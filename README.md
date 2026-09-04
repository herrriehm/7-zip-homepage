# 7-zip.de

This is just a repository for collaborative work on 7-zip.de.

We finally make the transition from HTML4 to HTML5. And from pure .html files to a
maintenance friendly, Python-based template system thanks to glamorous
[Nikola](https://getnikola.com/) static site generator! 🚀

## How the site is published

Content is edited **locally**, pushed to GitHub, and pulled on the Uberspace server,
where the site is built and deployed. The server never pushes.

    local edit → git commit → git push → (on server) git pull → nikola build → nikola deploy

`nikola build` writes to `output/`; `nikola deploy` mirrors that into the live
document root with `rsync -a --delete`. Nothing touches the live site until the
deploy step, so a failed build cannot break the running page.

## Server setup (Uberspace)

The build runs in a dedicated virtualenv on **Python 3.13**. Uberspace's default
`python3` is 3.9, which reached end of life in October 2025 — always call `python3.13`
explicitly.

    python3.13 -m venv ~/nikola-venv
    source ~/nikola-venv/bin/activate
    pip install -r requirements.txt

`requirements.txt` pins every package, so this recreates the exact environment the
site was last built with.

## Building and deploying

    source ~/nikola-venv/bin/activate
    cd ~/7zipde
    git pull
    nikola build
    nikola deploy

To force a complete rebuild (useful after upgrading Nikola or changing the theme):

    rm -rf output .doit.db cache/ && nikola build

## Updating dependencies

Upgrade, verify, *then* freeze — never the other way around:

    source ~/nikola-venv/bin/activate
    pip install -U Nikola
    rm -rf output .doit.db cache/ && nikola build
    diff -rq output/ ~/html/          # inspect what would change before deploying
    nikola deploy
    pip freeze | grep -v '^setuptools==' > requirements.txt

Commit the new `requirements.txt` locally so the environment stays documented.
`setuptools` is excluded on purpose: it is a build tool only, unused at runtime.

## Local development

Content is normally edited locally and built on the server, so no local Nikola
installation is required. If you do want a local preview with live reload, note that
`nikola auto` additionally needs `aiohttp` and `watchdog`, which are deliberately not
part of `requirements.txt`:

    pip install -r requirements.txt aiohttp watchdog
    nikola auto

After cloning, enable the repository's git hooks once:

    git config core.hooksPath .githooks

`.githooks/pre-commit` validates `data/*.json` before a commit, so a typo in the news
file is caught here rather than breaking the build on the server.

## Notes on the setup

* **Content** is reStructuredText (`pages/*.rst`). Markdown and Jupyter support are
  switched off via `DISABLED_PLUGINS` in `conf.py`.
* **News** live in `data/news.json` and are rendered by the `news_sidebar` macro in
  `themes/7ztheme/templates/post_helper.tmpl`. JSON is read by Python's standard
  library, so the file needs no extra dependency — unlike the YAML it replaced.
* **Theme** `themes/7ztheme` uses the Mako template engine and inherits from Nikola's
  built-in `base`. Mako is a hard dependency of Nikola itself, so the theme adds no
  package of its own. Note that `conf.py` must therefore *not* list `"mako"` in
  `DISABLED_PLUGINS` — that setting applies to template engines too, and Nikola would
  abort with `Error loading mako template system plugin`.
* **CSS** is compiled from `themes/7ztheme/less/style.less` by the local `plugins/less`
  plugin, which calls `lessc` (`~/bin/lessc` on the server).
* **`ROBOTS_EXCLUSIONS`** in `conf.py` keeps `support.html` out of `robots.txt` and
  `sitemap.xml`. Do not hand-edit files in the live document root — `nikola deploy`
  runs with `--delete` and will silently discard such changes.
