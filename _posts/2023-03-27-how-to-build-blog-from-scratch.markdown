---
layout: post
title:  "Your own personal space on the web: How to build a blog from scratch"
date:   2023-03-27 16:52:45 +1100
categories: web_dev
---

<!-- # Your own personal space on the web: How to Build a Blog from scratch -->
Having my own personal space on the web has been a long time goal of mine - one that I found myself procrastinating on each month by doing searching for the "best way to create a blog" and "best platforms for hosting your blog". There is no shortage of options out there to create your own little space on the web to share the digital content on the web. I have tried a few of these, some ranging for super simple like creating an medium account and clicking the "write" button to more complex like spinning a AWS server to self-host your site using WordPress.

More recently, while teaching myself web development on The Odin Project (an amazing resource.. if you're even remotely interested in how the web works, you should check this out), I came across Github pages. I have always thought of Github as a place to store and manage your code. It is that, but boy is it so much more. 💡 In a few clicks, I was able to publish this to the web and share my new 'website' with my wife.

🤯 Mind blown. What if I could build on my new found HTML and CSS skills and build a personal blog hosted on Github? Yes it would be 'more work'.. but I would walk away with a sense of pride and new found sense of freedom that I could set up a blog from "scratch". Down the google rabbit hole I went - this time searching for "How to host a blog on Github?". This journey led me to [Jekyll](https://jekyllrb.com) - a framework to transform plain text into static websites and blogs. The Jekyll framework automates most of the heavy-lifting so you can focus on your content, but also leaves some room for you unleash your inner developer and tweak your site just the way you want.

In this post, I will share the steps to build and launch a blog using Jekyll and GitHUB. I will cover two ways to get your site and up and running:
1. Quick. Doable in 15 mins, with no requirement to download anything to your Mac or PC.
2. Advanced. Up and running in 60 - 90 mins. You will need to install a few things on your Mac or PC. This is similar to the quick setup, but in this guide, we cover how to update and test your new site locally, before it is published. 

## Quick
Github covers the steps to set up a simple site or blog in detail here: https://github.com/skills/github-pages. The guide takes through a series of 5 steps can take you a Github account to creating a site hosted on your own personal URL that can be shared as you please. All of this doable on your browser.

This guide was great and it got me up and going in just about 15 mins. However, I found myself wanting more. Similar to how I was able to update an html file, hit refresh on my browser and have my updates reflected instantaneously, I wanted to be able to do this for my new site. This will allow me to  test and play in a local environment before pushing these changes to Github to be published. 

If this is you, keep reading. We cover this in the next section.

## Advanced
In this section, we will go through:
- building your site locally, using the terminal, an IDE and your browser
- hosting this site on GitHub pages
- connecting your site to a custom domain
- the basics of updating your post (e.g. adding images)

It assumes some prior knowledge (it is the advanced setup after-all). I have listed these below with links to learn more if you aren't familiar with these terms.
- You are familiar with the use of the terminal. Comfortable enough to execute commands. [Command Line Basics](https://www.theodinproject.com/lessons/foundations-command-line-basics)
- You are familiar with the use of an Integrated Development Environment (IDE). [Text Editors](https://www.theodinproject.com/lessons/foundations-text-editors)
- You are familiar with the use of git. [Setting Up Git](https://www.theodinproject.com/lessons/foundations-setting-up-git)

### 1. Setting up your local environment
You will need

#### Git
- [Introduction to Git](https://www.theodinproject.com/lessons/foundations-introduction-to-git)
- [Git Basics](https://www.theodinproject.com/lessons/foundations-git-basics)

#### Homebrew
[Homebrew](https://brew.sh/) is a package manager for macOS designed to simplify the process of installing software on a mac. It is an amazing piece of software taht allows you to install and remove software via the command-line. We won't cover the details here. For now, simply enter the following command in the terminal to install:
``` bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
If you already have homebrew installed, use this command to check that it is up to date:
``` bash
brew --version
Homebrew 4.0.09 # This is the latest version as of  "2023-03-27"
```
If out of date enter:
``` bash
brew update
```

Use this page if you'd like to follow along with more detailed steps: [Homebrew · Mac Install Guide](https://mac.install.guide/ruby/3.html).

#### Ruby
Ruby already comes installed on your mac but you don't want to use this version see [Do not use MacOS system Ruby · Mac Install Guide](https://mac.install.guide/faq/do-not-use-mac-system-ruby/index.html) for why. If you're a casual Ruby users (i.e. you're not sure what Ruby is or you won't be using it for any other purposes) then simply follow the instructions on this page to install ruby with homebrew [Brew Install Ruby · Mac Install Guide](https://mac.install.guide/ruby/13.html).

The last step to **Configure the shell environment** is tricky, make sure to go slow and follow the steps carefully.

#### Jekyll
Jekyll is a application built on Ruby that transforms markdown files into html. More specifically, Jekyll is a package that can be installed and used by developers to add specific functionality to their Ruby applications. These packages or libraries are also known in the world of Ruby as **Ruby Gems**. See [What is a gem? - RubyGems Guides](https://guides.rubygems.org/what-is-a-gem/) for more detail.

To install Jekyll, execute this command:
``` bash
gem install jekyll
```

You are now ready to start building your site!

### 2. Setting up your repo and new Jekyll Project
Okay, lets get going! In this step, we will create a new repository and clone this repo to a local directory.

Creating a new repo
1. Create a new repository by navigating to [Create a New Repository](https://github.com/new).
2. Name your new repository, add a description and add a README file - this will allow you to add a longer description for your project.

![New Repo](/assets/images/new-repo.png)

Cloning the repo to the local directory
There are a number of ways to do this, I prefer using VS Code.
1. In VSCode, use ⌘⇧P to bring up the command pallet. Search for `Git: Clone`.
![Git Clone](/assets/images/git-clone.png)
2. Copy and paste the URL of your newly created GitHub repo into the input box. 
![Git Clone URL](/assets/images/git-clone-url.png)
3. You will then be prompted to the parent directory where you want to clone this repo too. My repos are stored in `~/repos`. Pick your own!
4. When prompted, select **Open** to open the cloned repo directory in VS Code.
![Git Clone Confirmation](/assets/images/git-clone-confirm.png)

You should now see your repository in VS Code.
![Empty Repo](/assets/images/empty-repo.png)

The repo should be empty except for a `README.md` file.

Open up a terminal in VS Code in your project directory. In the menu bar: View ▶️ Terminal. A new terminal panel should open in VS Code. Run this command:
``` bash
jekyll new --skip-bundle . --force
```

This initializes a new Jekyll project by creating a bunch of files required to create your website.
![Template Repo](/assets/images/template-repo.png)

You should know the purpose of some of these files:
`Gemfile` is the configuration file that is used to specify the dependencies for the application.
Because we want to build our host our site on GitHub pages, you need to comment out this line by adding `#` or by using ⌘/ on the keyboard.
⚠️ You might be presented with a later version number.
```bash
# gem "jekyll", "~> 4.3.2"
```
and add this line instead
``` bash
gem "github-pages", "~> 228", group: :jekyll_plugins
```

The `_config.yml` is the Jekyll configuration which determines how your site will look like. Comment out these two lines because, GitHub Pages will automatically set these as part of the build process.
``` bash
# baseurl: ""  
# url: ""
```

Nearly there! You now need to run this command to ensure that all the dependencies for your project are installed and up to date.
``` bash
bundle install
```


#### 3. Building and testing your site locally
Your new Jekyll project structure is setup. Let's see what it looks like! Run the following command in your terminal. 

⚠️ make sure that this command is executed in your project folder. Best way tot do this is to open a new terminal console directly in VS Code.
``` bash
bundle exec jekyll serve
```
This will take a couple of seconds to process. At the end of it you should see the following output in your terminal:
``` bash
Configuration file: /Users/<username>/repos/test-jekyll-site/_config.yml
To use retry middleware with Faraday v2.0+, install `faraday-retry` gem
            Source: /Users/errollee/repos/test-jekyll-site
       Destination: /Users/errollee/repos/test-jekyll-site/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
       Jekyll Feed: Generating feed for posts
                    done in 0.107 seconds.
 Auto-regeneration: enabled for '/Users/<username>/repos/test-jekyll-site'
    Server address: http://127.0.0.1:4000
  Server running... press ctrl-c to stop.
```
Copy and paste the server address in your browser and voila.. you should you have a functioning site. I know what you're thinking.. how do I update all this template text. We'll cover this in part 6.

![Template Site](/assets/images/template-site.png)

You will notice that auto-regeneration is enabled. What this means that each time you save changes to your markdown, Jekyll will automatically update the website. You just need to refresh your browser to view the changes.

🐞 Error Handling
xxx

#### 4. Deploy your site
Now that you have built your site locally, it's time to deploy this to Github. There are a couple of ways to do this. 

You can do this on the command line in the terminal buy running the following commands. See [Git Basics | The Odin Project](https://www.theodinproject.com/lessons/foundations-git-basics) if you need a refresher on how git works.
``` bash
git add
git commit -m '<insert commit message>'
git push origin master
```
OR you can do this in VS Code (this is my preference)
1. Navigate to **Source Control** by clicking the icon on the left navigation bar or using this keyboard shortcut ⌃⇧G
2. You see the files you have updated in the source control menu. Type in a commit message and hit ⌘Enter. When asked to stage all changes and commit them directly, select **Yes**.
![Git Commit](/assets/images/commit.png)
1. Once changes are committed, click **Sync**. 
![Git Sync](/assets/images/sync.png)

After completing the above, all your files in your local directory will be visible on Github. To check:
1. Navigate to: `https://github.com/<github username>/<name of your repo>'
2. You should see the folders in your local directly now reflected on GitHub.
![Push to GitHub](/assets/images/push-to-github.png)

🏴 Notice that the `_site` and `.jekyll-cache` directories are missing. Files in this folder get generated as part of the build.

Now that your code is on GitHub, you can follow similar steps to the quick guide to publish your site your GitHub Pages. While you're on your GitHUB repo page, navigate to: Settings ▶️ Code and Automation ▶️ Pages ▶️ Build and deployment ▶️ Deploy from branch.

![Publish GitHub Page](/assets/images/publish-page.png)

See [Enable GitHub Pages](https://github.com/skills/github-pages#step-1-enable-github-pages)  for more info.

#### 5. Setting up your custom domain



#### 6. Now for the hardest part. Creating content!

