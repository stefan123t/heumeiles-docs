# heumeiles-docs

Documentation for the AhoyDTU and OpenDTU Projects

Go to https://stefan123t.github.io/heumeiles-docs to use it.

This repo contains the documentation for the AhoyDTU and OpenDTU Projects.

This repo is used to build the documentation for Ahoy-DTU and OpenDTU in a concise mkdocs format.

As most of the documentation for all MI-, HM- and HMS/HMT-series inverters are using the same protocol Gen3 / Gen2 DevInfo / DevCommand's the protocol and knowledge has a lot of overlap.

The HMS-WiFi-series instead use the NetworkCommand .protobuf commands which are described and documented in a separate chapter.

## How does it work

  1. You can edit any `*.md` document in the [docs](docs) folder.
  2. Then create a Pull Request for it to merge it into the `main` branch (or edit it directly in the `main` branch if you have the required rights).
  3. When it got merged, the [Github Actions](actions) will re-generate the documentation and place it in the `gh-pages` branch. This branch automatically gets populated to the public [Documentation Site](heumeiles-docs)

### Editing a page

Each page has a link on its top-right corner `Edit on GitHub` which brings you directly to the Github editor.

### Adding new pages

  1.  Add a new `*.md` document in the [docs](docs) folder.
  2.  Add the **filename** to the [docs/nav.yml](docs/nav.yml) at the wished position in the **Links** section.

<!--
### Parameter Documentation

Each parameter which is listed in the [configfile]() in the main project repo has its own description page in the folder `param-docs/parameter-pages` (grouped by the config sections). Those pages can be edited as needed.

The script `concat-parameter-pages.py` in `param-docs` should be run whenever one of the pages changed. It then concatenates all pages into the single `../docs/Parameters.md` which gets be added to the `mkdocs` documentation.

#### Template Generator

The script `generate-template-param-doc-pages.py` should be run whenever a new parameter gets added to the config file. It then checks if there is already page for each of the parameters.

  * If no page exists yet, a templated page gets generated.
  * Existing pages do not get modified.

If the parameter is listed in `expert-params.txt`, an **Expert warning** will be shown.

If the parameter is listed in `hidden-in-ui.txt`, a **Note** will be shown.
-->

### Formating

#### Boxes

Boxes can be shown using the **admonition** extension.

```
!!! Note
    I am a note
```

Make sure to have 4-whitespace Intents! Possible types: `attention, caution, danger, error, hint, important, note, tip, and warning` See https://python-markdown.github.io/extensions/admonition/

### Local Test

To test it locally:

  1. Clone this repo

  2. Install the required tools (See also [.github/workflows/build-docs.yaml](.github/workflows/build-docs.yaml)):

    ```
    pip install --upgrade pip
    pip install mkdocs mkdocs-gen-files mkdocs-awesome-pages-plugin mkdocs-material pymdown-extensions
    ```

  3. In the main folder of the repo, call `mkdocs serve` (and keep it running). This will locally generate the documentation. You can access it under [http://127.0.0.1:8000/heumeiles-docs/](http://127.0.0.1:8000/heumeiles-docs/)

Any change to the files will automatically be applied.
