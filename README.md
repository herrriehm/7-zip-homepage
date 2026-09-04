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

Scripts installed into a virtualenv carry that venv's interpreter in their shebang
(`#!/home/sevenzip/nikola-venv/bin/python`), so `nikola` runs correctly even without
activating the venv first. Uberspace has `~/bin` on `PATH` by default, so linking it
there makes the command available everywhere:

    ln -sf ~/nikola-venv/bin/nikola ~/bin/nikola

This is preferable to auto-activating the venv in a shell startup file, which would
silently redirect `python` and `pip` — not just `nikola` — for every shell.

## Building and deploying

    source ~/nikola-venv/bin/activate
    cd ~/7zipde
    git pull
    nikola build
    nikola deploy

To force a complete rebuild (useful after upgrading Nikola or changing the theme):

    rm -rf output .doit.db cache/ && nikola build

## Adding a news entry

This is the most frequent maintenance task — announcing a new 7-Zip release. The news
box on the front page is driven by `data/news.json`, a JSON array of objects. **The
newest entry goes at the top**: the order in the file is the order shown on the page.

Each object has four fields:

* `newstitle` — the bold heading, e.g. the version number.
* `newsdate` — shown next to the title. May be `""`, in which case the date span is
  omitted entirely (used for the evergreen changelog link).
* `newsurl` — if non-empty, `newstext` becomes a link to it.
* `newstext` — the link text, or the body when `newsurl` is empty.

Note the asymmetry in `news_sidebar`: with a `newsurl`, both it and `newstext` are
HTML-escaped; without one, `newstext` is inserted **unescaped**, which is deliberate —
it is what allows small tags such as `<br>` or an inline link. The practical consequence
is that in a link-less entry a literal `<` starts a tag rather than showing up as text.
A bare `&` is safe either way: Nikola pipes every page through `lxml`, which normalises
it to `&amp;`.

To add a release, insert a new object at the top of the array — and remember the comma
after it, since it is now followed by the previous entries:

    [
      {
        "newstitle": "7-Zip 26.04",
        "newsdate": "12.10.2026",
        "newsurl": "https://sourceforge.net/p/sevenzip/discussion/45797/thread/xxxxxxxxxx/",
        "newstext": "7-Zip 26.04"
      },
      … previous entries follow …
    ]

JSON is strict: a comma between objects but none after the last one, no comments, and
umlauts written as plain UTF-8 (no `\uXXXX` escapes). `.githooks/pre-commit` validates
the file on commit, so a syntax error is caught locally rather than breaking the build
on the server; check it manually with `python3 -m json.tool data/news.json`.

Then the normal flow applies: commit, push, and on the server
`git pull && nikola build && nikola deploy`.

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
* **CSS** is a static file at `files/assets/css/style.css`, copied verbatim into the
  output by `FILES_FOLDERS`. There is no CSS build step and no Node/lessc dependency.
* **`copy_assets` is disabled** in `DISABLED_PLUGINS`. The pages link exactly one
  stylesheet and no scripts, so the parent theme's assets (luxon, baguetteBox, the
  gallery and reStructuredText CSS, …) were 20 files and ~160 KB of never-requested
  payload. Re-enable it if the theme ever starts using inherited assets.
* **`ROBOTS_EXCLUSIONS`** in `conf.py` keeps `support.html` out of `robots.txt` and
  `sitemap.xml`. Do not hand-edit files in the live document root — `nikola deploy`
  runs with `--delete` and will silently discard such changes.
