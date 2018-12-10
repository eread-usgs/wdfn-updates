wdfn-updates
------------

*Updates from USGS Water Data For The Nation*

# Guidelines for submission
1. Applicable/useful to a greater audience.
2. Content provides additional information not available elsewhere.
3. Relevant to USGS employees or USGS data users
4. Showcases databases, applications, software, or common practices associated with USGS WMA or within the USGS WMA portfolio.

# Submitting an update

1. Fork repo
2. Create a markdown file (.md)
3. Add to `content` folder
4. Include static images in `static\name-of-post`. Images *must* include alt and title text
5. Add a header similar to:

  ```
  ---
  author: Laura DeCicco
  date: 2016-06-16
  slug: plotFlowConc
  draft: True
  type: post
  title: EGRET plotFlowConc using ggplot2
  categories: Data Science
  tags:
    - EGRET
    - R
  image: static/plotFlowConc/unnamed-chunk-4-1.png
  description: Using the R packages, ggplot and EGRET, a new function plotFlowConc        shows a new way to visualize the changes between flow and concentration.
  keywords:
    - EGRET
    - ggplot2
    - data visualization
  author_twitter: DeCiccoDonk
  author_github: ldecicco-usgs
  author_gs: jXd0feEAAAAJ
  author_staff: laura-decicco
  author_email: <ldecicco@usgs.gov>
  author_researchgate: Laura_De_Cicco
    ---
  ```

  Important notes about header:

  * Date format has to be "YYYY-MM-DD" for the updates to be organized properly.

  * Initial submission **must** include `draft: True`

  * `slug` slug will be the name of your url after waterdata.usgs.gov/blog/xxx

  * `image` is not required, but will improve the look of the main "update" page. Without an image, a generic USGS image will be included.

  * `categories` is a small list of approved options. The current list is `Data Science`, `Applications`, and `Software Development`. For each category, there is a designated list of people that have the authority to approve posts.

  * `tags` are more specific words, and do not need to be on a pre-approved list, these will show up on the navigation of the post.

  * `description` will go into a "meta" tag that Google and other sites use

  * `keywords` (can be the same as tags), also go in a "meta" tag to be used by Google and others.

  * It's a good idea to direct people to github issues, emails, or other ways to communicate if they have questions/comments/etc.

  * You can also add single author attributes for the following: twitter handles (`author_twitter`), github (`author_github`), Google Scholor (`author_gs`), ResearchGate (`author_researchgate`), USGS staff profile (`author_staff`), and email (`author_email`)

6. Submit a pull request
7. Wait for the pull request to get merged (wdfn-updates maintainers will do that), it will then appear on the dev site.
8. Submitter is responsible for getting 1 internal peer-review of content (interal reviews can be done on a Google Form). Send the reviewer a link to the dev site.
9. A designated approver must sign off on content based on review response
10. A designated web content manager will sign-off on if the page is generally fit to be published on a government website (verify the header follows the "Important notes" above, images contain alt/title tags)
11. Once the content is approved, the draft status can be removed, and the content will appear on the QA site.
12. Assuming all looks good, push to prod


# Build and develop with Docker

A Dockerfile and Docker Compose configuration is provided that is capable of running a development server and building the deployable static site.

## Local development

Using `docker-compose`, you may run a development server on http://localhost:1313:

```bash
docker-compose up
```

The default server instance will include draft articles.

## Build static site

Using `docker-compose`, the site may be built using the `build` command provided by the container:

```bash
docker-compose run hugo build
```

The base URL is specified with the `HUGO_BASEURL` environment variable:

```bash
docker-compose run -e HUGO_BASEURL=http://dev-owi.usgs.gov/blog/ hugo build
```

Additional arguments may be passed to the [**Hugo**](https://gohugo.io/) binary as the last argument:

```bash
docker-compose run hugo build --buildDrafts
```

## Debugging the container

If the need arises, you may run arbitrary commands in the container, such as a bash shell:

```bash
docker-compose run hugo bash -l
```

# Instructions for R users

[**Templates for R markdowns**](https://github.com/USGS-R/USGSmarkdowntemplates)

```r
install.packages("USGSmarkdowntemplates", repos=c("https://owi.usgs.gov/R",getOption("repos")))
```

This will add `draft: True` to the markdown header (not rmarkdown file). It is up to you to remove that AFTER the content has been reviewed.

To add 2 figures side by side, add `class="sideBySide"`, for example:

```html
<img class="sideBySide" src='/fig1.png'/ alt='/ggplot2'/>
<img class="sideBySide" src='/fig2.png'/ alt='/EGRET'/>
```



Disclaimer
----------
This software is preliminary or provisional and is subject to revision. It is being provided to meet the need for timely best science. The software has not received final approval by the U.S. Geological Survey (USGS). No warranty, expressed or implied, is made by the USGS or the U.S. Government as to the functionality of the software and related material nor shall the fact of release constitute any such warranty. The software is provided on the condition that neither the USGS nor the U.S. Government shall be held liable for any damages resulting from the authorized or unauthorized use of the software.
