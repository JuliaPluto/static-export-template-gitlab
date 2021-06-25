# Staticaly exporting Pluto notebooks in GitLab

This is a demo repository containing one Pluto notebook that is **automatically converted to HTML** by GitLab CI/CD, and published to gitlab pages! 🌝

This project is forked from [static-export-template](https://github.com/JuliaPluto/static-export-template).

See the gitlab repository running the CI/CD pipelines:

<https://gitlab.com/sosiristseng/pluto-static-export-template>

And the exported gitlab page:




More info here:
<https://www.notion.so/Interactive-web-articles-bf3af6de77854660807e674148c27b1f#1a997e538e0d48e0bf54d2d5f29dfc2b>

This project is at its infancy so be careful to use the code in this repository for your own projects.

## How to use the template

### 👉 Step 1

Create a GitLab account, and fork this project to your own.

### 👉 Step 2

Click on **Add files**, and then **Upload files**. In the next page, upload your `.jl` notebook files.

Your notebooks will run on gitlab every time that you update the files in this repository. To check the progress, click on `CI/CD` -> `Pipelines`, you will find the _jobs_ for the last commit.

Wait for the GitLab CI/CD to finish running your notebook.

## Update notebook files

To update an existing notebook file, simply repeat Step 2 above! (You can also use **Add files** `>` **Upload files** to _update_ upload a file that already exists on the repository.)

## Alternative setup: add web pages to an existing repository

If you already have a github repository with some pluto notebooks in it, you may want to add a web view like the one for this repository. In that case, the steps are slightly different. In this case, I assume that you are familiar with adding files to a repository. If not, follow the steps above.

### 👉 Step 1

Make sure that all your Pluto notebooks can be run from a fresh Julia environment. See the tips below about packages.

### 👉 Step 2

From this repository, download [`.gitlab-ci.yml`](.gitlab-ci.yml)

Save the file in your own repository, in the same location: make a folder `.github` in the main directory, within that a folder `workflows`, and add the file there, with the name `ExportPluto.yaml`. Commit the new file to your repository. 

*Note: The yaml file states that github should use the github notebooks in the `main` branch or `master` branch of your repository. If you changed the name of your default branch, or you want to use a different branch, change `main` in [line 5](https://github.com/JuliaPluto/static-export-template/blob/main/.github/workflows/ExportPluto.yaml#L5) in the yaml file to the name of your favourite branch.*

Your notebooks will run on github every time that you update the files in this repository. To check the progress, click on ["Actions"](./actions), you will find the _workflow_ for the last commit.

<img width="400" alt="Schermafbeelding 2021-01-06 om 00 45 25" src="https://user-images.githubusercontent.com/6933510/103711844-978b5600-4fb8-11eb-8b1b-1e5bdacc1c85.png">

### 👉 Step 3

Go to the ["Settings"](./settings) page of your repository, and in the left pane, choose the category _"Pages"_. For the "Source", choose `gh-pages`. Wait a minute for everything to initialize, and the URL to your web page will be shown! 

<img width="400" alt="Schermafbeelding 2021-01-06 om 00 43 00" src="https://user-images.githubusercontent.com/6933510/103711695-43807180-4fb8-11eb-9ba8-a96a70612177.png">

Don't worry if it doesn't work immediately! It can take a while for the web page to be ready, even after your settings page says it's done. (Github pages says 20 minutes, but it can take even longer.)


## 💡Tips

### Julia Packages

When your notebook runs on gitlab, no packages are installed. To solve this, you need to **declare a package environment** inside the notebook, using `Pkg`.

For example, instead of:

```julia
using Plots
```

```julia
using PlutoUI
```

You should write:

```julia
begin
    import Pkg
    # activate a clean environment
    Pkg.activate(mktempdir())

    Pkg.add([
        Pkg.PackageSpec(name="Plots"),
        Pkg.PackageSpec(name="PlutoUI"),
        # ... keep adding your packages
    ])

    using Plots
    using PlutoUI
    # ... place all usings and imports into this one cell
end
```

**You can use [this helper tool](https://fonsp.com/article-test-3/pkghelper.html) to generate these commands!**

**Important to note:**

-   Place the Pkg commands and the imports in the same cell.
-   You can use the same setup when running your notebook locally. Julia will re-use existing package installations, so this will only download and install packages the first time.

_In the future, Pluto will automate this process for you!_ 🙈

### Homepage

If you go to the (GitLab Pages) URL of repository, you will see a small index of the notebooks in this repository. You can customize this page, two options are:

-   Create your own `index.html`, it will be used as the homepage.
-   Rename one of your notebooks to `index.jl`, and it will be the default notebook!