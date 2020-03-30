# Deploying kb.pmem.io to GitHub Pages using Travis-CI



This persistent memory knowledge base uses [Jekyll](https://jekyllrb.com/) with the [Docs](https://themeforest.net/item/docs-responsive-documentation-manual-jekyll-theme/21131076) theme. The site uses [Jekyll collections](https://jekyllrb.com/docs/step-by-step/09-collections/) to keep documents organized within separate directories. Since there are lots of docs per collection, we need to use a paginator. The default Jekyll paginator only supports posts, not collections, so we need to use the [jekyll-paginator-v2](https://github.com/sverrirs/jekyll-paginate-v2) which does support collections. Unfortunately, GitHub pages does not support this plugin, see [this discussion](https://github.com/sverrirs/jekyll-paginate-v2/issues/9). Github pages uses a limited set of plugins, listed [here](https://pages.github.com/versions/). 

To get around this problem, we do not want GitHub Pages to automatically build the site for us. Instead, we need to build the site and deploy it manually, rather, having Travis-CI build and deploy it for us. These instructions are provided to deploy kb.pmem.io from scratch using this approach. It may prove useful to somebody in the future.

## Initial Setup

Using the instructions [How do I configure GitHub to use non-supported Jekyll site plugins?](https://stackoverflow.com/questions/28249255/how-do-i-configure-github-to-use-non-supported-jekyll-site-plugins) from Stackoverflow. 

**Step 1)** [Create a Developer Personal Access Token](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line) within GitHub. For Step 7 of the GitHub instructions, select only the 'repo' option which also includes 'public_repo'. These are the only permissions necessary for Travis-CI.

Note: Please ensure you copy the key when it is generated as it's the last time you'll see it. This key is required for Travis-CI.

**Step 2)** Follow [Travis getting started](https://docs.travis-ci.com/user/getting-started/) guide to enable Travis for your repo. 

View or create `script/cibuild` in the knowledge-base repository with the following content

```
#!/usr/bin/env bash
# halt script on error
set -e

# Build the static site using jekyll
bundle exec jekyll build

# This file tells gh-pages that there is no need to build the site automatically
touch ./_site/.nojekyll
```

Create `.travis.yml` with the following content (modify as required)

```
language: ruby
rvm:
- 2.6

before_script:
 # - gem update --system
 - gem --version
 - chmod +x ./script/cibuild # or do this locally and commit

# Assume bundler is being used, therefore
# the `install` step will run `bundle install` by default.
script: ./script/cibuild

# branch whitelist, only for GitHub Pages
branches:
  only:
  - master

env:
  global:
  - NOKOGIRI_USE_SYSTEM_LIBRARIES=true # speeds up installation of html-proofer

sudo: false # route your build to the container-based infrastructure for a faster build

deploy:
  provider: pages
  skip_cleanup: true
  keep-history: true
  local_dir: _site/  # deploy this directory containing final build
  github_token: $GITHUB_API_KEY # Set in travis-ci.org dashboard
  on:
    branch: master
```

Commit and push the change to the repository.

**Step 3)** In the `.travis.yml` file we specified a secret environment variable `GITHUB_API_KEY`. Go to https://travis-ci.org/dashboard and click on the 'knowledge-base' repository from the 'Active repositories' list. If you do not see this repository, ensure you followed [Travis getting started](https://docs.travis-ci.com/user/getting-started/) and activated the 'knowledge-base' repository within https://travis-ci.org/account/repositories. 

Select 'More Options' -> 'Environment Variables':

Name = GITHUB_API_KEY

Value = <The developer access key you generated in Step 1 from Github>

Branch: master

Click 'Add' to add the variable. You're now ready to begin building the site.

**Step 4)** Verify the [GitHub Pages settings](https://github.com/pmem/knowledge-base/settings) for the repository sets the 'Source' to the 'gh-pages branch' so GitHub Pages serves the rendered static site from the correct branch (defaults to 'master'). 

## Deployment steps (after every push):

1. Make a change to the repository and push to the 'master' branch.
2. Travis will build the site by executing `bundle exec jekyll build` using our script `script/cibuild` and output to the `_site` directory.
3. The `_site` directory will be pushed to `gh-pages` branch that GitHub pages uses to serve the website.
4. GitHub pages will serve the site as it is without building it again (because of the `.nojekyll` file). This process make take up to 15mins to complete before the website reflects the updates.