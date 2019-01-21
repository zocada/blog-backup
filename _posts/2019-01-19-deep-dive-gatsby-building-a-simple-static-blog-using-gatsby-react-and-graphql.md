---
ID: 895
post_title: 'Deep dive into Gatsby &#8211; Building a static blog using Gatsby, React and GraphQL'
author: haxzie
post_excerpt: >
  Gatsby.js is one of the most exciting
  technologies happened in this decade.
  Building lightning fast websites have
  never been easier before. Gatsby
  combines the flexibility of React and
  benefits of GraphQL to build static
  websites. Not to confuse with what
  Gatsby does, the description provided in
  the website gives a clear idea on what
  Gatsby is.
layout: post
permalink: >
  https://zocada.com/deep-dive-gatsby-building-a-simple-static-blog-using-gatsby-react-and-graphql/
published: true
post_date: 2019-01-19 18:54:38
---
Gatsby.js is one of the most exciting technologies happened in this decade. Building lightning fast websites have never been easier before. Gatsby combines the flexibility of React and benefits of GraphQL to build static websites. Not to confuse with what Gatsby does, the description provided in the website gives a clear idea on what Gatsby is.

<!-- GATSBY QUOTE -->
<blockquote>Gatsby.js is a static PWA (Progressive Web App) generator. You get code and data splitting out-of-the-box. Gatsby loads only the critical HTML, CSS, data, and JavaScript so your site loads as fast as possible. Once loaded, Gatsby prefetches resources for other pages so clicking around the site feels incredibly fast.</blockquote>
<em>Official <a href="https://www.gatsbyjs.org/">Gatsby website</a>.</em>

<!-- GETTING STARTED -->

<!-- ================================================================= -->
<h2>Getting Started</h2>
<p>Gatsby provides an amazing CLI to kickstart any Gatsby project easily. Most of this tutorial is concentrated on Linux/Mac machines. You are good to go if you are using Windows with the latest version of Node.js and NPM installed. If you don't have both installed checkout our articles on how to install Node.js and npm on <a href="https://zocada.com/installing-node-js-in-ubuntu-and-other-linux-distros/" target="_blank" rel="noopener">Linux/mac</a> Systems and <a href="https://zocada.com/installing-node-js-in-windows-10-and-below/" target="_blank" rel="noopener">Windows</a></p>

<h2>Step 1. Installing Gatsby-CLI</h2>
<p><a href="https://www.gatsbyjs.org/docs/gatsby-cli/" target="_blank" rel="noopener">Gatsby CLI</a> is a simple tool that helps us to use Gatsby starter templates. Here we'll be using a simple starter template with bare basic boilerplate. Fire up a terminal and execute the following command to install Gatsby-CLI using npm</p>
<pre class="EnlighterJSRAW" data-enlighter-language="shell">npm install -g gatsby-cli</pre>
<p>This will quickly install Gatsby-CLI on your system. Next we'll jump into using a starter template to build up our blog.</p>
<p>Note: All the code used in this article and the sample project created is available in our <a href="https://github.com/zocada/gatsby-blog-tutorial-1" target="_blank" rel="noopener">GitHub repo</a>. Head over there to have a sneak peek on how things should look if you get lost anywhere between the instructions below.</p>

<!-- ================================================================= -->
<h2>Step 2. Creating a new project with a starter</h2>
Once you are ready with Gatsby CLI, we can head on to creating your first Gatsby project. Navigate your terminal into your desired directory and execute the following command.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">gatsby new my-blog</pre>
<img class="aligncenter size-full wp-image-936" src="https://zocada.com/wp-content/uploads/2019/01/Screenshot-from-2019-01-18-21-02-49.png" alt="" width="802" height="508" />

This will clone the <a href="https://www.gatsbyjs.org/starters/gatsbyjs/gatsby-starter-default/" target="_blank" rel="noopener">Gatsby-Starter-Default</a> and execute an <code>npm install</code> to install all the dependencies and plugins.

<!-- ================================================================= -->
<h2>Step 3. Starting gatsby Dev Server</h2>
<code>cd</code> into the project folder and open up your favorite editor (Obviously, VSCODE ❤). Fire up a terminal and run <code>gatsby develop</code> inside the project directory to start the dev server.

<img class="aligncenter size-full wp-image-938" src="https://zocada.com/wp-content/uploads/2019/01/Screenshot-from-2019-01-18-23-03-42.png" alt="" width="1024" height="666" />

Once the server is up, you can visit <code>localhost:8000</code> in your browser to see a delightful Gatsby landing page.

<img class="aligncenter size-full wp-image-939" src="https://zocada.com/wp-content/uploads/2019/01/Screenshot-from-2019-01-18-22-40-19.png" alt="" width="1098" height="709" />

Awesome! you have successfully finished the basic steps! now, let's get into coding!

<!-- ================================================================= -->
<h2>Step 3. Understanding the project structure.</h2>
Under the hood, Gatsby projects are react applications. Well, it's a complete react application, the only part Gatsby comes in is to build the site by executing all the graphql queries, optimizing images, importing necessary data from sources and breaking down the site into static contents using technologies like webpack. If you have a background in developing with React, the current project structure might seem familiar.
<pre>my-blog/
│
├── node_modules/
│   └── [You don't wanna get in here]
│
├── public/
│   ├── [Your site's static contents]
│   └── [Automatically generated by gatsby]
│
├── src/
|   ├── components/
│   │   ├── [These are the building blocks of your website]
│   │   └── [All your react components]
│   │
│   ├── images/
│   │
│   └── pages/
│       ├── 404.js [Your site's 404 page]
│       ├── index.js [the front/first page of your site]
│       └── page-2.js [yet another page]
│
├── gatsby-browser.js
├── gatsby-config.js
├── gatsby-node.js
├── gatsby-ssr.js
├── package.json
├── package-lock.json
└── LICENSE

</pre>
<p>Let's take a close look at what these files and directories are..</p>
<style>
.dir { 
font-weight: bold;
color: #663399;
}
.file {
color: #00cc66;
font-weight: bold;
}
</style>
<p><span class="dir">node_modules/ : </span>This directory contains all of the modules of code that your project depends on (npm packages) are automatically installed.</p>

<p><span class="dir">public/ : </span> Contains automatically generated static build of your site. This is automatically done by Gatsby on issue of the command <code>gatsby build</code> or <code>gatsby develop</code></p>

<p><span class="dir">src/ : </span> This directory will contain all of the code related to what you will see on the front-end of your site (what you see in the browser) such as your site header or a page template. src is a convention for “source code”.</p>

<p><span class="dir">src/components/ : </span> This sub-directory will contain all the components you require as the building blocks of react application.</p>

<p><span class="dir">src/pages/</span> Gatsby treats this directory differently, any Javascript files added as a react component in this directory will be treated as a page of your website. You can simply navigate to each of these pages from your browser without the file extension. eg. <code>localhost:8000/404</code> or <code>localhost:8000/page-2</code>, where as the <code>index.js</code> will be treated as your default landing page.</p>

<p><span class="file">gatsby-browser.js : </span>This file is where Gatsby expects to find any usage of the <a href="https://www.gatsbyjs.org/docs/browser-apis/" rel="noopener" target="_blank">Gatsby browser APIs (if any)</a>. These allow customization/extension of default Gatsby settings affecting the browser.</p>

<p><span class="file">gatsby-node.js : </span> This file is where Gatsby expects to find any usage of the Gatsby Node APIs (if any). These allow customization/extension of default Gatsby settings affecting pieces of the site build process.</p>

<p><span class="file">gatsby-ssr.js : </span> This file is where Gatsby expects to find any usage of the Gatsby server-side rendering APIs (if any). These allow customization of default Gatsby settings affecting server-side rendering.</p>

<p><span class="file">gatsby-config.js : </span> This is the main configuration file for a Gatsby site. This is where you can specify information about your site (metadata) like the site title and description, which Gatsby plugins you’d like to include, etc. (Check out the <a href="https://www.gatsbyjs.org/docs/gatsby-config/" rel="noopener" target="_blank">config docs</a> for more detail).</p>

<!-- ================ AD ==================== -->
<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="ca-pub-7556700931518738"
     data-ad-slot="2974167105"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>

<!-- ================================================================= -->
<h2>Step 4. Installing necessary Plugins</h2>
<p>
Gatsby is all about JAM Stack, if you are new to the concept:
<blockquote>
<b>JAMstack</b>: <i>noun \’jam-stak’\</i>
Modern web development architecture based on client-side JavaScript, reusable APIs, and prebuilt Markup.
</blockquote>

Here, we'll be using markdown to write our blogs and GraphQL to query our markdown files (just like an API) and display the data using React. So, we need a few of the Gatsby plugins to get started with writing blogs in markdown and querying them using GraphQL. Execute the following command inside your project directory to install the necessary plugins.
</p>
<pre>
npm install --save gatsby-source-filesystem gatsby-transformer-remark gatsby-remark-images
</pre>
<h3>Applying your plugins</h3>
<p>We need to specify to Gatsby on which plugins we are using so that Gatsby can use them to integrate to our project's workflow. Add the following lines into your <code>gatsby-config.js</code> file to enable the plugins. Before doing this we need to create a directory to store all our posts, which will be written in markdown. So, create a new subdirectory inside the <code>src/</code> directory as <code>posts</code>. Your directory structure should look somewhat like this now.</p>
<pre>
.
.
.
├── src/
|   ├── components/
│   ├── pages/
│   ├── posts/  <-- The directory you need to create
│   └── images/
│   
.
.
</pre>
<p>Now apply the plugins in <code>gatsby-config.js</code> so as your file should look like this.</p>
<script src="https://gist.github.com/haxzie/180e9ff37baca50193cd96e282e6b082.js"></script>
<p>We are creating our blog posts and querying them as markdown files. Gatsby uses the Remark library to achieve this. Since we already installed the plugin, we can write down our blog posts in markdown files and put them inside the <code>posts</code> directory. A sample post will look similar to this.</p>
<pre>
---
slug: /my-first-blog-post
date: 2018-10-27
author: Jhone Doe
title: My first blog post on gatsby
---

The contents of your blog in either markdown or html.
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
</pre>
<p>You might be wondering what the <code>---</code> dashes are? The part enclosed with dashes are called as the frontmatter of your file. It's commonly used in Jekyll as a handy way to store additional data in the markdown. The data inside the markdown is written in YAML format. You can learn more about the YAML syntax in <a href="https://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html" rel="noopener" target="_blank">here</a>. Note that, the <code>slug</code> in your frontmatter is the relative url of your blog in your website. That is, where your blog post will be visible.</p>
<p>Create a couple of blog posts in the <code>src/posts/</code> subdirectory so that we can start working on creating the home page of our website which lists all the blog posts. </p>
<pre>
.
.
.
├── src/
|   ├── components/
│   ├── pages/
│   ├── posts/ 
│   │   ├── my_first_blog.md
│   │   ├── my_second_blog.md
│   │   └── my_third_blog.md
│   └── images/
│   
.
.
</pre>

<!-- ====================================================== -->
<h2>Step 5. Using GraphQL to fetch data and display on home page</h2>
<p>Gatsby provides out of the box support for using GaraphQL and comes with a built-in GraphiQL IDE. If you have ran <code>gatsby develop</code> on your terminal, You'll might have seen gatsby printing out an additional URL to to the Graphiql as <code>localhost:8000/___graphql</code>. Let's create a graphQL query to fetch the title of the blog posts to display them in the home page. Hop into the GraphQL editor at <code>localhost:8000/___graphql</code> from your browser and execute the following query to get the JSON data of all the posts.</p>
<pre>
query postsQuery {
    allMarkdownRemark (
        sort: { fields: [frontmatter___date], order: DESC } 
    ) {
        edges {
          node {
            frontmatter {
              slug
              title
            }
          }
        }
    }
}
</pre>
<img src="https://zocada.com/wp-content/uploads/2019/01/Screenshot_2019-01-19-GraphiQL.png" alt="" width="1025" height="501" class="aligncenter size-full wp-image-970" />
<p> We won't be going in much depth into GraphQL in this post, but for the record: The <code>edges</code> means, we are letting graphQL know that we are looking for an array, and the <code>node</code> mentioning how each element should look like. The contents inside the <code>node</code> is pretty much staright forward on mentioning what we are querying from the markdown files.</p>
<p>You can change the <code>src/pages/index.js</code> to look like this to use graphQL to fetch data and pass them into a React component.</p>
<script src="https://gist.github.com/haxzie/8f34c2891425e0b7c5d8f2f8b6fde1f9.js"></script>
<p>Once you have made the above changes by removing un-necassry elements from your <code>src/pages/index.js</code> file and added the GraphQL query. Restart the dev server. You'll be able to see your website on the browser now listing all the blogposts you have created.</p>
<img src="https://zocada.com/wp-content/uploads/2019/01/Screenshot_2019-01-19-Screenshot.png" alt="" width="1241" height="612" class="aligncenter size-full wp-image-973" />

<p>All the links will render a 404 error page since we haven't created any page to display the content of our blog post yet.</p>


<!-- ================ AD ==================== -->
<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="ca-pub-7556700931518738"
     data-ad-slot="2974167105"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>
<!-- ===================================================================== -->
<h2>Step 6. Creating template to display blog posts</h2>
<p>In this step, we'll create a simple template to render the contents of our blog post into a template and view them on the slug url specified. So, let's start by creating a new sub-directory inside <code>src/</code> as <code>src/templates/</code>. Create a new file named as <code>blog_template.js</code> and add the following lines of code. Which includes a simple react component and a GraphQL query to fetch data from a specific url supplied by gatsby.</p>
<script src="https://gist.github.com/haxzie/97b116ba9a8730cfd3dd22899aef1437.js"></script>

<h2>Step 7. Using Gatsby's Node APIs to generate Pages</h2>
<p>We need to interact with the Gatsby's Node APIs to tell Gatsby to use all the markdown files and generate the pages using the template we created above. Open the <code>gatsby-node.js</code> file and add the following code to complete building of your simple blog using Gatsby.</p>
<script src="https://gist.github.com/haxzie/e0da6c695454dd8f22c2d938cf7e3b53.js"></script>
<p>In here, we are using the Gatsby's <a href="https://www.gatsbyjs.org/docs/node-apis/#createPages" rel="noopener" target="_blank">createPages()</a> node API to tell Gatsby to execute a query to find all markdown files and using the template, create pages at the slug provided in the frontmatter of the file.</p>
<p>Restart the Gatsby dev server and goto <code>localhost:8000</code> to view your website and click on any of the blog links to view your live blog posts. Yaaaay!</p>
<img src="https://zocada.com/wp-content/uploads/2019/01/Screenshot_2019-01-19-Screenshot1.png" alt="" width="1241" height="612" class="aligncenter size-full wp-image-974" />

<p>We'll look more into How we can add cover images and style our static blog in an upcoming post. Till then, Cheers!</p>


<!-- ================ AD ==================== -->
<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="ca-pub-7556700931518738"
     data-ad-slot="2974167105"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>