---
layout: post
title:      "HTML Fundamentals "
date:       2020-01-04 21:22:51 -0500
permalink:  html_fundamentals
---

**Intro to HTML**

HTML which stands for (Hypertext Markup Language) basically makes up the structure of web content. It is not a programming language like ruby or javascript because it can not process logic like programming languages can. For example you can not implement an if else conditonal block in HTML. HTML is strictly just a markup language. An HTML document is made up of tags or markup elements that wrap it's content. These usually consist of an opening and closing tag, though some tags are self closing. A tag that defines the document called the doctype declaration tag is needed at the top of the document to tell the web browser the type of HTML being used. The HTML tag is used to tell the browser that everything being coded in between these tags is HTML code. Two other tags needed for your HTML document are the head tag and the body tag. The head tags contain the metadata between it which is data about the HTML document itself and it also contains other information for the web browser. The body tags contain the main content between it which usually includes other tags such as headers and paragraph tags. Headers range from h1 to h6 (largest to smallest), they change the way text appears and allow search engines to determine what the web page is about. A title tag is a tag that contains text which is displayed in the upper tab of the web page usually used to describe the page content.



```
<!DOCTYPE html>

<html>
  <head>
	
	<title></title>
		
 </head>
  <body>
		
  </body>
</html>
```
**Attributes**

HTML attributes are used to provide additional information to your elements such as links or properties like width and height. They are implemented with a name="value" in the opening tag of an HTML element, where name is the attribute name and value is the attribute value. 

**Comments**

HTML comments are used as helpful notes in the HTML document. They do not get rendered to the browser with the other code.  `<!-- This is a comment -->`.

**Images and Lists**

Images can be inserted into our web pages using the img tag along with the src attribute `<img src="image-url"  alt="description of image">` , the alt attribute is used to describe the image, it is useful for users with disabilities and for images that have trouble loading. In HTML lists are another common markup element. The types that are usually used are unordered lists and ordered lists. Unordered lists contain list item tags that appear bulleted. Ordered lists contain list item tags that appear numbered.  
```
<!-- Unordered Lists -->
<ul>
 <li></li>
 <li></li>
</ul>
```
```
<!-- Ordered Lists -->
<ol>
 <li></li>
 <li></li>
</ol>
```

**Conclusion**

In summary, HTML is needed to develop for the web as it is a necessary tool to build web pages and web apps. It makes up the structure  of our websites.

![](https://intellipaat.com/mediaFiles/2015/02/html-fundamentals.jpg)

*Sources for blog:*
https://learn.co/tracks/full-stack-web-development-v8/module-4-introduction-to-html-and-css/section-2-html-basics/html-introduction
https://www.w3schools.com/html/html_basic.asp
https://intellipaat.com/mediaFiles/2015/02/html-fundamentals.jpg

