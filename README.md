# [Deep Speeling Blog](https://mdcramer.github.io/Deep-Speeling-Blog/)

This repo is the [blog](https://mdcramer.github.io/) for the [Deep Speeling](https://github.com/mdcramer/Deep-Speeling) project. Deep Speeling is a Recurrent Neural Network (RNN), implemented in Tensorflow, designed to correct spelling mistakes using Deep Learning.

### Special Characters
Since we would like permalinks to be generated automatically, special characters (non-english) e.g **ñ** are going to be problematic.

For this reason it's best to explicitly specify the permalink if the page title/filename contains these special characters.

For example, in **_deep-speeling-blog/2017-10-16-No-hablo-español.md**, I have explicitly specified the permalink like so:

```yaml
...
permalink: /deep-speeling-blog/no-hablo-espanol/
```

### Set up the site on your github pages
Push changes to the `blog` branch; GitHub Actions builds the site and deploys it to `master`, which is served by GitHub Pages.


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

4. To change the color of a blog header, uncomment and alter the value of the **background** entry.
For custom header images, look to main.scss.

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

