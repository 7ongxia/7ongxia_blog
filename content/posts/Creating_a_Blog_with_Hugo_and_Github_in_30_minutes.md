---
title: "Creating a Blog with Hugo and Github in 30 minutes"
date: 2021-06-30T18:02:00+08:00
draft: false
toc: true
images: 
tags:
  - hugo
  - github
---


You can start your own blog by using Hugo and Github in 30 minutes. 
Hugo is one of the world’s fastest framework for building websites.
This quick start uses macOS in the examples. 
Let's start!

**Steps**

1. Install `Hugo`
1. Create a site and add a theme
1. Add Some Content
1. Test your site locally
1. Create two Github repositories
1. Modify the `config.toml` file
1. Build your site
1. Deploy your site with `GitHub Pages`
1. Deployment Automation!


## 1. Install Hugo

> `Homebrew` and `MacPorts`, package managers for `macOS`, can be installed from [brew.sh](https://brew.sh/) or [macports.org](https://www.macports.org/) respectively. See [install](https://gohugo.io/getting-started/installing) if you are running Windows etc.

```
brew install hugo
# or
port install hugo

# To verify your new install
hugo version
```


## 2. Create a New Site and add a theme

The below will create a new Hugo site in a folder named "quickstart".

```
hugo new site quickstart
```


See [themes.gohugo.io](https://themes.gohugo.io/) for a list of themes to consider. This quickstart uses the cool [hello-friend-ng](https://themes.gohugo.io/hugo-theme-hello-friend-ng) theme.

First, download the theme from GitHub and add it to your site’s themes directory:

```
cd quickstart
git init
git submodule add https://github.com/rhazdon/hugo-theme-hello-friend-ng.git themes/hello-friend-ng
```

Then, add the theme to the site configuration, `config.toml`:

```
echo theme = \"hello-friend-ng\" >> config.toml
```


## 3. Add Some Content

You can use the `new` command to do a few things for you (like add title and date):
This command will create content files in `content` directory and provide metadata in them.

```
# run the command in the root directory of your site
hugo new posts/my-first-post.md
```

Edit the newly created content file, `my-first-post.md`, if you want, it will start with something like this:

```
---
title: "My First Post"
date: 2021-06-30T08:47:11+01:00
draft: true
---
```

> Drafts do not get deployed; once you finish a post, update the header of the post to say draft: false. More info [here](https://gohugo.io/getting-started/usage/#draft-future-and-expired-content).


## 4. Test your site locally

Now, start the Hugo server:

```
# with drafts enabled:
hugo server -D
# with drafts disabled:
hugo server
```

Navigate to your new site at <http://localhost:1313>.

Feel free to edit or add new content and simply refresh in browser to see changes quickly (You might need to force refresh in webbrowser, something like Ctrl-R usually works).


## 5. Create two Github repositories

Go to GitHub and create two new repository.

- Create a first Github repository: "{yourGithubID}.github.io"
- Create a second Github repository: "{yourGithubID}_blog"

The first repository will directly host your site with `GitHub Pages`.
The second repository is going to host your source code so every time you want to add a new post, you will push the changes into this repository.


## 6. Modify the config.toml file

Once the repository is created, you HAVE to modify the `config.toml` found on the root directory of your site. You need to modify the `baseUrl` property to point to your `GitHub Pages`.

```
baseURL      = "https://{yourGithubID}.github.io/"
title        = "Jong Kim"
languageCode = "en-us"
theme        = "hello-friend-ng"
paginate     = 10
```


## 7. Build your site

To build your site:

```
hugo
```

The output from the build will be put into `./public/` directory. The `public` directory is what you are going to publish into GitHub.


## 8. Deploy your site with GitHub Pages

It’s time to upload the contents of the `./public` directory into the GitHub repository.

```
cd quickstart/public
git init
git remote add origin https://github.com/{yourGithubID}/{yourGithubID}.github.io.git
git add .
git commit -m "Initial commit"
git push --set-upstream origin main
```

After pushing the code into GitHub, you still need to modify the Repository settings.
Change the setting to "main branch" found in: 

- `Settings > Options > GitHub pages > Source -> main branch`

Just wait a couple of minutes for the page to refresh and browse to: 
<https://{yourGithubID}.github.io>. You will see your website is running properly.


## 9. Deployment Automation!

The site is up and running and everything works great! 
But be aware that right now the source code is only on your local machine.

So your final step is going to be:

- After you push the changes to `{yourGithubID}_blog` repository, `Github Action` will grab the content from `{yourGithubID}_blog` and publish the output into your `{yourGithubID}.github.io` repository.


First of all, create a `.gitignore` file and ignore `./public` folder.

```
echo "public/" >> .gitignore
```

After that, push your source code into the `{yourGithubID}_blog` repository.

```
cd quickstart
echo "public/" >> .gitignore
git init
git remote add origin https://github.com/{yourGithubID}/{yourGithubID}_blog.git
git add .
git commit -m "Add site contents"
git push --set-upstream origin main
```

The last step is setting `GitHub Action`.
`GitHub Action` is going to grab the content from `{yourGithubID}_blog` repository, build and push the output into `{yourGithubID}.github.io` repository.

```
name: hugo CI

on:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true 
          fetch-depth: 1   

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'

      - name: Build
        run: hugo

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          personal_token: ${{ secrets.PERSONAL_TOKEN }}
          external_repository: {yourGithubID}/{yourGithubID}.github.io
          publish_branch: main
          publish_dir: ./public
```

---

**Congratulations!**

Now you can write some posts locally and simply publish your contents in a minute. `Github Action` will automatically deploy your site when you push to your repository.

Thank you for reading!


## Useful websites

[Markdown Guide](https://www.markdownguide.org/basic-syntax#links)

[Shortcodes](https://gohugo.io/content-management/shortcodes/)