# [https://shagn.github.io/](https://shagn.github.io/)

Code for my personal website

## Development

1. Install dependencies
    - Hugo: `brew install hugo` (on MacOS)
    
    - Add theme as submodule: `git submodule add https://github.com/luizdepra/hugo-coder.git themes/hugo-coder` (from repo root)

2. Build the site with `hugo server`

## Updating template 

Go into the subdirectory and pull the newest changes from `master` and commit the changes. 

```
cd themes/hugo-coder
git pull
```

## Deployment

Pushes to the `master` branch are automatically deployed to GitHub Pages.
