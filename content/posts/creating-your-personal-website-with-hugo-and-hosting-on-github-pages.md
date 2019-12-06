---
title: "Creating Your Personal Website With Hugo and Hosting on Github Pages"
date: 2019-12-06T12:51:21-05:00
draft: true


---

In this post I will explain how I've created this website your are accessing right now through the Github Pages.

Yes, it's is possible to have your personal website on Github and not expend any money with hosting and domain to access it.

The objective for this website was having a about page telling my work experience and a blog with posts explaining subjects I like to study.

The only issue with Github pages it that your website need to be static, but don't worry, we have a solution for this.

So how to have a blog that is generally a dynamic website hosting as a static website on Github Pages?

#### Hugo is the answer

Hugo is a framework that allows you generate a static website through out terminal commands.

The idea is to have 2 repositories on your Github account, the first one will be placed your source from the Hugo's project and another to receive your generated static files.

For this tutorial I'm using Mac OS, so all the instructions will be placed considering the following:

- You have Homebrew installed;
- Your are familiar using a terminal;

#### Let's begin...

First we have to install Hugo, using your preferred terminal enter:

{{< highlight bash>}}
brew install hugo
{{< / highlight >}}

To check if it was correctly installed enter

{{< highlight bash>}}
hugo version
{{< / highlight >}}

Now, we need to create your Hugo Project

{{< highlight bash>}}
hugo new site hugo_site
cd hugo_site
{{< / highlight >}}

Define it as a Git local repository

{{< highlight bash>}}
git init
{{< / highlight >}}

Let's add a [theme][themes] for this website, I'm using [Beaulfigul Hugo][beautifulhugo]

{{< highlight bash>}}
git submodule add https://github.com/halogenica/beautifulhugo.git themes/beautifulhugo
{{< / highlight >}}

This theme has a sample configuration file we can copy and use it in our project 

{{< highlight bash>}}
cp themes/beautifulhugo/exampleSite/config.toml .
{{< / highlight >}}

With our theme added, we can run our project

{{< highlight bash>}}
hugo server -D
{{< / highlight >}}

We can access it right now on your browser [http://localhost:1313/][localhost]

<imagem do website recem criado>

## Deploying

Like I explained before, we have to create two repositories on Github. 
Access your Github account and create a repository called hugo_site and another called `<your_github_username>`.github.io

Important: replace `<your_github_username>` with your exact Github username.

Let's vinculate your local repository to the Github we have created

{{< highlight bash>}}
git remote add origin git@github.com:<your_github_username>/hugo_site.git
{{< / highlight >}}

Add all files to be committed and commit all files

{{< highlight bash>}}
git add .
git commit -m "Adding initial files from my Hugo website"
{{< / highlight >}}

Now we are going to create a folder in our project to receive the static generated files and let's define it as a Git sub repository

{{< highlight bash>}}
git submodule add git@github.com:<your_github_username>/<your_github_username>.github.io.git
{{< / highlight >}}

We can now commit again all the changes made and push to the Github.

{{< highlight bash>}}
git add .
git commit -m "Second change in the initial files"
git push -u origin master
{{< / highlight >}}

For while, we only have pushed files to the hugo_site repository, but remember, Github Pages only permits you having a website with static files, so we need to push the generated static files to your other repository `<your_github_username>`.github.io.git

Let's inform Hugo that all generated files go to our `<your_github_username>`.github.io.git local folder and our URL to access our website is `<your_github_username>`.github.io. Open your config.toml and edit:

{{< highlight bash>}}
baseURL = "https://<your_github_username>.github.io/"
...
publishDir = "<your_github_username>.github.io"
...
{{< / highlight >}}

Now type the following command to generate the static files:

{{< highlight bash>}}
cd ..
hugo
{{< / highlight >}}

We are almost there, now we only commit those generated filed to our `<your_github_username>`.github.io repository

{{< highlight bash>}}
cd <your_github_username>.github.io
git add .
git commit -m "Commiting my first static generated files"
git push origin master
{{< / highlight >}}

That's it, you can access your website through out of the URL http://<your_github_username>.github.io

[themes]: https://themes.gohugo.io/beautifulhugo/
[beautifulhugo]: https://themes.gohugo.io/beautifulhugo/
[localhost]: http://localhost:1313/
