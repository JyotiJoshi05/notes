# IIS((Internet Information Services) WebServer Notes

- IIS is a web server that runs on the Microsoft .NET platform on the Windows OS.

```
A web server is a process for hosting web applications. The web server allows an application to process messages that arrive through specific TCP ports (by default). For example, the default port for HTTP traffic is 80, and the one for HTTPS is 443.

When you visit a website in your browser, you don’t typically specify the port number unless the web server is configured to receive traffic on ports other than the default. Visiting http://www.example.com will send your request to port 80 implicitly. You could specify the port number if you’d like http://www.example.com:80, and https://www.example.com:443 for TLS (Transport Layer Security).
```
## How does IIS handle web requests?
The two main process models for web servers are to either handle all requests on a single thread, or to spawn a new thread for each request. Although the single-thread model (Node.js, for example) has some worker threads available, it typically only uses them for certain kinds of work, such as file system access. The thread-per-request model that IIS (and its lightweight cousin IIS Express) uses will grab a thread from a thread pool for each request.

- Windows NT is a family of operating systems produced by Microsoft, the first version of which was released on July 27, 1993. It is a processor-independent, multiprocessing and multi-user operating system.

The main job of a web server is to display the website content. If a web server is not exposed to the public and is used internally, then it is called Intranet Server. When anyone requests for a website by adding the URL or web address on a web browser’s (like Chrome or Firefox) address bar (like www.economictimes.com), the browser sends a request to the Internet for viewing the corresponding web page for that address. A Domain Name Server (DNS) converts this URL to an IP Address (For example 192.168.216.345), which in turn points to a Web Server. 

The Web Server is requested to present the content website to the user’s browser. All websites on the Internet have a unique identifier in terms of an IP address. This Internet Protocol address is used to communicate between different servers across the Internet. These days, Apache server is the most common web server available in the market. Apache is an open source software that handles almost 70 percent of all websites available today. Most of the web-based applications use Apache as their default Web Server environment. Another web server that is generally available is Internet Information Service (IIS). IIS is owned by Microsoft.