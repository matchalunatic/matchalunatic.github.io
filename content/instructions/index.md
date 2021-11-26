---
draft: false
title: "Create your own blog: instructions"
date: 2021-11-26T15:16:58+01:00

---
# create a GitHub repository

give it whatever name you want, it will be used to access your website at

`https://<YourGitHubUsername>.github.io/<YourRepositoryName>`

Do not add a README or Gitignore or whatever: an empty repository is fine.

I chose to name my repository b2021, and I use the matchalunatic GitHub account for the demo, check it out at [https://github.com/matchalunatic/b2021](https://github.com/matchalunatic/b2021).

# create a local repository and set your GitHub repository as remote

In the terminal, that's a matter of running

```bash
git init <YourRepositoryName>
cd <YourRepositoryName>
git remote add origin git@github.com:<YourUsername>/<YourRepositoryName>.git
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
baseURL = 'https://matchalunatic.github.io/b2021'
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

Using VS Code, you need to enter the "Source Control" panel:

{{<figure title="such an icon" src="scicon.png" alt="a branch icon, with three dots and connecting lines forming a Y">}}
