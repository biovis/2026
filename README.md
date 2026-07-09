# BioVis 2026 Website

The 2026 version of the BioVis website.

It uses [Jekyll](http://jekyllrb.com/) as CMS and it is a copy of the 2021
version of the website.

This is automatically built by [GitHub Pages](https://pages.github.com/) and is
published on http://biovis.net/ under a directory that matches the repository
name, e.g., 2026.

## Creating a next year version

1. create a new repository (e.g., 2027) at [https://github.com/biovis/](https://github.com/biovis/)

    - note that the repository should be public and the main branch must be named `gh-pages`
    - you can _fork_ the current year repository and rename it

2. update the \_config.yml file

3. update the remaining content of the webpage as you see fit

4. push the changes into the new repository (created in step 1)

5. update forwarding in the index.html file at [https://github.com/biovis/biovis.github.io/](https://github.com/biovis/biovis.github.io/)

## Random stuff

Navigation menu is configured in `_data/navigation.yaml`.

