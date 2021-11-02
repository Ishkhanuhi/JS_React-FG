# Server Side Rendering in React

SSR or server-side rendering is the ability of a web application to render the web page  
on the server instead of rendering it in the browser.

## How does the SSR works?

Whenever you visit a website, your browser makes a request to the server that contains the contents of the website.  
The request usually only takes a few milliseconds, but that ultimately depends on a multitude of factors:  
- Your internet speed  
- The location of the server  
- How many users are trying to access the site  
- And how optimized the website is.

Once the request is done processing, your browser gets back the fully rendered HTML and displays it on the screen.  
If you then decide to visit a different page on the website, your browser will once again make another request for the new information.  
This will occur each and every time you visit a page that your browser does not have a cached version of.  

It doesn’t matter if the new page only has a few items that are different than the current page,  
the browser will ask for the entire new page and will re-render everything from the ground up.  

Take for example this `HTML document` that has been placed in an imaginary server with an HTTP address of `example.testsite.com.`
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Example Website</title>
  </head>
  <body>
    <h1>My Website</h1>
    <p>This is an example of my new website</p>
    <a href="http://example.testsite.com/other.html.">Link</a>
  </body>
</html>
```

If you were to type the address of the example website into the URL of your imaginary browser,  
your imaginary browser would make a request to the server being used by that URL and expect a response of some text to render onto the browser.  
In this case, what you would visually see would be the title, the paragraph content and the link.  
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Example Website</title>
  </head>
  <body>
    <h1>My Website</h1>
    <p>This is an example of my new website</p>
    <p>This is some more content from the other.html</p>
  </body>
</html>
```
What would actually happen would be that the entire new page would be rendered, and not just the new content.

While it might not seem like a big deal for these two examples, most websites are not this simple.  
Modern websites have hundreds of lines of code and are much more complex.  
Now imagine browsing a webpage and having to wait for each and every page to render when navigating the site.  
If you have ever visited a WordPress site, you have seen how slow they can be.  

### Use SSR
- if SEO is your priority, typically when you are building a blog site and you want everyone who searching on google go to your website,  
  then SSR is your choice.
- if your website needs a faster initial loading.  
- if the content of your website doesn't need much user interaction.  

Google indexes JavaScript-based web pages using a two-wave indexing system.  
When Googlebot first encounters your website, it crawls your pages and extracts all of their `HTML`, `CSS` and links, typically within a few hours..
Google then puts the JavaScript content in a queue, rendering it when it has the resources.  
Sometimes that takes days or weeks. During that time, your web pages are not being indexed and, therefore, not being found on Google.  
That’s a lot of traffic you’re missing out on. 

What’s worse, if your JavaScript pages aren’t able to be crawled and indexed properly, Google reads them as a blank screen and ranks it accordingly,  
which can be catastrophic to your website’s SEO health.

### Use CSR
- when SEO is not your priority
- if your site has rich interactions  
- if you are building a web application

### A few more disadvantages about SSR
- Complex caching: configuring your cache is usually more complex on SSR sites than CSR sites.
- Server cost: SSR often needs a bigger and more powerful server to provide high-performance than CSR.
- Higher latency: SSR sites tend to get a high latency if you get lots of traffic at the same time,   
  which delays/slows down the browsing experience for everyone.  
  CSR doesn’t suffer from this nearly as much. Latency is also known as ping rate which is usually measured in ms (milliseconds).

## Universal Rendering
Fortunately, there’s a method called universal rendering, where you can get the best of both worlds,  
the quick and seamless app-like page transitions of client-side rendering + the SEO and blazing fast first-paint of server-side rendering.  

In modern times (2020+) the ideal solution for most use cases is to combine CSR and SSR,  
along with some type of SSG, as this gives you maximum speed, strong security, great SEO, lower server costs, and the best user experience possible.  


## There’s a Better Solution Still: Prerendering
prerender.io scrapes your website on a regular basis using the latest Chrome.  
Then it stores all the rendered HTML pages into a database and gives you an API for that so you can access the rendered HTML for every URL of your website.

The only thing you need to do is to add a proxy that checks the user agent.  
If the user agent is a search engine or some kind of crawler (Facebook, Linkedin, etc.) you just send an API call,  
get the rendered HTML from prerender.io, and return it to the crawler.  
If the user agent is not a crawler you can just return the `index.html` of your SPA so the JS would kick in.

```
const express = require('express');
const secure = require('express-force-https');
const prerender = require('prerender-node'); 

// Load from env vars
const port = process.env.PORT;
const indexHtml = process.env.INDEX_HTML;
const prerenderToken = process.env.PRERENDER_TOKEN;

const app = express();

// Use secure middleware to redirect to https 
app.use(secure);

// Use prerender io middleware 
app.use(prerender.set('prerenderToken', prerenderToken));

// Serve index.html on every url.
app.get('*', (req, res) => {
  res.send(indexHtml);
});

app.listen(port);
```

