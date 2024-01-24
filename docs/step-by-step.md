# Step-by-step

## Pre-requisites
- Python
- Github CLI
- VsCode

## Assumptions
This tutorial assumes:

* You are using a computer with Windows 10 or superior;<br>
* You already have a GitHub profile. Click [here](https://docs.github.com/en/get-started/quickstart/creating-an-account-on-github) to learn how to create a GitHub profile.

## Create new GitHub repository
* Click [here](https://docs.github.com/en/repositories/creating-and-managing-repositories/quickstart-for-repositories) to learn how to create a new repository in GitHub.
- Repository created for this project: [https://github.com/szalbuque/mkdocs-githubpages-docs-automation.git](https://github.com/szalbuque/mkdocs-githubpages-docs-automation.git).

## Clone the GitHub repository to your machine
- In VSCode, click on File > Open folder and choose the folder to host the clone of the GitHub repository.
- Click on Terminal > New Terminal to open a new terminal in VSCode.
- Use the command 'git clone' to create a copy of the GitHub repository into the selected folder.

## Install MkDocs
- MkDocs requires a recent version of Python and the Python package manager, pip, to be installed on your machine. See [this page](https://www.mkdocs.org/user-guide/installation/#mkdocs-installation) to know how to meet this requirements .

- Attention!
-- If you have problems activating the Python Virtual Environment (venv), make sure you have the necessary permissions to execute scripts. See [this page](https://learn.microsoft.com/pt-pt/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.4) to learn more about these permissions. 
-- Use the commands below to create and activate the Python Virtual Environment (venv):
> python -m venv venv
> .\venv\Scripts\activate.ps1

- In VSCode, open the folder containing the clone of the GitHub repository you created.

## Create a new MkDocs Website
In VSCode, open a new terminal (Terminal > New Terminal).
Run the command below to create a new MkDocs Website:
> mkdocs new .
It creates two files:
- .\mkdocs.yml
- .\docs\index.md

## Launch the MkDocs server
Run the command below to launch the local server for the new website created:
> mkdocs serve
Open the address http://127.0.0.1:8000/ in your browser and see the default initial MkDocs website running.

## Add the 'material' theme to the website
Open the mkdocs.yml in VSCode.
Add these two lines to the file and save it:
theme:
  name: material

Remember: In YML files you must use exact number of spaces before each line. You must read the MkDocs documentation to learn how to configure the mkdocs.yml file.

## Customize MkDocs features
Add the lines below to the mkdocs.yml, then save the file and refresh the browser to see the modifications in the navigation bar and colors.
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

## Create a new page inside the website
Inside the docs folder, create a new file named page2.md
Add this line to page2.md file and save it:
* This is page 2
Refresh the browser and see the link to page2 created in the navigation bar.
Click on the link page2 and see the new page you created.

## Publish the documentation portal on GitHub Pages
Create the folder .github inside the main folder of the project.
Create the folder workflows inside the folder .github.
Create the file ci.yml inside the folder workflows.
Copy the content below inside the file ci.yml and save it.
See this page to learn more about using GitHub Actions to automate the deployment of MkDocs documentation website (https://squidfunk.github.io/mkdocs-material/publishing-your-site/).
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

## Update the GitHub repository
Open a new terminal in VSCode.
Use the commands below to push the files to the repository:
> git add .
> git commit -m "initial commit"
> git push origin main

## Configure GitHub to create a GitHub Page
Enter the repository of this project in GitHub website.
Click on the Settings option, on the navigation bar.
Click on the Pages option, on the left side menu.
Select the Source option Deploy from a branch.
Under Branch subtitle, select the branch gh-pages.
Select /(root) folder and click Save.
After you click on Save, the GitHub Actions begins the execute the workflow.

To see the workflow, click on Actions in the navigation bar.
Click on the link pages-build-deployment to see the URL of the website published.












