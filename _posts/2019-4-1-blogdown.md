---
layout: post
title: blogdown | Creating self-website using R Markdown
---

Source: [Yihui Xie, et al. blogdown](https://bookdown.org/yihui/blogdown)
**Note**: "" means the content is collected from the source book.

# A recommended workflow
- **To start a new website**  
1. pick a theme at [Hugo](http://themes.gohugo.io) -> "Download" to find the GitHub repository link, e.g. https://github.com/gcushen/hugo-academic.  
2. Create a new project in RStudio -> `blog-down::new_site(theme = gcushen/hugo-academic)`.  
3. Edit the options in **config.toml** if necessary, details in the **README** page of the theme.

- **To edit a website**  
1. Open the project -> "Tools" -> "Addins" -> "Serve Site" to preview the site in Viewer.  
2. "Addins" -> "New Post" to create a new post or page, then edit the content.  
3. "Addins" -> Update Metadata" to modify the YAML metadata if necessary.  

- **To customize the site**  
- Using config.toml to set global options without touching theme authors' template files.  
  Refer to following **config.toml** section for more details.
  
- The other way is to leave a few lightweight template files under "layouts/" in the theme, so that we could override them without touching the core template files. Take the XMin theme for example:  
Yihui put two empty HTML files *head_custom.html* ("will be added inside <head></head> of a page, e.g. to load JavaScript libraries or include CSS style sheets via <link>") and *foot_custom.html* ("added before the footer of a page, e.g. to load additional JavaScript librarier or embed Disqus comments there") under *layouts/partials/* in the theme.  

**Note**:

1. The latter way "means you only need to create and maintain at most two files under layouts/ instead of maintaining all files under themes/. Note that this overriding mechanism applies to all files under layouts/, and is not limited to the partials/ dir. It also applies to any Hugo theme that you actually use for your website, and is not limited to hugo-xmin."

2. Similarly, we can partially override static files using the same mechanism as overriding layouts/ files, i.e. "static/file" will override "themes/theme-name/static/file".

- **To publish a website**  
- Without GitHub way
1. Restart the R session -> `blogdown::hugo_build()`, then a "public/" dir is created under the root dir of the project.  
**Tips**: A doc could be setted as a draft by setting `draft: true` in corresponding YAML metadata. Draft posts will not be rendered if the site is built via `blogdown::build_site() or blogdown::hugo_build()`, but will be rendered in the local preview mode.(**Chapter 3**)
2. Log into [Netlify](https://www.netlify.com/) using the GitHub account.  
3. Is this your first time to publish a website?  
  - Y. Create a new site -> Drag and drop the "public/" folder to the indicated area on the Netlify web page.  
  - N. Update the existing site you created last time.  
4. Wait for Netlify to deploy the files, and the assigned random subdomain of the form "random-word-12345.netlify.com".  
5. Change the random subdomain to a more meaningful one.  

- With GitHub way  
Create a new website on Netlify from the GitHub repos that contains the source files of the website, so that we could continuously deploy the site instead of manually uploading the "public/" every time.
Details in Chapter 3.

**Tips**  
- `weight`: which is YAML metadata, is used to tell Hugo the order of pages when sorting them, e.g. when you generate a list of all pages under a dir, and two posts have the same date, you may assign diff weights to them to get the desired order on the lis.  

---
## Things to know | from the Preface
- "A well-designed and maintained website can be extremely helpful for other people to know you, and you do not need to wait for suitbale chances at conferences or other occasions to introduce yourself in person to other people."
- Using Hugo to generate static website. All pages are built from blogdown and Hugo.
- Authors' homepage to refer:
  - Yihui's: Chinese version: https://yihui.name/cn/     English version: https://yihui.name/en/   https://yihui.name/knitr/
  - Amber's: https://amber.rbind.io
  - Alison's: https://alison.rbind.io
- Structure of the blogdown book:
  - Chapter 1: quick start to create a new website based on **blogdown**.
  - Chapter 2: intro the static website generator Hugo, on which blogdown is based.
  - Chapter 3: ways to publish a website, i.e. other people can visit it through a link.
  - Chapter 4: ways to migrate existing websites from other platforms to Hugo and blogdown.
  - Appendix A: a quick tutorial on R Markdown.
  - Appendix B: basic knowledge about websites, such as HTML, CSS, and JavaScript. Need to learn then if creator are care    
                about the website.
  - Appendix C: ways to have owner's domain name.
  - Appendix D: some optional topics for advanced users.
- Organization of the posts:
  - "typically blog posts are stored under the *content/post/* dir"
  - "pages are under other dirs (including the root *content/* dir and its subdirs), but Hugo doesn't require this stucture."
  
## Tricks to keep in mind
- `blogdown::new_site()` to create a new site, downloading the default theme, add some sample posts, etc. and launch in the      RStudio Viewer.
- *LiveReload*
  - website will be auto rebuilt and reloaded in the web browser when modifying any source file.
  - `blogdown::serve_site()`.
  - uncheck both "Preview site after building" and "Re-knit current preview when supporting files change", as the options         are not really useful after calling `serve_site()`.
- *config.toml*
  - in the root dir, i.e. /config.toml.
  - options like title, description of the site, links to social networks, the navigation menu, and the base URL for the site.
  - set global settings, e.g. `title = "Ming"`. All options are listed [here](https://gohugo.io/overview/configuration/).
  - useful options  
  
  ```
  # baseurl: set this only when we have a domain name for the site. Do not forget the trailing slash.
  baseurl = "/"  
  
  # relativeurls: Set this only if we want to view the site locally through the file viewer. Defaul is false, it means the       site must be viewed via a web server, e.g. blogdown::serve_site() has provided a local web server, so we can preview the       site locally when relativeurls = false.
  relativeurls = false
  
  # disqusShortname: The Disqus ID created during the account settings at [Disqus](https://disqus.com). Disqus is a system       enabling commenting on the site. Note that setting up a functional baseurl and website publish is required before Disqus       comments func can work.
  disqusShortname = ""  
  
  # ignoreFiles: >=3 patterns patterns (regex) for Hugo is recommended to being ignored when building the site.  
  ignoreFiles = ["\\.Rmd$", "\\.Rmarkdown", "_files$", "_cache$"]  
  
  # .Rmd files should be ignored as blogdown will compile them to .html, and it suffices for Hugo to use the .html files.  
  # Dir with suffixes _files and _cache should be ignored as they contain auxiliary files after an Rmd file is com[iled.
  
  # links to show on each page
  [social]
	    github = "https://github.com/rstudio/blogdown"
  	  twitter = "https://twitter.com/rstudio"  

  # It is recommended to set this option to true, so that Hugo's automatic summary and word count work better.
  hasCJKLanguage
  
  ```
  
  ```
  # generate permanent links of the page. ":slug" is recommended instead of ":title". A slug is used to identify a specific       post. A slug will not change, even if the title changes, e.g. change title of a post from "title1" to "title2", and the       post's title was used in the URL, the old links will be broken if we set the options with ":title". If we specified the       URL via ":slug", then the link will not be broken when changing the title as many times we'd like!
  [permalinks]
      post = "/:year/:month/:day/:slug"
  ```
  
  ```
  # To avoid repeat coding in Hugo themes, user could set params option to easily edit a single config file to apply the theme   to the site, instead of going through many HTML files and making changes one by one, e.g. .Site.Params.author is Tom with     the following config file:  
  [params]
  	author = "Tom"
	dateFormat = "2006/01/02"
  ```
  
- *content/*
  - to write the R Markdown or Markdown source files for the posts and pages. Free to organize arbitrary files and dirs           under *content/* to structure the website.
- *public/*
  - Related with publishing the website, details in Chapter 3.
  - No need to manually add any files to this dir.
  - Typically it contains lots of \*.html, \*.css, \*.js, and images.
  - We can upload everything under *public/* to any web server that can serve static websites, and the website will be up         and running.
- *Themes*
  - custom themes in Section 1.6.
  - Learning techs like the Hugo templating language, HTML, CSS and JavaScript are required to custom a more complicated and       fancier theme.
- *Addins* -> *Browse Addins*
  - `blogdown::New Post` -> Execute -> Install Package -> type info such as title, author, etc. -> edit auto created `*.md`       to write the content of the post. Sig to specify **categories and tags** to better organize the posts!
  - `blogdown::Update Metadata` -> update the YAML metadata of the currently opened post.
- *Build Website*
  - `blogdown::newsite()` -> a pane in RStudio named "Build" -> click "Build Website" button -> RStudio subsequently call         `blogdown::buildsite()` func -> files will be auto generated in the *public/* dir;
  - followed up with above steps -> restart R and click "Build Website" -> publish the website.
- *Global options*
  - Set global options either use a global profile *~/.Rprofile* or a per-project *.Rprofile* under the project, the former       will be applied to all R sessions, unless we use latter setting to override it. Global options, e.g. blogdown.author to       set the default author of new posts, blogdown.ext to set the default extension of new posts, like ".md".
  - `file.edit("~/.Rprofile")` to set global options for all R sessions.
  - e.g. `options(blogdown.ext = ".md", blogdown.author = "Ming")`
  - After above setting, everytime I use the RStudio addin "New Post", the options will be auto populated.
  - Note that R will silently ignore the last line of ur .Rprofile if it doesn't have a trailing newline, so make sure add         at least one newline to the end of the .Rprofile.
  
## R Markdown vs. Markdown
- For R code chunks
    
    **Plain Markdown format**
  
    > \`\`\`r \# no {} here  
    > R code chunks  
    > \`\`\`
    
  disadvantage: R code will not be executed...
    
  advantage: for pure demonstration purposes.
    
  **vs.**
    
   **R Markdown format**
  
    > \`\`\`{r}  
    > R code chunks  
    > \`\`\`
    
  advantage: R code will be executed and corresponding results will be displayed! :)
  
- For math expressions: The authors added **MathJax** support to the default theme (hugo-lithium) in blogdown to render LaTeX math on HTML pages.

    **Plain Markdown format**
    
    *For plain inline math expressions*  
    ```
    `$math$`
    ```
    
    *For display-style expressions*  
    ```
    `$$math$$`
    ```
    
    **R Markdown format**
    
    *For plain inline math expressions*  
    `$math$`
    
    *For display-style expressions*  
    `$$math$$`
    
**Note:**
- Most R Markdown syntax is similar as plain Markdown.
- R Markdown doc is compiled through packages rmarkdown, [bookdown(https://bookdown.org/yihui/bookdown/components.html)         and [Pandoc](http://pandoc.org/MANUAL.html#pandocs-markdown), by which most features are avail. Yihui recommended             reading doc of Pandoc and bookdown to know possi features. Example website [here](https://blogdown-demo.rbind.io).
- There is another type of R Markdown doc with extension .Rmarkdown, such doc are processed by Hugo instead of Pandoc.           We cannot use Markdown features onlu supported by Pandoc, such as citations. In fact, there is a limited func with             compiling .Rmarkdown.
- Use `rmarkdown::html_document` to set options for the format `blogdown::html_page`, e.g. to set options for                   blogdown::html_page() globally, create a `_output.yml` file under the root dir of the website. The YAML files should           contain the output format directly, below is an example  
> blogdown::html_page:  
>   toc: true  
>   fig_width: 6 # 6 inches  
>   dev: "svg" # for plots
- If code chunk has graphic output, avoid using special char like spaces in the chunk label, try to use alphanumeric char        and dashes, e.g. \`\`\`{r, my-label}\`\`\` instead of \`\`\`{r, my label}\`\`\`.
- Temporarily change extension from .Rmd to unknown extension such as .Rmkd to prevent blogdown from compiling the R            Markdown post.
     
## Other themes
[Hugo themes](http://themes.gohugo.io). Not all themes have been tested against blogdown. If not working, try a diff one.
- pick a fancy theme, note down the GitHub username and repository name
- under another new dir, install the theme using `blogdown::new_site(theme = "gcushen/hugo-academic") #username/repos`
- recommended themes: hugo-academic, Tranquilpeak.


