---
title: Servlets and JSP
author: Vishnu Rajeev
date: 2020-08-11
hero: ./images/servlets_and_jsp.jpg
slug: servlets-and-jsp
excerpt: A brief introduction to servlets and JSP
---

# What is a servlet?

Servlet is a Java program that runs on the web server. It is used for building dynamic web pages.

# Servlet execution

![Servlet execution](./images/servlet_execution.png)

Servlet execution consists of the following steps:

- The client sends a request to the web server.
- The web server receives the request.
- The web server gives the request to the corresponding servlet.
- Servlet processes the request and generates the response.
- Servlet sends the response back to the web server.
- The web server sends the response back to the client and the client browser displays it on the screen.

# Servlet example

The following example shows a simple servlet that outputs text.

```
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class ServletTemplate extends HttpServlet {
 public void doGet(HttpServletRequest request,
                   HttpServletResponse response)
     throws ServletException, IOException {

   PrintWriter out = response.getWriter();
   out.println("Hello World");
 }
}
```

This servlet handles GET requests. A browser generates this request when the user enters a URL on the address bar, follows a link from a web page, or submits an HTML form that specifies METHOD=”GET” or doesn’t specify a METHOD. Servlets can also handle POST requests, which are generated when someone submits an HTML form that specifies METHOD=”POST”.

Servlets extend HttpServlet and override doGet or doPost, depending on whether the data is being sent by GET or by POST. Both doGet and doPost take two arguments: an HttpServletRequest and an HttpServletResponse. HttpServletRequest lets you get all of the incoming data and HttpServletResponse lets you specify outgoing information.

# Servlet Lifecycle

The servlet life cycle contains five phases:

1. **Load a servlet class:** The servlet is loaded when the first request for the servlet is received by the web container.

2. **Servlet instance is created:** At the time the servlet is loaded, the server creates a single instance. That single instance handles every request made to the servlet.

3. **init() method:** init() method is called after creating the servlet instance. It is used to initialize the servlet. init() is guaranteed to be called and completed before the servlet handles its first request.

4. **service() method:** service() method is called whenever a request for a servlet is received. service() method is used to handle requests for the servlet. The service() method accepts 2 parameters: a request object and a response object.

5. **destroy() method:** The servlet calls the destroy() method after the servlet has been taken out of service and all pending requests have completed or timed out.

# What is JSP?

JSP stands for JavaServer Pages. JSP is mainly used for implementing the GUI part of an application. Like servlets, JSP is also used to create dynamic web pages. The difference between them is that the servlet is used to implement business logic whereas JSP is used for creating the presentation. In servlets, we write HTML code inside Java while in JSP we write Java code inside HTML. JSP is an extension of servlets and every JSP page first gets converted into a servlet by JSP container before processing the client’s request.

# Advantages of JSP over Servlet

There are many advantages of JSP over servlets. They are as follows:

1. **More features:** JSP technology is the extension of servlet technology. We can use all the features of the servlet in JSP. Also, we can use implicit objects, predefined tags, expression language, and custom tags in JSP, which makes JSP development easy.

2. **Maintenance is easier:** JSP can be easily managed because we can easily separate our business logic with presentation logic. In servlet technology, we mix our business logic with the presentation logic.

3. **Faster development:** No need to recompile and redeploy. If the JSP page is modified, we don’t need to recompile and redeploy the project. The servlet code needs to be updated and recompiled if we have to change the look and feel of the application.

4. **Less code:** In JSP, we can use many tags such as action tags, JSTL, custom tags, etc. that reduce the code. Also, we can use Expression Language, implicit objects, etc.

# JSP Example

The following example shows a simple JSP that displays Hello World.

```
<html>
  <head>
    <title>JSP Example</title>
  </head>
  <body>
    <% out.print("Hello World"); %>
  </body>
</html>
```

This JSP contains HTML tags and also a scriptlet. Scriptlet is a JSP element that contains the Java code. Syntax of scriptlet is: <% executable Java code %>. out.print(“Hello World”) is a Java statement that prints “Hello World”.

Combined with servlets, JSP pages are very powerful and provide access to a wide range of Java capabilities.
