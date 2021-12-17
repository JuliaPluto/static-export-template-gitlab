# Statically exporting Pluto notebooks in GitLab

This is a demo repository containing one Pluto notebook that is **automatically converted to HTML** by GitLab CI/CD, and published to GitLab pages! 🌝

This project is forked from [static-export-template](https://github.com/JuliaPluto/static-export-template).

See the gitlab repository running the [CI/CD pipelines](https://gitlab.com/sosiristseng/static-export-template-gitlab/-/pipelines).

And the exported gitlab pages is [here](https://gitlab.com/sosiristseng/static-export-template-gitlab/pages)


More info here:
<https://www.notion.so/Interactive-web-articles-bf3af6de77854660807e674148c27b1f#1a997e538e0d48e0bf54d2d5f29dfc2b>

This project is at its infancy so be careful to use the code in this repository for your own projects.

## How to use this template

### 👉 Step 1

Create a GitLab account, and fork this repository to your GitLab projects.

![image](https://user-images.githubusercontent.com/40054455/123437682-8552b200-d602-11eb-8daa-d7aaeca3eb7e.png)


### 👉 Step 2

Click on **Upload file** to upload your `.jl` notebook files and commit changes.

![image](https://user-images.githubusercontent.com/40054455/123435949-b16d3380-d600-11eb-8597-30d324f608b8.png)

Your notebooks will run on gitlab every time that you add / update the files in this repository. To check the progress, click on `CI/CD` -> `Pipelines`, you will find the _jobs_ for the last commit.

![image](https://user-images.githubusercontent.com/40054455/123438575-67d21800-d603-11eb-991f-84ee90b6808f.png)

Wait for the GitLab CI/CD to finish running your notebook and publish the HTML files to GitLab pages. The URL is available in the `Settings` -> `Pages` of your repository.

## Update notebook files

To update an existing notebook file, simply repeat Step 2 above! 

You can also click on the file and then press **Replace** to update a file that already exists on the repository.

![image](https://user-images.githubusercontent.com/40054455/123435720-73700f80-d600-11eb-9c44-7b4ad699a969.png)


## Setup in an existing repository

If you already have a GitLab repository with some pluto notebooks in it, you may want to add a web view like the one for your repository. In that case, the steps are slightly different. In this case, I assume that you are familiar with managing a repository. If not, follow the steps above.

### 👉 Step 1

Make sure that all your Pluto notebooks can be run from a fresh Julia environment. See the tips below about packages.

### 👉 Step 2

From this repository, download [`.gitlab-ci.yml`](.gitlab-ci.yml) and save the file in your own repository root. Commit it to your repository.

*Note: The YAML file assumes you are using `main` as the default branch. Change `main` to your default branch name in line 28 and 41 if necessary.*

The rest is the same as `👉 Step 2` in the previous section.


## 💡Tips

### Environment for the notebooks

Please see [🎁 Package management](https://github.com/fonsp/Pluto.jl/wiki/🎁-Package-management) in Pluto notebooks. (Requires Pluto 0.15+)

### Homepage

If you go to the website URL of this repository, you will see a small index of the notebooks in this repository if you don't have a `index.html`. You can customize this page, two options are:

- Create your own `index.html`, it will be used as the homepage.
- Rename one of your notebooks to `index.jl`, and it will be the default notebook!
