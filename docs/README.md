# MkDocs Material theme for sdmx-core documentation

## Directory layout
```
sdmx-core/
    pom.xml
    fusion-api/
    fusion-api-dao/
    fusion-api-sdmx/
    ...
    docs/
        mkdocs.yml    # The mkdocs configuration file.
        docs/
            index.md  # Documentation homepage.
            page1.md  # Top-level page
            page2.md  # Top-level page
            topic-a/   
                page3.md    # Second-tier page
                page4.md    # Second-tier page
            topic-b/
            topic-c/
            ...
```

## Authoring
Add and edit Markdown files under the `sdmx-code/docs/docs/` directory. Add sub-directories as needed to create the documentation hierarchy which will be reflected in the site's TOC.

Images as png, jpg, svg etc files can also be included anywhere in the `docs/` directory. It's a good idea to hold the image in the same directory as the Markdown which references it thus allowing a simple relative reference:
```
![Image title](theimage.png){ align=left }
```

From the directory containing `mkdocs.yml` use the `mkdocs serve` to preview the documentation. This runs a local web server publishing the site on `http://localhost:8000`.

## Versioning using `mike`
`mike` is a Python tool that allows different versions of the documentation to be maintained. Moreover, it adds a version dropdown to the documentation site's header bar allowing users to choose the version to consult. Note that this versioning operates separately from the GitHub tags and releases so care is required to keep the documentation's version numbers aligned with those of the actual software.

`mike` takes care of building the actual static website for deployment on GitHub pages and implements the versioning by adding subpaths to the base site URL. For instance:
```
https://sdmx-core.sdmx.io/1.2.2
https://sdmx-core.sdmx.io/2.3.7
```
The process for authoring and publishing documentation for a new sdmx-core release is set out below: 
### 1. Author
Add and edit Markdown and images as described above.

Use `mkdocs serve` to preview the results, however this will only show the current iteration of the documentation and not the other versions. For this use `mike serve`.

### 2. PR and merge to develop
Just follow the normal development lifecycle to merge the code and documentation changes into `develop`.

### 3. Publish
On creation of a GitHub release, a GitHub action triggers which generates the static content for the documentation in `master` and pushed it to the `gh-pages` branch using the release tag by executing:
```
mike deploy [RELEASE_TAG] latest
```
GitHub pages is configured to deploy from 

