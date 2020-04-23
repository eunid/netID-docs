# EnID Documentation Proof of Concept

- Static Site Generator: MkDocs
    - https://www.mkdocs.org
- Material Design Theme for MkDocs (V5 RC3)
    - https://squidfunk.github.io/mkdocs-material/

## Access Documentation

- Rendered MkDocs HTML output on Github Pages:
    - https://developerzone.netid.dev

## Project Structure

- Github Repo: https://github.com/eunid/netID-docs/
- Deployment Repo: https://github.com/eunid/eunid.github.io
- Master Branch:
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
    - CNAME file for custom domain settings

## Deployment

Documentation is deployed at EnID organisation site with a custom domain (see above).
Deployment is done as described in the mkdocs documentation https://www.mkdocs.org/user-guide/deploying-your-docs/#organization-and-user-pages

Folder structure:
```
netID-docs/
    mkdocs.yml
    docs/
eunid.github.io/
```
Push documentation from eunid master repo
```
eunid.github.io# mkdocs gh-deploy --config-file ../netID-docs/mkdocs.yml --remote-branch master
```


## Content Creation

- Write new docs with Markdown: https://www.mkdocs.org/user-guide/writing-your-docs/
- Convert existing Word Document -> Markdown with pandoc:
    - command line: 'pandoc -f docx -t markdown foo.docx -o foo.markdown'
    - to save the images, add the option --extract-media=./ to the command above. It will create a folder 'media' with all the images and they will be correctly shown in the markdown file.
    - Make sure that the result of the automatic conversion is proper. 

## PlantUML -> Diagrams

- Install Java `brew cask install adoptopenjdk`
- Install "PlantUML" -> `brew install plantuml`
- Install MkDocs PlantUML Plugin: `pip3 install mkdocs-build-plantuml-plugin` (https://github.com/christo-ph/mkdocs_build_plantuml)
- Generate PlantUML Source Files in `/docs/diagrams/src/filename.puml`
- When starting with `mkdocs serve`, it will create all diagrams initially.
- Integrate Output File in ".md" -> `![file](diagrams/out/filename.svg)`
- Styling: https://plantuml.com/de/skinparam

## Mermaid -> Diagrams (currently not implemented)

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
