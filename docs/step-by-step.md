# Step-by-step

## Pre-requisites
- Python
- Github CLI
- VsCode

## Assumptions
This tutorial assumes that:

* You are using a computer running Windows 10 or higher;<br>
* You already have a GitHub profile. Click [here](https://docs.github.com/en/get-started/quickstart/creating-an-account-on-github) to learn how to create a GitHub profile.

## Create a new GitHub repository
* Click [here](https://docs.github.com/en/repositories/creating-and-managing-repositories/quickstart-for-repositories) to learn how to create a new repository on GitHub.
- The repository I created for this project is: [https://github.com/szalbuque/mkdocs-githubpages-docs-automation.git](https://github.com/szalbuque/mkdocs-githubpages-docs-automation.git).

## Clone the GitHub repository to your computer
- In VSCode, click on `File > Open folder` and select the folder to host the clone of the GitHub repository.
- Click on `Terminal > New Terminal` to open a new terminal in VSCode.
- Use the `git clone` command to create a copy of the GitHub repository into the selected folder. 
- See the example below.
```
git clone https://github.com/szalbuque/mkdocs-githubpages-docs-automation.git
```
- In this example I used my repository. You need to use the repository you created.
- Click [here](https://docs.github.com/pt/repositories/creating-and-managing-repositories/cloning-a-repository) to learn how to clone a GitHub repository.

## Install MkDocs
- MkDocs requires a recent version of Python and the Python package manager, <i>pip</i>, to be installed on your machine. See [this page](https://www.mkdocs.org/user-guide/installation/#mkdocs-installation) for information on how to meet these requirements .

!!! warning

    If you have problems activating the Python Virtual
    Environment (venv), make sure you have the necessary
    permissions to run scripts. See [this page](https://learn.microsoft.com/pt-pt/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.4)
    to learn more about these permissions.

## Create a new MkDocs website
* In VSCode, open the folder that contains the clone of the GitHub repository you created.
* Open a new terminal `(Terminal > New Terminal)`.
* Use the following commands to create and activate the Python Virtual Environment (venv):
```
python -m venv venv
.\venv\Scripts\activate.ps1
```

* Run the following command to create a new MkDocs website:
```
mkdocs new .
```
* MkDocs will create two files:

| Description | File |
|-------------|------|
| Contains the configurations for creating the website. |     .\mkdocs.yml |
| Contains a sample content. |     .\docs\index.md |

## Start the MkDocs server
* Run the following command to start the local server for the newly created website:
```
mkdocs serve
```
* Open the address [http://127.0.0.1:8000/](http://127.0.0.1:8000/) in your browser and see the default initial MkDocs website running.

## Add the 'material' theme to the website
* Open the mkdocs.yml file in VSCode.
* Add these two lines to the file and save it:
```
theme:
  name: material
```
!!! warning

    In YML files you must use the exact number of spaces before each line. You must read the MkDocs documentation to learn how to configure the mkdocs.yml file.
* Refresh the page [http://127.0.0.1:8000/](http://127.0.0.1:8000/) in your browser and see what changes.

## Customize MkDocs features
* Add the following lines to the <i>mkdocs.yml</i> file, then save the file and refresh the browser to see the changes in the navigation bar and colors.
```
site_name: MkDocs with GitHub Pages Tutorial
theme:
  name: material
  features:
    - navigation.tabs
    - navigation.sections
    - toc.integrate
    - navigation.top
    - search.suggest
    - search.highlight
    - content.tabs.link
    - content.code.annotation
    - content.code.copy
  language: en
  palette:
    - scheme: default
      toggle:
        icon: material/toggle-switch-off-outline 
        name: Switch to dark mode
      primary: teal
      accent: purple 
    - scheme: slate 
      toggle:
        icon: material/toggle-switch
        name: Switch to light mode    
      primary: teal
      accent: lime
```
## Create a new page within the website
* In the <i>docs</i> folder, create a new file named <i>page2.md</i>
* Add this line to the <i>page2.md</i> file and save it:

```
 This is page 2
```

* Refresh the browser and see the link to page2 created in the navigation bar.
* Click on the page2 link and see the new page you created.

## Publish your documentation portal to GitHub Pages
### Prepare the local repository
* Create the folder <i>.github</i> inside your project´s root folder.
* Create the folder <i>workflows</i> inside the <i>.github</i> folder.
* Create the <i>ci.yml</i> file inside the  <i>workflows</i> folder.
* Copy the following content into the <i>ci.yml</i> file and save it.

(1) See more...
{ .annotate }

1. [Click here to learn more about using GitHub Actions
   to automate the deployment of MkDocs documentation website](https://squidfunk.github.io/mkdocs-material/publishing-your-site/).

```
name: ci 
on:
  push:
    branches:
      - master 
      - main
permissions:
  contents: write
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: 3.x
      - uses: actions/cache@v2
        with:
          key: ${{ github.ref }}
          path: .cache
      - run: pip install mkdocs-material
      - run: mkdocs gh-deploy --force
```

### Update the GitHub repository
* Open a new terminal in VSCode.
* Use the following commands to push the files to the repository:
```
git add .
git commit -m "initial commit"
git push origin main
```

### Configure GitHub to create a GitHub Page
* Enter the repository for this project on the GitHub website.
* Click on the `Settings` option, on the navigation bar.
* Click on the `Pages` option, on the left side menu.
* Select the `Source` option `Deploy from a branch`.
* Under `Branch` subtitle, select the branch `gh-pages`.
* Select `/(root)` folder and click `Save`.
* After you click on `Save`, the GitHub Actions will begin executing the workflow.

* To view the workflow, click on `Actions` in the navigation bar.
* Click `pages-build-deployment` link to see the URL of the published site.












