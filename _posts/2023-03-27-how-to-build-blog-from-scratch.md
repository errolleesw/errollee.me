---
layout: post
title:  "Your own personal space on the web: How to build a blog from scratch"
date:   2023-03-27 16:52:45 +1100
tags: how_to web_dev jekyll
---

I have always wanted my own personal space on the web, but I kept putting it off, constantly searching for the "best way to create a blog" or the "best platforms for hosting your blog." There are so many options! I tried everything from simple solutions like posting on Medium to more complex endeavors like setting up an AWS server to self-host a WordPress site.

Recently, while learning web development through [The Odin Project](https://www.theodinproject.com) (an incredible resource), I stumbled upon Github pages. I used to think Github was just for storing and managing code, but it turns out there's so much more to it. 💡💡💡 With just a few clicks, I was able to publish a basic website and excitedly share it with my wife.

🤯🤯🤯 What if I could combine my newfound hacker skills from [TOP](https://www.theodinproject.com) to create a personal blog hosted on Github? Sure, it would involve more work, but the sense of accomplishment and freedom to create a blog from "scratch" would be worth it. 

So, I dived back into the world of Google searches, this time looking up "How to host a blog on Github". I discovered [Jekyll](https://jekyllrb.com/) - a framework that turns plain text into static websites and blogs. With [Jekyll](https://jekyllrb.com/) doing most of the heavy lifting for you, you can focus on your content while also providing room for customization and tweaks to make your site truly unique.

GitHub has a quick guide [here](https://github.com/skills/github-pages) to get something up in about 15 mins without having to download anything to your Mac. Worth doing just to get familiar with the GitHub interface.

In this post, I will cover how to get to same outcome (publishing a site on GitHub Pages), but this time with a local environment that can be used to update and test your site locally, before it is published. We will cover off the following topics:
- building your site locally, using the terminal, an IDE and your browser
- hosting this site on GitHub pages
- connecting your site to a custom domain
- the basics of updating your post (e.g. adding images)

## Assumed knowledge
This guide assumes you have some prior knowledge, nothing to difficult to pick up for a tech savvy individual like yourself. I have listed these below with links to learn more if you aren't familiar with these terms.
- You are familiar with the Terminal - comfortable enough to execute commands. Check out the [Command Line Basics](https://www.theodinproject.com/lessons/foundations-command-line-basics) secion on TOP if you need a refresher
- You are familiar with the use of an Integrated Development Environment (IDE). Check out [Text Editors](https://www.theodinproject.com/lessons/foundations-text-editors) section on TOP if you need a refresher
- You are familiar with the use of Git. Check out [Setting Up Git](https://www.theodinproject.com/lessons/foundations-setting-up-git) if you need a refresher.

## Step 1: Setting up your local environment
Because we want to have a version of our site running on our local environment, we will need to install a few things.

### Git
The Git installation process is well document on multiple sources on the internet. The best ones I have come across by far are these series of articles on TOP. It not only takes you through the setup process, but also the basics of how to use Git.
- [Setting Up Git](https://www.theodinproject.com/lessons/foundations-setting-up-git)
- [Introduction to Git](https://www.theodinproject.com/lessons/foundations-introduction-to-git)
- [Git Basics](https://www.theodinproject.com/lessons/foundations-git-basics)

### Homebrew
[Homebrew](https://brew.sh/) is a package manager for macOS designed to simplify the process of installing software on a mac. It is an amazing piece of software that allows you to install and remove software via the command-line. To install, execute this in your terminal:
``` bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
If you already have [Homebrew](https://brew.sh/) installed, execute this command to check that it is up to date:
``` bash
brew --version
Homebrew 4.0.09 # This is the latest version as of  "2023-03-27"
```
If out of date, execute:
``` bash
brew update
```

If you run into any issues or would just like to follow along with more detailed steps. Check out [Homebrew · Mac Install Guide](https://mac.install.guide/ruby/3.html).

### Ruby
Ruby already comes installed on your mac but you don't want to use this version. see [Do not use MacOS system Ruby](https://mac.install.guide/faq/do-not-use-mac-system-ruby/index.html) for why. If you're a casual Ruby users (i.e. you're not sure what Ruby is or you won't be using it for any other purposes) then  follow the instructions on this page ([Brew Install Ruby](https://mac.install.guide/ruby/13.html)) to install Ruby with homebrew .

⚠️ The last step to **Configure the shell environment** is tricky, make sure to go slow and follow the steps carefully.

### Jekyll
Jekyll is a application built on Ruby that transforms markdown files into HTML. More specifically, Jekyll is a package that can be installed and used by developers to add specific functionality to their Ruby applications. These packages or libraries are also known in the world of Ruby as [
**Ruby Gems**](https://guides.rubygems.org/what-is-a-gem/).

To install Jekyll, execute this command:
``` bash
gem install jekyll
```

🥂 You are now ready to start building your site!

## 2. Setting up your project repository
In this step, we will create a new repository and clone this repo to a local directory.

### Creating a new repo
1. Create a new repository by navigating to [Create a New Repository](https://github.com/new).
2. Name your new repository, add a description and add a README file - this will allow you to add a longer description for your project.

![New Repo](/assets/images/new-repo.png)

### Cloning the repo to the local directory
There are a number of ways to do this, I find using VS Code the easiest.
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

### Initialising a new Jekyll project
Open up a terminal in VS Code in your project directory. In the menu bar: View ▶️ Terminal. A new terminal panel should open in VS Code. Run this command:
``` bash
jekyll new --skip-bundle . --force
```

This initializes a new Jekyll project by creating a bunch of files required to create your website.
![Template Repo](/assets/images/template-repo.png)

There are two files that you should be aware for now:
- `Gemfile` is the configuration file that is used to specify the dependencies for the application. Because we want to build our host our site on GitHub pages, you need to comment out this line by adding `#` or by using ⌘/ on the keyboard.
⚠️ You might be presented with a later version number.
```bash
# gem "jekyll", "~> 4.3.2"
```
and add this line instead
``` bash
gem "github-pages", "~> 228", group: :jekyll_plugins
```
- The `_config.yml` is the Jekyll configuration which determines how your site will look like. Comment out these two lines because, GitHub Pages will automatically set these as part of the build process.
``` bash
# baseurl: ""  
# url: ""
```

Finally, you now need to run this command to ensure that all project dependencies  are installed and up to date.
``` bash
bundle install
```


## 3. Build your site
The foundations of your new site is setup. Let's see what it looks like! Run the following command in your terminal. 
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
Copy and paste the server address in your browser and voila! You should you have a functioning site. 

![Template Site](/assets/images/template-site.png)

You will notice that auto-regeneration is enabled. What this means that each time you save changes to your markdown, Jekyll will automatically update the website. You just need to refresh your browser to view the changes.

## 4. Deploy your site
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

Give the publishing workflow a minute or two to run (if you're interested, click the **Actions** tab to see progress) then **refresh**. You should now notice a new modal at the top of your page saying that your site is live at `https://<user_name>.github.io/<repo name>`.

Click **Visit Site**. See [Enable GitHub Pages](https://github.com/skills/github-pages#step-1-enable-github-pages)  for more info.
![Publish GitHub Pages](/assets/images/publish-github-page.png)

Your site is now live! 🍾 Congratulations on this fantastic achievement! Take a moment to celebrate and give yourself a well-deserved pat on the back. Enjoy a relaxing ☕, and revel in your accomplishment. In the upcoming sections, we'll cover how to update your site's content.

## 6. Creating your first blog post
You've successfully set up your own site! That wasn't too hard, was it? Now it's time to dive into creating some awesome content. With the Jekyll framework, publishing various types of content is super easy. In this section, you'll learn how to publish your first blog post.

Jekyll uses Markdown for writing posts – a user-friendly markup language designed to make it simple to write in plain text. Jekyll then converts this text file into HTML and publishes it on your site. Read [Getting Started](https://www.markdownguide.org/getting-started/) to learn more.

You'll find all your blog posts in the `_posts` folder within your project repository. Look for it now in the VS Code explorer. There, you'll see a sample file named `YYYY-MM-DD-welcome-to-jekyll.markdown`. Open this file in VS Code and compare the text with what you see on your site. Do you start to see how the content in the file corresponds to what's displayed on your site? Feel free to experiment by updating the text and observing how it affects the page.

⚠️ Remember to check that your local server is running and to refersh your browser after you've made your updates. See part 3 for help.

### Creating Posts
To create a post, you will need to add a file to your `_posts` directory in this format: `YYYY-MM-DD-title.markdown`. For example, `2023-03-27-my-first-post.markdown`. 

Each post is split up into two sections:
1. [Front Matter](https://jekyllrb.com/docs/front-matter/) 
2. Content of your post

``` md
<!-- Front Matter --!>
---
layout: post
title: "My First Post"
categories: category_1
date: 2023-03-27
---

<!-- Content of your post --!>
# Welcome

**Hello everybody**, this is my first blog post!
```

All posts must begin with [Front Matter](https://jekyllrb.com/docs/front-matter/). This is used to set the layout and other metadata for your post. There are a few of these that you should be aware of:
- `layout: post` - this sets the layout of your post.
- `title: "My First Post"` - this sets the title of your page and the text that goes into your browser tab.
- `date: 2023-03-27` - this is the date that appears on your post

You can add the content for your post below this section.
 
Give this a go, once a new file is added to the `_posts` folder. Make sure that your local server is up and running then refresh your browser. Once you're happy with these changes you can then follow detail in step 4 to get these changes deployed to GitHub.

### Adding Images
After publishing your first post, you'll probably want to enhacne yoru content with images. To do so, simply store your image assets in a folder `/assets/images` within your project's root directory. This makes it easy to mange your images and also allows you to add sub-folders for other asset types in the future.

Your image can then be referenced in a post using this syntax:
``` md
![example screenshot](/assets/images/screenshot.png)
```

## 6. Updating the default text on your site
You're almost there! Just a few final touches and your site will look pretty amazing. Let's update the default values the `_config.yml` file to give it that personal touch.

### Title, email and description:
- Update `title:` to the name of your site. Don't know what to call it? Use chatGPT to generate a few ideas.
- Set `email:` to your email address.
- Use `description:` to give visitors an idea of what to expect on your site.

### Social media links
Personalise your social media handles by updating the default Jekyll values for these items:
- `twitter_username:`
- `github_username:`
- `linkedin_username:`
- `facebook_username:`

## Conclusion
Congratulations! Give yourself a well-deserved pat on the back – you now have your own personal space on the web to share your content. These are the exact steps I followed to set up this site, and it took me about half a day. I hope this guide helps you achieve your goal even faster.

There's so much more to explore - we are only touching the tip of the iceberg. In future posts, I'll share tips on adding a custom domain and updating your site with more personal branding touches.

In the meantime, dive into content creation and let your imagination run wild! I can't wait to see the amazing things you come up with. Happy creating!