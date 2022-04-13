# Overview Developer Docs

## Overview
### part 1
- userdocs
- installation
- pelican
- jinja2
- javascript
- content

- templates
    - blocks
	- static (see themes first)
	- critical css (see themes first)
- websites
  - publishconfig
  - pelicanconfig
- custom-page
- custom-template
- drafts
- npm
- themes
- custom-css
- design resources

### part 2
- scripts
    - copy_content
	- parse_content -> see plugins/content-aggregator
	- parse_publication -> see publication pipeline
- above-the-fold
- plugins
    - bootsrapify
    - content aggregator
    - edit-url
    - fileutil
    - pagehierachy
    - imgutil
    - inline extend
    - bibtex loader
- publication pipeline
    - diag-literature
    - parse publications
    - bibliography
- imgoptim
	- optimize images

  
### part 3
- netlify
- hosting (yourhosting)
- dns
- assets
- deploy
- github actions
- webteam deploy bot
	- webteam deplot bot, used for deploying the wesbites
	 - two secrets 
		1. curl diag.bib (used in parse publications)
		2. workflow dispatch (used in github action diag-literature)

- development branch / deploy
- security
- google analytics
- colofon
- techdocs and documentation website 
 
---

## Part 1

### User docs
The user documentation can be found in docs/. This documentation explains user how to add/change content. In addtiotion is includes some advanced topics about css, redirects and website configuration. A new webteam member should become familiar with all the user documentions. 

### Installation 
Installation for developers can be done in two ways: 

#### Locally 

To get website local running, the following steps need to be taken

    - clone repository 
    - install requirements (recommendation is to use a conda/virtual environment)

#### Docker

A dockerfile is provided to to build a container (in progress)

### pelican
Pelican is a static site generator that requires no database or server-side logic.
Some of Pelican’s features include:
- Write content in reStructuredText or Markdown markup
- Completely static output is easy to host anywhere
- Themes that can be customized via Jinja templates
- Publish content in multiple languages
- Atom/RSS feeds
- Code syntax highlighting
- Import from WordPress, RSS feeds, and other services
- Modular plugin system and corresponding plugin repository

### jinja2
Jinja is a fast, expressive, extensible templating engine. Special placeholders in the template allow writing code similar to Python syntax. Then the template is passed data to render the final document.

### javascript
JavaScript is a scripting or programming language that allows you to implement complex features on web pages — every time a web page does more than just sit there and display static information for you to look at — displaying timely content updates, interactive maps, animated 2D/3D graphics, scrolling video jukeboxes, etc. — you can bet that JavaScript is probably involved. Even though we use a relatively stimple static website build (pelican) some javascript is used.  

### content
We have 2 types of content folders
- Content folder in main folder (website-content)
- Content folders in separate website folders (e.g., website-pathology).  
The copy_content.sh script copies content from the main folder to a website folder (this is also one of the first scipts you need to run in order to build a website locally). Within the copy_content.sh script, the default website pages are copied (such as the home page, 404 and the colofon), the content bib files are copied, and the parse_content.sh script is called which copies only the relevant site specific content to the website folder. Later down the website building pipeline some of the files of the websites' content folders are generated automatically by --BY WHAT--?.  

### templates
The radboudumc-template folder contains the website page templates, as well as subfolders for recurring blocks of code, css (page and text layout style sheets). 

The html templates provide backbones of the web pages. They contain many jinja placeholders that are filled in automatically when the websites are built. -- NOT SURE HOW THESE ARE USED

#### blocks
Blocks are pieces of code that can be used in multiple pages. For example there is a code block that can be used to show the website viewer where he/she is in our sites (called breadcrumbs). For example, it shows: Home / Members / -Member name-
Using these blocks of code on websites are optional (for example this breadcrumb option is used in www.computationalpathologygroup.eu but not in www.diagnijmegen.nl)

#### static folder (see themes first)
This contains some default css and js files
-- Not sure how these relate to critical css

#### critical css (see themes first)
The critival css files contain the default style sheets of their corresponding pages. This default css file makes sure the site will always render (almost) properly, even if a site specific css file is missing. --

More information here: website-content/docs/critical-above-the-fold-css.md 

### websites
general info here. Separate folders containthing the main structure 
Websites also contain the following files that are essential for the build of these sites: 


#### pelicanconfig
The pelican_config.py files contain the site-wide settings that control the build of the website.
For example the NAV_SECTIONS control which site pages are shown in the navigation bar on thop of the website.

More infor here: website-content/docs/website-configuration.md

#### publishconfig
--NO IDEA--

### custom-page
Custom pages are 'stand alone' pages such as https://www.diagnijmegen.nl/doing-a-phd-at-diag/

Custom pages can be made by (1) overwriting a default page, or (2) by creating an independent page.

More info here: website-content/docs/create-custom-page.md

### custom-template

### drafts

### npm

### themes

### custom-css

### design resources



## part 2

### scripts

#### copy_content and parse_content -> see plugins/content-aggregator
The copy_content.sh script copies content from the main folder to a website folder (this is also one of the first scipts you need to run in order to build a website locally). Within the copy_content.sh script, the default website pages are copied (such as the home page, 404 and the colofon), the content bib files are copied, and the parse_content.sh script is called which copies only the relevant site specific content to the website folder. Later down the website building pipeline some of the files of the websites' content folders are generated automatically by --BY WHAT--?.  

#### parse_publication -> see publication pipeline
-- Not sure where this is called

More info here: website-content/docs/publications-pipeline-developers.md

### above-the-fold
Above the fold content is what is shown to the website viewer when he/she enters our website (without scrolling). -- not sure what we do with this

### plugins
#### bootsrapify
The bootstrap plugin contains many predefined classes for html. 
#### content aggregator
#### edit-url
#### fileutil
#### pagehierachy
#### imgutil
#### inline extend
#### bibtex loader

### publication pipeline
#### diag-literature
#### parse publications
#### bibliography

### imgoptim

#### optimize images

  
## part 3

### netlify
Netlify is used to build an deploy our websites. We trigger this with GitHub actions. 
### hosting (yourhosting)
yourhosting hosts our domain names
### dns
DNS links our domain names to our websites deployed by Netlify
### assets

### deploy

### github actions
In the .github folder > workflows > actions the github actions are stored. The "deploy-master.yml" file describes how the master branch is deployed using netlify. This github action is triggered when changes are comitted/pushed to the master branch. Within the repo's readme file there is a button on top that whows whether the master branch deploys succesfully (green) or not (red). If built unsuccessfully, you can start debugging by inspecting the github actions tab, and check the error messages within the corresponding failed build. If a build fails, websites will still remain online since it will continue to show the last successful build.

The "deploy-develop.yml" is used to deploy the develop branch. This is for example used to check out big layout changes of our websites, which is generally not a task for the webteam.

The "images.yml" file is used to optimize the images used on our sites to make our sites more lightweight. Ofcouse a faster loading site is better, but another side effect of a well optimized site is that google will like your site and make it more findable (show your site higher in google's search results)/

### webteam deploy bot
#### webteam deploy bot, used for deploying the wesbites
#### two secrets 
    1. curl diag.bib (used in parse publications)
    2. workflow dispatch (used in github action diag-literature)

### development branch / deploy

### security

### google analytics

### colofon

### techdocs and documentation website 
 
---
