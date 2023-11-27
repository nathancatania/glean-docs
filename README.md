# help.glean.com
PoC Glean Help Portal based on Mkdocs Material

## Setup
The [insiders](https://squidfunk.github.io/mkdocs-material/insiders/) version of Mkdocs Material is used which gives us additional features only available to sponsors of the project ($15/month). You will need a GH_TOKEN set as per the [instructions here](https://squidfunk.github.io/mkdocs-material/insiders/getting-started/) to access the insiders build.

#### Install [Mkdocs Material (Insiders)](https://github.com/squidfunk/mkdocs-material-insiders):
```
export GH_TOKEN=insert_github_token_here
pip install git+https://${GH_TOKEN}@github.com/squidfunk/mkdocs-material-insiders.git@9.4.2-insiders-4.42.0
```
NB: List of releases is here: [https://github.com/squidfunk/mkdocs-material-insiders/releases](https://github.com/squidfunk/mkdocs-material-insiders/releases)

#### Install the required extensions
MacOS (required for the social cards extension):
```
brew install cairo libffi
export LDFLAGS="-L/opt/homebrew/opt/libffi/lib"
export CPPFLAGS="-I/opt/homebrew/opt/libffi/include"
export PKG_CONFIG_PATH="/opt/homebrew/opt/libffi/lib/pkgconfig"
```

All:
```
pip install cairosvg
pip install 'mkdocs-material[imaging]'
pip install mkdocs-awesome-pages-plugin
```

## Running Locally
Use the `mkdocs serve` command to build the documentation and run it on a local webserver @ `http://127.0.0.1:8000/`

```
mkdocs serve

INFO    -  Building documentation...
INFO    -  Cleaning site directory
INFO    -  Documentation built in 0.29 seconds
INFO    -  [15:36:39] Watching paths for changes: 'docs', 'mkdocs.yml'
INFO    -  [15:36:39] Serving on http://127.0.0.1:8000/
```

## Deploying
TODO

## Navigation
Navigation is enhanced via the [Mkdocs Awesome Pages Plugin](https://github.com/lukasgeiter/mkdocs-awesome-pages-plugin).

TL;DR:
* Each folder has a `.pages` file that defines the navigation for all documents in that directory.
* Hardcode naviagtion and links in these files.
* Use `...` as a catchall - Mkdocs will render any doc pages NOT explicitly defined in the `.pages` file where you insert this.

## Documentation
See the [documentation for Mkdocs Material](https://squidfunk.github.io/mkdocs-material/getting-started/).

## Images
Use https://pika.style to generate images of screenshots.
* Size should be set to **Open Graph**.
* Watermark should be disabled.
* Frame should be set to **macOS dark**.
* URL should be set to `app.glean.com`.
* Gradient/background should be set to colors similar to the Glean color palatte.
  * All screenshots within the same document should use the same gradient/background.
  * Different document pages should use different gradient/backgrounds.
