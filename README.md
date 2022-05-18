# EnID Documentation

- Static Site Generator: MkDocs
    - https://www.mkdocs.org
- Material Design Theme for MkDocs
    - https://squidfunk.github.io/mkdocs-material/

## Access Documentation

- Rendered MkDocs HTML output on Github Pages:
    - https://developerzone.netid.dev

## Project Structure

- Github Repo: https://github.com/eunid/netID-docs/
- master branch:
    - docs folder
    - *.md documentation pages (markdown)
        - Folder '/stylesheets/' (override theme preset)
        - Folder '/images/' (image files)
        - Folder '/diagrams/src' -> PlantUML source files
        - Folder '/diagrams/out' -> PlantUML SVG output
    - custom theme folder
        - main.html (override standard footer)
    - .gitignore
        - /site Folder
        - **/.DS_Store
        - .vscode/settings.json
    - docs/CNAME file for custom domain settings
- gh-pages branch
    - deployment 

## Build documentation locally (single version)

1. Install necessary packages

``` shell
pip install -r requirements.txt
```

2. Build 

``` shell
mkdocs build
```

3. Serve locally

``` shell
mkdocs serve
```

## Deployment

Documentation is deployed via the gh-pages (see above) branch to a custom domains.
Deployment is done as described in the mkdocs documentation https://www.mkdocs.org/user-guide/deploying-your-docs/#deploying-your-docs

Folder structure:
```
netID-docs/
    mkdocs.yml
    docs/
```

### Production deployment / Versioning

Live Documentation is deployed using version managment based on [mike](https://github.com/jimporter/mike). Local builds can still be deployed as described above. Mike creates self-contained deployed documentation versions on the gh-pages branch, once a version is build it can stay deployed unrelated to further changes and updates of dependencies.

### Setup a clean versioned deployment (remote)

1. Clean up gh-pages branch

``` shell
mike delete --push --all
```

2. Create CNAME on gh-pages Branch

Create CNAME file in the gh-pages branch root with content developerzone.netid.dev

3. Add fonts (root dir of gh-pages branch)
	
Create fonts folder and add the necessary locally hosted fonts

4. Create intial version

``` shell
mike deploy --push --update-aliases --no-redirect [VERSION] latest
```

5. Set default version

``` shell
mike set-default --push latest
```
### Deploy a new version

1. Create a release tag with version name and push to origing

``` shell
git tag -a [VERSION]
git push origin [VERSION]
```

2. Deploy new version and set as new latest

``` shell
mike deploy --push --update-aliases --no-redirect [VERSION] latest
```

### Update existing version (minor patches)

Existing versions can simply be overwritten by-redeploying with the same version number. Make sure to update latest (i.e include latest alias when re-deploying) in case this version is the most current one (as we are not using re-direct for latest).

## Content Creation

Write new docs with Markdown: https://www.mkdocs.org/user-guide/writing-your-docs/

### PlantUML -> Diagrams

- Install Java `brew cask install adoptopenjdk`
- Install "PlantUML" -> `brew install plantuml`
- Install MkDocs PlantUML Plugin: `pip3 install mkdocs-build-plantuml-plugin` (https://github.com/christo-ph/mkdocs_build_plantuml)
- Generate PlantUML Source Files in `/docs/diagrams/src/filename.puml`
- When starting with `mkdocs serve`, it will create all diagrams initially.
- Integrate Output File in ".md" -> `![file](diagrams/out/filename.svg)`
- Styling: https://plantuml.com/de/skinparam

### Mermaid -> Diagrams (currently not implemented)

The trick is:

- To include MermaidJS assets in your bundle
- to use Pymdown's Superfences extension to make mkdocs build "mermaid" code sections into div with the "mermaid" class.

This section is the relevant section of the doc: https://facelessuser.github.io/pymdown-extensions/extensions/superfences/#custom-fences

Mermaid Syntax: https://mermaid-js.github.io/mermaid/#/

``` shell
markdown_extensions:
  - pymdownx.superfences:
      custom_fences:
        - name: mermaid
          class: mermaid
          format: !!python/name:pymdownx.superfences.fence_div_format

extra_javascript:
  - https://unpkg.com/mermaid@8.4.6/dist/mermaid.min.js
```
