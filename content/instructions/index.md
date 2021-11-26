---
draft: false
title: "Create your own blog: instructions"
date: 2021-11-01T15:16:58+01:00

---
# create a GitHub repository

Name it `<yourgithubusername>`.github.io

Make it a public repository. Do not add a README or Gitignore or whatever: an empty repository is fine.

Mine is [https://github.com/matchalunatic/matchalunatic.github.io](https://github.com/matchalunatic/matchalunatic.github.io), check it out!

# create a local repository and set your GitHub repository as remote

In the terminal, that's a matter of running

```bash
git init <YourRepositoryName>
cd <YourRepositoryName>
git remote add origin git@github.com:`YourUsername>/<YourRepositoryName>.git
```

Then you can add this repository to your IDE if you use one (I will use VS Code here).

If you are not into CLI it's okay too. With VS Code, there are a few more steps
but overall it's simple:
- open the command palette (Ctrl+shift+P on Windows and Linux, Command+shift+P on a Mac)
- search for the Clone repository action (type "Clone" and it will find it) and run it
- when asked for it, paste the `git@github.com:...` URL provided
- select "Clone from GitHub"
- allow the GitHub extension to access your GitHub account, it's safe
- then pick the location where you want your GitHub repository to be cloned
- and add it to your workspace!

# Bootstrapping Hugo

This uses the terminal, so please open your favorite terminal and switch to the newly created repository folder.

Tip: if you use VS Code, you just have to right-click the folder and click "Open in integrated terminal".

Then run the following command:

```bash
hugo new site . --force
```

This will create a Hugo site in your Git repository. We are almost there, as we need to pick a theme. I propose we use the Diary theme

This is done with the following command:

```bash
git submodule add https://github.com/AmazingRise/hugo-theme-diary.git themes/diary
```

This clones the Diary theme of Hugo to the `themes/diary` folder in your local project.

Then we just need to edit the config.toml file to tell Hugo we want to use that theme: just add a
line containing the following to that file:

```toml
theme = 'diary'
```

While we are at it we will also edit the infos about our blog. In the end the toml file will resemble that:

```toml
baseURL = 'https://<YourGitHubUsername>.github.io/'
languageCode = 'en-uk'
title = "MatchaLunatic's women and queer folks poetry blog"

theme = 'diary'
```

It will be very generic for the moment but we can already see it working by running

```bash
hugo server -D
```

and clicking the provided link. This is only a local server but you now got something ready to create content. Let's publish the source for that already

# Publishing the source code: a first step

We will commit the code. This is basically publishing the changeset we made to it online, in a distinct object with an author (you), a date, a message, and contents.

Using the terminal, this is done like this:

```bash
git add .
git commit -m "My first commit in this blog"
```

Using VS Code, you need to enter the "Source Control" panel in the toolbar.

{{<figure title="such an icon" src="scicon.png" alt="a branch icon, with three dots and connecting lines forming a Y">}}

then right click on "Changes", select "Stage all Changes", then enter a Message on top of the "Staged changes" section and validate with Ctrl+Enter

Now we have created a change and committed it to the repository. We can send it to GitHub and the source code will then be published.

Using the terminal, it's done this way:

```bash
git push -u origin main
```

Using VS Code, you can click on the '...' icon next to the repository name and click on "Push".

If you refresh the page on GitHub, you will now see your source code! And so can everyone!

# Publishing the website now

We now enter the world of DevOps. Without DevOps tools, in order to publish a Hugo website to GitHub pages you would need to do the following actions:

- run the `hugo` command to generate the `public` folder on your laptop
- create a Git branch `gh-pages` in your repository (using `git checkout -b gh-pages` for example)
- empty that branch and add only the `public` folder to it
- push that branch to the remote `gh-pages` branch on GitHub
- (first-time only) enable GitHub Pages in the repository settings on GitHub

We will make use of an automation tool, called a GitHub Action, that will do just that automatically each time we push our changes to the main branch of our repository.

The action is available from https://github.com/peaceiris/actions-hugo, and you can copy mine from here: https://github.com/matchalunatic/matchalunatic.github.io/blob/main/.github/workflows/gh-pages.yml (click the "Copy Raw contents" button which is 2 stacked squares). You can just copy it as-is.

Commit and push your changes like before, and the GitHub action will trigger. You can check it out directly from GitHub by clicking the Actions button on the menu bar of your repository.

Since this is our first time publishing the website, we need to run an extra step just this once:
- Go to your repository's Settings tab on GitHub
- Click the Pages tab on the left menu
- Pick the Source for GitHub Pages as branch gh-pages and click Save.
- That's it! Your website will appear online after a few seconds on `https://<YourUsername>.github.io`

# Let's add Contents!

First let's create an about-me page.

Open the terminal and run the following command

```bash
hugo new about-me/index.md
>> Content "/home/matcha/personal/blog/b2021/content/about-me/index.md" created
```

Open the file whose path is given by the command and edit it a little so it looks like this:

```markdown
---
title: "About Me"
date: 2021-11-26T17:32:08+01:00
draft: false
---

# About me

Hey, my name is Matcha and I am participating in a workshop!

Happy to be here!
```

You can then check how it looks like locally by running

```bash
hugo server -D
```

and opening the link given by the command in your browser.

When you're happy with the result, commit, push and see the results online: that's DevOps magic.

# Add more contents

Pick one file from [https://github.com/matchalunatic/queer-and-womens-poems](https://github.com/matchalunatic/queer-and-womens-poems). Download the file and add it to your repository under a `contents/posts` folder.

Check the result locally. Then commit, push, see it online. More DevOps magic.

# Cooperating

DevOps is a lot about working together. Turn to your neighbour, ask them the URL for their Git repository, and you can work together.

We won't have time for this right now but you can then clone their website locally, make changes (like adding a new poem or something else), and then open a Pull Request to their repository. This is a nice way to cooperate although there are others (like git branches).

# Summary

DevOps is about doing the heavy lifting as automatically as possible. For this workshop, I did not write a single line of code, I focused on what I wanted to do best: contents.

Once the ground work was done we were able to just focus on contents and that's one of the great things with DevOps.

If you want to dive deeper, feel free to hang out and we can discuss stuff.

`<3
matcha
