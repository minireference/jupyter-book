# Use the Build command line interface

When you've written your book's content, it is now time to build outputs for your book so that you may share them with others.
For example, you may wish to build HTML files to host as a static website, or a PDF to share with colleagues.

## Build via the command-line

The basic way to build your book is via the following command:

```bash
jupyter-book build <path-to-book>
```

In addition, you may control the kinds of outputs that are generated, and the ways in which your book conducts the build.
The rest of the sections on this page cover some of these options.

## Types of build outputs

You can build a variety of outputs using Jupyter Book. To choose a different builder, use the `--builder <builder-name>` configuration when running `jupyter-book build` from the command-line.

Here is a list of builders that are available to you:

- `html`: HTML outputs (default)
- `singlehtml`: A single HTML page for your book
- `dirhtml`: HTML outputs with `<filename>/index.html` structure.
- `pdfhtml`: Build a PDF via HTML outputs (see [](pdf:html))
- `linkcheck`: Run the Sphinx link checker (see [](html:link-check))
- `latex`: Build Latex files for your book
- `pdflatex`: Build a PDF of your book via Latex (see [](pdf:latex))


## Exclude some pages from your book's build

By default, Jupyter Book will build all content files that are found in your book's
folder, even if they are not specified in `_toc.yml` (and will raise a warning if
it finds a file that isn't listed there).

If you'd like Jupyter Book to skip a file entirely, you can do so with the following
configuration in `_config.yml`:

```yaml
exclude_patterns: [pattern1/*, path/to/myfile.ipynb]
```

Any files that match the patterns described there will be excluded from the build.
If you'd like to exclude files from being *executed* but still wish for them to be
built by Jupyter Book, see [](execute/exclude).


(clean-build)=
## Clean your book's generated files

It is possible to "clean up" the files that you generate when you build
your book. This is often useful if you have recently changed a lot of content
in order to ensure that you build your book from a clean slate.

You can clean up your book's generated content by running the following command:

```bash
jupyter-book clean mybookname/
```

By default, this will delete all folders inside `mybookname/_build` *except*
for a folder called `.jupyter_cache`. This ensures that the *content* of your book
will be regenerated, while the cache that is generated by *running your book's code*
will not be deleted (because regenerating it may take some time).

To delete the `.jupyter_cache` folder as well, add the `--all` flag like so:

```bash
jupyter-book clean mybookname/ --all
```

This will entirely remove the folders in the `_build/` directory.

(config:exclude-non-toc-files)=
## Disable building files that aren't specified in the TOC

By default, Jupyter Book will build all files that are in your book's folder, regardless of whether they are specified in the Table of Contents.
To disable this behavior and *only* build files that are specified in the TOC, use the following pattern in `_config.yml`:

```yaml
only_build_toc_files: true
```

Note that files that are in *hidden folders* (e.g. in `.github` or `.venv`) will still be built even if they are not specified in the TOC. You should exclude these files explicitly.

## Debug your book's build process

When debugging your book build, the following options can be helpful:

```bash
jupyter-book build -W -n --keep-going mybookname/
```

This will check for missing references (`-n`), turning them into errors (`-W`),
but will still attempt to run the full build (`--keep-going`),
so that you can see all errors in one run.

You can also use `-v` or `-vvv` to increase verbosity.
