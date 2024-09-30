+++
title = 'How I setup this Hugo Blog'
date = 2024-09-26T13:00:00+01:00
draft = false
category = ['Hugo','Blog']
tags = ['setup','github-pages','github-actions']
+++
# Install Pre-Requisites

##### Install PowerShell 7

```powershell
winget install --id Microsoft.Powershell --source winget
```

##### Install VisualStudio Code

```powershell
winget install --id Microsoft.VisualStudioCode --source winget
code --install-extension ms-vscode.powershell
```

##### Install Hugo on Windows 11

```powershell
winget install --id Hugo.Hugo.Extended
```

##### Install Windows Terminal (Optional)

```powershell
winget install --id Microsoft.WindowsTerminal --source winget
```

#### Create a repo in Github

Create yourself a repo in your GitHub account
I've created mine as blog
Clone that down to your dev computer (the one above where you installed Hugo)

#### Create a new site

> Note: My source root folder is `D:\Source`, obviously replace with the source path you are using

```powershell
Set-Location -Path "D:\source"
hugo new site blog
Set-Location -Path "./blog"
"Blog Site" | Out-File "./README.md"
git init
git add --all
git commit -am "First Commit"
git branch -M main
git remote add origin https://github.com/andrewrdavidson/blog.git
git push -u origin main
git clone https://github.com/Lednerb/bilberry-hugo-theme.git themes/bilberry-hugo-theme
Remove-Item -Path "./themes/bilberry-hugo-theme/.git" -Recurse -Force
Remove-Item -Path "./themes/bilberry-hugo-theme/.github" -Recurse -Force
git add --all
git commit -am "Add theme"
git push -u origin main
$hugoConfigFile = @"
baseURL = 'https://blog.kelrys.com/'
languageCode = 'en-gb'
title = 'PowerShell and other technologies...'
theme = 'bilberry-hugo-theme'
enableRobotsTXT = true
DefaultContentLanguage = "en"
googleAnalytics = ""
[blackfriday]
  hrefTargetBlank = false
[params]
  subtitle = 'My adventures in IT'
  enableLightDarkTheme = true
  permanentTopNav = true
  stickyNav = true
  toc = true
  baseColor = "#ff8080"
  siteWidth = "2000px"
  css_modules = ["//cdnjs.cloudflare.com/ajax/libs/cookieconsent2/3.1.0/cookieconsent.min.css"]
  js_modules = ["//cdnjs.cloudflare.com/ajax/libs/cookieconsent2/3.1.0/cookieconsent.min.js","init-cookieconsent.js"]
  author = "Andrew Davidson"
  description = "PowerShell and other technologies... blog"
  keywords = "blog,personal,responsive,search,font awesome,pages,posts,multilingual,highlight.js,syntax highlighting,premium,shortcuts"
  paginate = 5
  enable_mathjax = false
  algolia_search = false
  resizeImages = true
  gravatarEMail = "github@kelrys.com"
  customImage = "/images/andrewD_256.png"
  overlayIcon = "fa-home"
  showHeaderLanguageChooser = true
  enableMomentJs = true
  dateFormat = "RFC1123"
  dateForm = "RFC1123"
  showReadingTime = false
  tocMinWordCount = 400
  showFooter = true
  amountLatestPostsInFooter = 7
  amountCategoriesInFooter = 7
  showFooterLanguageChooser = true
  showSocialMedia = false
  showArchive = true
  archiveDateGrouping = "2006-01"
  
  copyrightBy = "by Andrew Davidson"
  copyrightUseCurrentYear = true
  copyrightYearOverride = "2017"
  copyrightUrl = "https://github.com/andrewrdavidson"
  creditsText = "."
  creditsUrl = "."
"@
$hugoConfigFile | Out-File -FilePath "./hugo.toml" -Force
git add --all
git commit -am "Set hugo.toml file"
git push -u origin main

```

#### Add a post (or two)

#### Publish to GitHub Pages

enable github pages

Click Settings
In the "Code and automation" section of the sidebar, click  Pages.
Under "Build and deployment", under "Source", select GitHub Actions
Create the workflow in the .github/workflow directory

add workflow
make it run

#### Add a custom domain (optional)

Go into repo on github website
Set the domain

(remember to add a CNAME appropriately to make it work)