# Unshittify.org

Unshittify is a project by father-daughter team Jude and Tatiana Anthony, a 30-year software developer and an 8-year mechanical engineer, respectively.  We are documenting our attempts to combat enshittification in our lives, and sharing our recommendations for how you can do the same, at nearly any skill level or budget.

## Overview

This repo has the entire contents of the live [Unshittify Website](https://www.unshittify.org).  This will be of little use to anyone other than Jude and Tatiana, but you are welcome to explore it.

This README is primarily to assist Jude and Tatiana in managing the website.  It also includes documentation of our themes and some data sources.

## Potentially Interesting Information

### Website Theme

Unshittify.org is a static site built with [Jekyll](https://jekyllrb.com/).  We are using the [Minimal Mistakes theme](https://github.com/mmistakes/minimal-mistakes).

We have kept the Minimal Mistakes example posts and documentation posts in our repo, but only serve them when we run the site locally.

## Maintenance Documentation

### Private Drafts on a Public Repo

This public repo contains our blog posts.  We push the commits here, then Cloudflare Pages notices a change, and [automatically rebuilds our site and deploys it](https://developers.cloudflare.com/pages/framework-guides/deploy-a-jekyll-site/).

However, this is a public repo, which means anyone can see our posts here.  So we are using a private repo to draft and discuss posts, before pushing to this public repo.  [This post on Stackoverflow](https://stackoverflow.com/a/30352360) by Martin Konicek was very helpful in setting it up.  Here's our process for using this:

<details markdown="1">
    <summary><h4>How to Use a Private Repo for Drafts of a Public Repo</h4></summary>
<a href="https://stackoverflow.com/a/30352360" target="_blank">"This comment"</a> by <a href="https://stackoverflow.com/users/90998/martin-konicek" target="_blank">Martin Konicek</a> is licensed under <a href="http://creativecommons.org/licenses/by-sa/4.0" target="_blank">CC BY-SA 4.0</a>  Portions of the licensed comment have been used in this section.

#### Setup
1. Create a new private repo, a bare clone of the public repo.
``` 
git clone --bare https://github.com/exampleuser/public-repo.git
cd public-repo.git
git push --mirror https://github.com/yourname/private-repo.git
cd ..
rm -rf public-repo.git
```

2. Clone the private repo so you can work on it.
```git clone https://github.com/yourname/private-repo.git
cd private-repo
make some changes
git commit
git push origin master
```

3. Add Public Remote to the Private Repo.
```
cd private-repo
git remote add public https://github.com/exampleuser/public-repo.git
git pull public master # Pulls everything from the public repo, creates merge commit
git push origin master # Pushes everything to the private remote origin
```

4. We're not using a pull requests, so we don't need the private pull request repo.  Instead, we're adding the overall private remote to the public repo.
```
git remote add private_repo_yourname https://github.com/yourname/private-repo.git
git pull private_repo_yourname master
git push origin master
```

#### Live Usage

1. Check that the private repo has the public remote
    ```
    git remote
    ```
2. Pull from the public remote. 
    ```
    git pull public master
    ```
3. Push new changes from public repo to private remote origin. 
    ```
    git push origin master
    ```
4. Switch to the public repo
5. Check that the public repo has the private remote
7. Pull changes from the private repo 
   ```
   git pull private_repo_yourname master
    ```
8.  Push changes to public remote `git push origin master

#### Pull Requests

So you want to use a pull request.

1. Complete steps 1-5 from the Live Usage section.
2. Create a new branch on the public repo 
   ```
   git checkout -b pull-request-yourname
   ```
3. Check that you're on the correct branch 
   ```
   git status
   ```
4. Pull changes from the private repo's master branch to the new local branch 
   ```
   git pull private_repo_yourname master
   ```
5. Push the changes to the public remote, in the new branch 
   ```
   git push origin pull_request_yourname
   ```
6. Use your favorite method to create a pull request.

#### Squashing [WIP]

If one of the old commits from the private repo has something you do NOT want showing up in the public repo, you should squash the commit before pushing to remote.

TBD how to do this.

---

</details>



### Local Config

To host the site locally while you work, run `bundle exec jekyll serve --config _config.yml,_config_dev.yml -H {LOCAL_IP}`

Some important notes:

1. `{LOCAL_IP}` should be replaced with your local IP address - e.g. 10.0.0.145
2. There must **not** be a space after the comma.  Without the space, Jekyll will use the configurations in `_config.yml`, but override any that are duplicated in `_config_dev.yml` with the values it finds there.<br>
  **With** the space, Jekyll will completely ignore the `_config_dev.yml` file, like you didn't even bother including it.
3. The config files are YAML files. When both files have the same top level variables, Jekyll will override the value defined in the first config file with the value in the second config file. This means that for variables that are actually lists, there is no way to tell it to _add_ the elements that are in `_config_dev.yml` to the elements in `_config.yml`.<br>
    Therefore, some sections, like the frontmatter defaults and the collection settings, unfortunately must fully included in both `_config.yml` and `_config_dev.yml`.  Ensure that you update these sections in both files when you change them.  They have marked in the config files.

#### Aliases

I use the PowerShell Alias `localjekyll` for the above command.

I created it following the instructions from [Ben Carp's Stack Overflow Comment](https://stackoverflow.com/a/50309277). I did not need to turn on developer mode, or reboot my computer to activate the scripts, because the checkbox was already selected. 

I did make sure to refresh my PowerShell session with `. $profile` before attempting to use the alias, though.

If you want the same alias that I do, my `Microsoft.PowerShell_profile.ps1` file looks as follows:

```ps1
function serveJekyllLocally {bundle exec jekyll serve --config _config.yml,_config_dev.yml -H $$$LOCAL_IP$$$}
New-Alias localjekyll serveJekyllLocally
```

Again, replace `$$$LOCAL_IP$$$}` with your local IP address.

## TODO:

- [x] Remove sample posts from home page
- [ ] Add home page "newest posts" section
- [ ] Add [Definition Tooltips](https://erikw.me/blog/tech/open-sourcing-my-second-jekyll-plugin-glossary-tooltip) to blog
- [ ] Add bounding box CSS for accordions
- [ ] More TBD