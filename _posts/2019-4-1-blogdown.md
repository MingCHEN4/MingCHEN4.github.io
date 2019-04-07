---
layout: post
title: blogdown: Creating self-website using R Markdown
---

Source: [Yihui Xie, et al. blogdown](https://bookdown.org/yihui/blogdown)

# A recommended workflow
- **To start a new website**  
1. pick a theme at [Hugo](http://themes.gohugo.io) -> "Download" to find the GitHub repository link, e.g. https://github.com/gcushen/hugo-academic.  
2. Create a new project in RStudio -> `blog-down::new_site(theme = gcushen/hugo-academic)`.  
3. Edit the options in **config.toml** if necessary, details in the **README** page of the theme.

- **To edit a website**  
1. Open the project -> "Tools" -> "Addins" -> "Serve Site" to preview the site in Viewer.  
2. "Addins" -> "New Post" to create a new post or page, then edit the content.  
3. "Addins" -> Update Metadata" to modify the YAML metadata if necessary.  

- **To publish a website  
- Without GitHub way
1. Restart the R session -> `blogdown::hugo_build()`, then a "public/" dir is created under the root dir of the project.  
2. Log into [Netlify](https://www.netlify.com/) using the GitHub account.  
3. Is this your first time to publish a website?  
  - Y. Create a new site -> Drag and drop the "public/" folder to the indicated area on the Netlify web page.  
  - N. Update the existing site you created last time.  
4. Wait for Netlify to deploy the files, and the assigned random subdomain of the form "random-word-12345.netlify.com".  
5. Change the random subdomain to a more meaningful one.  

- With GitHub way  
Create a new website on Netlify from the GitHub repos that contains the source files of the website, so that we could continuously deploy the site instead of manually uploading the "public/" every time.
Details in Chapter 3.

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
  - to custom global settings for the site, e.g. `title = "Ming"`.
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


