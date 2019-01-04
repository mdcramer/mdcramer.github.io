# [Deep Speeling Blog](https://mdcramer.github.io/Deep-Speeling-Blog/)

This repo is the [blog](https://mdcramer.github.io/Deep-Speeling-Blog/) for the [Deep Speeling](https://github.com/mdcramer/Deep-Speeling) project. Deep Speeling is a Recurrent Neural Network (RNN), implemented in Tensorflow, designed to correct spelling mistakes using Deep Learning.

### Special Characters
Since we would like permalinks to be generated automatically, special characters (non-english) e.g **ñ** are going to be problematic.

For this reason it's best to explicitly specify the permalink if the page title/filename contains these special characters.

For example, in **_deep-speeling-blog/2017-10-16-No-hablo-español.md**, I have explicitly specified the permalink like so:

```yaml
...
permalink: /deep-speeling-blog/no-hablo-espanol/
```

### Set up the site on your github pages
To setup the website, we shall use a different approach than you have used before. We shall:
* Use forestry.io
* Use 2 repos. The current repo will act as the source. All the changes to your site will occur on this repo. The second repo will serve as the deployment repo. Follow the following steps

1. **Unpublish https://mdcramer.github.io/Deep-Speeling-Blog**
I suppose you already  now how to do this

2. **Sign Up for an account on forestry.io**
Forestry.io will do the following for you.
* Sync with the source repo (this repo) and generate your site on the deployment repo everytime you make changes to the repo.
* Provide you with a cms. This means you can opt to make changes to your site through their dashboard if you choose to. It will by no means overhaul your workflow; it will just be an added option.

I would recommend you signup for an account through github.

3. **Import your site into forestry.io**
Follow this quick guide https://forestry.io/docs/git-sync/github/...

4. **Create the deployment repo on your github**
Create a new repo and name it **mdcramer.github.io**. Initialize it with an empty readme file. That will be all for now.

5. **Go back to forestry.io**
Go to the site you imported. You will need to play with settings here. We will set the source and deployment repos here.


### Adding a new blog
Let's say you want to add a new blog called **Neural Engines**, this is all you need to do
 
1. Create a folder called **_neural-engines.md**
2. Register the new collection in **_config.yml**

Current *_config.yml*
```yaml
...
collections:
  deep-speeling-blog:
    output: true
    permalink: /deep-speeling-blog/:path/
...
```

New *_config.yml*
```yaml
...
collections:
  deep-speeling-blog:
    output: true
    permalink: /deep-speeling-blog/:path/
  neural-engines:
    output: true
    permalink: /neural-engines/:path/
...
```
3. Add the description of the new blog in **_data/blogs.yml**
This description will be used to list the blog in the home page:

Current *_data/blogs.yml*
```yaml
# [name] values should be written in lower case
- name: deep speeling blog
  description: A blog for Mark Cramer's Deep Speeling Github repository. Recurrent neural network (RNN) using Tensorflow designed to correct spelling mistakes.
  # background: darkgoldenrod
```
New *_data/blogs.yml*
```yaml
# [name] values should be written in lower case
- name: deep speeling blog
  description: A blog for Mark Cramer's Deep Speeling Github repository. Recurrent neural network (RNN) using Tensorflow designed to correct spelling mistakes.
- name: neural engines
  description: Something interesting about neural engines ...
  # background: darkgoldenrod
```

> The **name** entry in this data file must always be in lower case

> To change the color of a blog header, uncomment and alter the value of the **background** entry

## Working locally

If you're working locally, make sure you're on the right branch. From your terminal
1. cd to your project directory
2. Checkout to your working git branch, like so:

```
git checkout -b blog
```

3. Once you're done working, push your changes to the right branch like so:

```
git push --set-upstream origin blog
```

> Note that the above git commands assume that your working git branch is **blog**

