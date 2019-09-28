---
ID: 1154
post_title: >
  Dark and Light theme switcher using CSS
  variables and pure JavaScript
author: haxzie
post_excerpt: ""
layout: post
permalink: >
  https://zocada.com/dark-and-light-theme-switcher-using-css-variables-and-pure-javascript/
published: true
post_date: 2019-09-28 08:47:23
---
CSS variables give an exceptional ability to build themes and easy theme switching for websites. Changing color schemes of modern websites becomes much easier using plain CSS and a few lines of JavaScript. Let's take a look at building a simple theme switcher using CSS-variables and pure JavaScript. This approach makes it easier to implement theme switching in any front-end frameworks. We'll also have examples on implementing the theme switcher on React.js and Vue.js.
<h2>Setting up color schemes for Dark and Light themes</h2>
Using CSS variables, we need to create two classes defining all the colors that are being used in our style sheets for two different themes. In our case, we'll create <code>theme-light</code> and <code>theme-dark</code> classes. You can use the same methodology to create any number of color schemes and have not just two but, tons of different themes to be used on your website.
<h4>CSS classes representing the colors</h4>
<pre class="EnlighterJSRAW" data-enlighter-language="css">.theme-light {
  --color-primary: #0060df;
  --color-secondary: #fbfbfe;
  --color-accent: #fd6f53;
  --font-color: #000000;
}

.theme-dark {
  --color-primary: #17ed90;
  --color-secondary: #243133;
  --color-accent: #12cdea;
  --font-color: #ffffff;
}
</pre>
&nbsp;
<label>Note that CSS variables will always start with <code>--</code> in front of their names</label>
&nbsp;
<p>
Let's throw them into a stylesheet file and link it to a sample HTML file.
</p>
<pre class="EnlighterJSRAW" data-enlighter-language="css">
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
}

.theme-light {
  --color-primary: #0060df;
  --color-secondary: #fbfbfe;
  --color-accent: #fd6f53;
  --font-color: #000000;
}

.theme-dark {
  --color-primary: #17ed90;
  --color-secondary: #243133;
  --color-accent: #12cdea;
  --font-color: #ffffff;
}

.container {
  display: flex;
  width: 100%:
  height: 100%;
  background: var(--color-secondary);
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.container h1 {
  color: var(--font-color);
}

.container button {
  color: var(--font-color);
  background: var(--color-primary);
  padding: 10px 20px;
}
</pre>
&nbsp;
<p>And a smaple HTML file to view the example. To set the default theme, set the class of html to the theme name.</p>
<pre class="EnlighterJSRAW" data-enlighter-language="html">
&lt;!DOCTYPE html>
&lt;html lang="en" class="theme-light">
&lt;head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="./styles.css" type="text/css"/>
&lt;/head>
&lt;body>
    <div class="container">
        <h1>Theme Switcher</h1>
        <button id="switch">Switch</button>
    </div>
&lt;/body>
&lt;/html>
</pre>
&nbsp;
We should be able to get something like this.
<img src="https://zocada.com/wp-content/uploads/2019/09/Screenshot_2019-09-28-Document.png" alt="sample switcher" width="761" height="447" class="aligncenter size-full wp-image-1172" />

<h2>Using Javascript to change the theme programmatically</h2>
<p>
There are a few things we need to do to have the ability to change the themes programmatically, and for saving the chosen theme in <code>localstorage</code> so that whenever a user comes back to our website, the website should use the theme previously selected by the user.
</p>

<pre class="EnlighterJSRAW" data-enlighter-language="javascript">
// function to set a given theme/color-scheme
function setTheme(themeName) {
    localStorage.setItem('theme', themeName);
    document.documentElement.className = themeName;
}

// function to toggle between light and dark theme
function toggleTheme() {
    if (localStorage.getItem('theme') === 'theme-dark') {
        setTheme('theme-light');
    } else {
        setTheme('theme-dark');
    }
}

// Immediately invoked function to set the theme on initial load
(function () {
   if (localStorage.getItem('theme') === 'theme-dark') {
      setTheme('theme-dark');
   } else {
      setTheme('theme-light');
   }
})();
</pre>
&nbsp;
<p>
Let's include these javascript functions inside a script tag inside the HTML file, and you will be able to call these functions anywhere in the project by referencing from the <code>window</code> object, no matter what framework you use. For now, let's attach a click-listener to the button to call the <code>toggleTheme()</code> function. The final HTML file with the script should look somewhat like this.
</p>
<pre class="EnlighterJSRAW" data-enlighter-language="javascript">
&lt;!DOCTYPE html>
&lt;html lang="en" class="theme-light">

&lt;head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="./styles.css" type="text/css" />
&lt;/head>

&lt;body>
    <div class="container">
        <h1>Theme Switcher</h1>
        <button id="switch" onclick="toggleTheme()">Switch</button>
    </div>
    <script>
        // function to set a given theme/color-scheme
        function setTheme(themeName) {
            localStorage.setItem('theme', themeName);
            document.documentElement.className = themeName;
        }

        // function to toggle between light and dark theme
        function toggleTheme() {
            if (localStorage.getItem('theme') === 'theme-dark') {
                setTheme('theme-light');
            } else {
                setTheme('theme-dark');
            }
        }

        // Immediately invoked function to set the theme on initial load
        (function () {
            if (localStorage.getItem('theme') === 'theme-dark') {
                setTheme('theme-dark');
            } else {
                setTheme('theme-light');
            }
        })();
    </script>
&lt;/body>

&lt;/html>
</pre>
&nbsp;
<h2>Result? Welcome to the Dark Side!</h2>
<img src="https://zocada.com/wp-content/uploads/2019/09/theme-switcher.gif" alt="" width="900" height="429" class="aligncenter size-full wp-image-1179" />