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

### Use CSR
- when SEO is not your priority
- if your site has rich interactions  
- if you are building a web application
