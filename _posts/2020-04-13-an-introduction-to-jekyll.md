---
title: An Introduction to Jekyll
author: Mike Conroy
layout: post
permalink: /2020/04/an-introduction-to-jekyll/
comments: true
categories:
  - Computing
  - Technology
---

[![Jekyll Logo](/assets/images/Jekyll/jekyll.webp){: .centre-image}](https://jekyllrb.com/)

The website you are reading right now has been built by a tool called Jekyll which is used for generating 'static websites' and I have recently migrated to it from Wordpress. This post explains my reasons for moving over and a quick introduction into using Jekyll and break down of project structure.

Firstly, what is a 'static website'? Essentially it means that the website doesn't have any server side code (e.g. PHP) running when delivering pages to a browser. All the client-side files (HTML, JS & CSS) are static and delivered directly to the browser. This offers various advantages which will be discussed further below but it enables you to host the site on [GitHub Pages](https://pages.github.com/), [AWS S3](https://aws.amazon.com/s3/) or your own web server. The key is that you don't need to worry about a server side language/framework/database being setup & maintained. An analogy could be drawn between interpreted & compiled languages when comparing Jekyll sites to PHP/Wordpress - with Jekyll the compilation is done up front as part of a build phase which outputs the final files that can be ran easily whilst PHP would be interpreted each time a request is made to that page.

# Why I have moved over to Jekyll
***

There are 2 main reasons that I have moved the site over to Jekyll one is performance and the other is to learn.
* **Performance** - A major reason was that the old Wordpress site was beginning to feel bloated and slow. After being used for over 7 years various add-ons & extensions had been added which no doubt had an impact on the site. Sure, I could have spent some time debugging and optmising the Wordpress site to bring it back up to speed but PHP & a framework like Wordpress will always be slower than a static website. Wordpress is likely overkill for my needs.
* **Learning** - The second major reason was for my own learning. I wanted to learn and understand a new technology which seems to have gained a lot of traction over the last few years so wanted a better understanding of how it works.

Some other considerations that helped me make this decision are as follows:
* **Flexibility** - Jekyll is much more flexible. Firstly, there is no database (like with Wordpress) so the site files can be dropped in any web server and be served immediately without maintaining a database. Secondly, it is easier to customise Jekyll as it is much closer to editing HTML, CSS & JS unlike Wordpress where you must understand how all the PHP files are interlinked to work out which piece of code should be edited.
* **Familiarity** - I am not familiar with Ruby and its [Gems](https://rubygems.org/) but I am familiar with using [VS Code](https://code.visualstudio.com/), having a local test environment, versioning with Git and writing Markdown, YAML, HTML, JS & CSS. All of which Jekyll makes it easier for me to do.
* **Hosting Costs** - Whilst I'm not currently spending a lot on hosting (£4.19/month with [Unlimited Web Hosting](https://www.unlimitedwebhosting.co.uk/)) I now have the option to reduce this significantly by either moving the site to S3 for a very low cost or on GitHub Pages for free. The performance improvement from Wordpress to Jekyll is also means I  won't need to worry about scaling up or upgrading a server any time soon.
* **PHP** - I have [wrote websites with PHP before](https://github.com/mikecon94/AstonBookStore) and I think that PHP does have it's place and can be used to quickly build 'apps'. However, I also believe PHP codebases devolve into spaghetti code the bigger they get and PHP does have its [problems](https://www.google.com/search?q=php+problems). This means over time it can be hard to read and write PHP codebases. Using Jekyll means I don't have to worry about interacting with PHP :).
* **Security** - Since Jekyll is all client side there isn't much risk with regards to security whereas running PHP & Wordpress extensions could cause many concerns (since this is a personal blog there is less to worry about with regards to security).

There are likely some things I mentioned here that could also be done with Wordpress but from my experience they were not as accessible as they have been with Jekyll. For instance if I wanted a Dev/Test environment to run my Wordpress site I would have had to run PHP on my local machine & a database that was kept in sync. By default, the Jekyll build tool has the option to serve the site locally which I can use as a test environment.

# How to get started with Jekyll
***
The [Quickstart page](https://jekyllrb.com/docs/) on the Jekyll docs make it clear how to get up and running with Jekyll quickly but it essentially boils down to the following steps:
1. Install Ruby.
2. Install Jekyll & Bundler with *gem install jekyll bundler*
3. Create a new site with *jekyll new sitename*
4. In the created directory run *bundle exec jekyll serve* to start running the site locally.

For Windows I opted to use the 'Windows Subsystem for Linux' so I could use a Linux environment. A guide for installing that can be found [here](https://docs.microsoft.com/en-us/windows/wsl/install-win10).

#### Key Commands

Building & Running the site locally -
{% highlight bash %}
bundle exec  jekyll serve --drafts
{% endhighlight %}
The *drafts* flag is optional but will display the site as if the posts in the _drafts folder have been published. This is useful for previewing how your drafts posts will be displayed in the browser without publishing them.

Building the site -
{% highlight bash %}
bundle exec jekyll build
{% endhighlight %}
This will build a *test* instance of your site. This means various features will be disabled such as Google Analytics if used.

In order to do a production build the JEKYLL_ENV variable must be set to production - 
{% highlight bash %}
JEKYLL_ENV=production bundle exec jekyll build
{% endhighlight %}

#### Project Structure

The following are files and folders that are used by Jekyll and what they do. Most of the files & directories can be viewed in the repository for this site on [GitHub](https://github.com/mikecon94/mikeconroy.com).
* **_drafts** - You may have to create this one yourself but it is a place you can write new posts in. They can then be served locally until they are ready to be published at which point move them to the _posts folder.
* **_includes** - This is a folder you will put custom HTML snippets that you want to use in. For instance I have created [image.html](https://github.com/mikecon94/mikeconroy.com/blob/master/_includes/image.html) which allows a post to contain images that can be zoomed into & centered when clicked. For example view the images on the [MuleSoft blog post.]({% link _posts/2015-12-21-an-introduction-to-mulesoft-anypoint-studio.md %})
* **_layouts** - Here is where html templates can be stored that need to be used in multiple locations. For example there is a [post.html](https://github.com/mikecon94/mikeconroy.com/blob/master/_layouts/post.html) layout which is the template for blog post pages (like this one) and outlines how the page should look.
* **_posts** - This is the place that the Markdown files for any published posts go. When Jekyll runs it converts these into the HTML pages following the layouts.
* **_site** - In here are the built website files (HTML, CSS & JS), these are the static files to be served to the browsers. This folder is what will be deployed to the webserver.
* **assets** - The folder for storing images, javascript, css & any other static files that the built site will need to reference.
* **vendor/bundle** - This folder can be ignored mostly as it is a folder that stores the code for the Gems in the project. I used it recently to find out the layout files used in the theme in order to override the defaults. To override defaults of a theme copy the theme's file into your site's corresponding directory. For example, I wanted to change the date format on posts and I use the Minima theme so I went to the path vendor/bundle/gems/minima-2.5.0/_layouts/ and copied the post.html file to the root _layouts/ directory and modified the date format. The commit for this can be found [here](https://github.com/mikecon94/mikeconroy.com/commit/f0a36827137bb627febc8fa4eb33d280a9232334).
* **_config.yml** - This YAML file contains global properties for the website that Jekyll will use in the build and that the theme will use.
* **404.html** - Contains the html & layout details for 404 error pages that get displayed to the user.
* **Gemfile** - Used to manage dependencies of the project. On this site I wanted to ensure that all new links open up in a new tab and used this file to include the [jekyll-target-blank](https://github.com/keithmifsud/jekyll-target-blank) dependency which automatically handles this. It was as simple as adding the line "gem 'jekyll-target-blank'" to the end of the Gemfile and updating the plugins section on '_config.yml'. The commit for this can be found [here](https://github.com/mikecon94/mikeconroy.com/commit/cd839e6ac39168c049b17ffd66581e936babd453).
* **index.md** - This is the Markdown or HTML file for the home page of the website. The file on this site hasn't been modified from the default and just uses the home layout which displays the posts in order of date. If the site was more than a blog then this could be modified as normal into a 'normal' HTML page which linked to a separate blog page containing a link to the posts.

# Conclusion
***
So far I have been happy with the move and enjoying using a development environment and workflow that I am familiar with. I have also enjoyed playing around with Jekyll and customising small pieces such as date formats and the plugins used. The website itself has seen a significant increase in speed compared to when it ran on Wordpress. Moving over to Jekyll has also enabled me to open source the site & automate deployments which will be covered in a future post.
