# auto-p2docking docs

This project contains the auto-p2docking manual.

## Building the docs

Before building the documentation, check the `source/conf.py` file to make sure that the auto-p2docking version is right.

### Building the docs with the sphinx Docker image

You only need `docker` installed to generate the documentation. Then, placed in this directory, run `make html`. Documentation will be generated in `./build/html` directory.

In order to generate de whole PDF, run `make latexpdf`. You will need the `latexmk` package. Documentation will be generated in `./build/latex`. 

In case of having problems of missing dependencies of latex packages, try installing these packages: `texlive-fonts-recommended`, `texlive-latex-recommended`, and `texlive-latex-extra`.

## Writing the documentation

The documentation source files are located at the `./source` directory.

Documentation is written using [reStructuredText](http://docutils.sourceforge.net/rst.html). In the following links you can find information about the syntax:
- http://docutils.sourceforge.net/docs/user/rst/quickref.html
- http://docutils.sourceforge.net/docs/ref/rst/restructuredtext.html

### Editing with Visual Studio Code and Live Preview

You can use two extensions to edit and see live previews, **but not both**:

- [Esbonio extension](https://marketplace.visualstudio.com/items?itemName=swyddfa.esbonio), to manage the [Esbonio server](https://pypi.org/project/esbonio/), who is able to build and serve sphinx projects. The `.vscode/settings.json` is configured to make Esbonio build its results into `_build`, avoiding conflicts with the `build` folder, which is generated during `make html`.

- [RestructuredText extension](https://marketplace.visualstudio.com/items?itemName=lextudio.restructuredtext), which also integrates with the Esbonio server, as the previous. Read the [prerequisites](https://docs.restructuredtext.net/articles/prerequisites) as you may need to install `esbonio` as well.

None of both are perfect by now. The Esbonio extension generates a working preview (links work, but there is no vertical scroll sync), but lacks some functionalities when editing that the RestructuredText extension provides. However, we detect bugs in the latter, such as links not working properly in live preview.

Moreover, from our experience, you will need Python 3.8 or greater in order the *Live preview* to work without errors.
