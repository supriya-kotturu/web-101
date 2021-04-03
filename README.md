# web-101

<br>

## Difference between HTTP/1.1 vs HTTP/2

The Hypertext Transfer Protocol, or HTTP, is an application protocol that has been the de facto standard for communication on the World Wide Web since its invention in 1989.

HTTP is a top-level application protocol that exchanges information between a client computer and a local or remote web server. In this process, a client sends a text-based request to a server by calling a method like GET or POST. In response, the server sends a resource like an HTML page back to the client.

| HTTP/1.1                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | HTTP/2                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| HTTP1.x uses text-based commands to complete HTTP requests. If you were to view one of these requests they would be perfectly readable                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | HTTP2, on the other hand, uses binary commands (1s and 0s) to complete HTTP requests. It needs to be converted back from binary to read the request. <br> This conversion to Binary takes place in the Binary Framing Layer, so only binary commands are transmitted over the network.                                                                                                                                                                                                                                                                                                                                            |
| Messages or request data is transfered as frames                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | HTTP/2 introduces an extra step. It divides HTTP/1.x messages into frames, which in turn are embedded in a stream.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| It is ordered and blocked                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | It is fully multiplexed                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| With HTTP/1.x if a user wanted to make multiple parallel requests to improve performance, they would need to use a technique such as **Domain Sharding**. <br><br> This is where a user would use a subdomain (or multiple subdomains) for assets such as images, CSS files, and JavaScript files so that they could make two or three times the number of connections to speed up the download of files. <br> <br> This is further exacerbated by a problem called “**head-of-line blocking**.” This is where a new request can only be made once the results of the first request must have been received. | The new binary framing layer removes these limitations. <br> <br> It allows full request and response multiplexing, by allowing the client and server to break down an HTTP message into independent frames, interleave them, and then reassemble them on the other end. Furthermore, it only uses a single TCP connection to do all this.                                                                                                                                                                                                                                                                                        |
| With HTTP/1.1, this was easy, as head-of-line blocking made it simple to load various assets in the correct order.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | With HTTP/2, however, the response to the browser request may be received back in any order. <br> <br> The new protocol solves this by allowing the browser to communicate with the server and indicate the priorities for the respective objects \ files. <br> <br> No changes will be required by web \ app developers as modern web browsers will take care of prioritization and handling of data streams.                                                                                                                                                                                                                    |
| With HTTP/1.1 a new TCP connection has to be provided for every asset requested, which if you have a page with over 100 requests can be time-consuming                                                                                                                                                                                                                                                                                                                                                                                                                                                       | The new Protocol can send all the headers in a single connection utilizing compression. <br> <br> Due to a significant “CRIME” attack targeting the use of GZIP Stream Compression the HTTP/2 developers had to abandon its use. Instead, they created a new `header-specific compression scheme` called **HPACK** <br><br>HPACK compresses the individual value of each header before it is transferred to the server. It then looks up the encoded information in a list of previously transferred header values to reconstruct the full header information.<br><br>This creates a significant performance benefit over HTTP/1. |

<br><br>

## HTTP version history

- **HTTP 0.9** - Time Berners-Lee released the first documented version of HTTP in 1991.

  It consisted of a single line containing a GET method and the path of the requested document. The response was just as simple, returning a single hypertext document without headers or any other metadata.

- **HTTP 1.0** - Version 1.0 received official recognition in 1996, and coincided with the rapid evolution of the HTML specification, and the “web browser.”

  The main addition was “request headers” and “response headers.” Also, the new response headers allowed multiple file types, such as HTML, plain text, images, and more.

- **HTTP 1.1** - Version 1.1 was released in 1997 and became the Internet Standard. This version added many performance enhancements, such as keepalive connections, caching mechanisms, request pipelining, transfer encodings, and byte range requests.

  This new version was better and removed many of the ambiguities found in HTTP/1.0.

- **HTTP 2.0** - Released in February 2015 by the Internet Engineering Task Force (IETF) focussed on improving the performance of HTTP. This article focuses on the major changes of this version in more detail.

- **HTTP 3** - The new HTTP/3, based on the QUIC protocol, is anticipated to be released in late 2019.
  HTTP/3 is an evolution of the QUIC (Quick UDP Internet Connections) protocol from Google, first suggested by Mark Nottingham in October 2018. HTTP/3 is due to be released in 2019 (hopefully).

  QUIC is similar to TCP+TLS+HTTP2 but is implemented on top of UDP. UDP stands for User Datagram Protocol. UDP is essentially TCP without all the error checking.

  This has many benefits:

  - UDP packets are received by the recipient more quickly.
  - The sender will not have to wait to ensure the packet has been received.

  Because no error checks are made, when the recipient misses packets, they cannot be requested again. As a result, UDP is used when speed is more important than the occasional lossed packet, such as live broadcasts or online gaming.

  - Key features of QUIC:
    - Dramatically reduced connection establishment time
    - Improved congestion control
    - Multiplexing without head-of-line blocking
    - Forward error correction
    - Connection migration

  <br><br>

## Difference between Browser vs Node.js

Both the browser and Node.js use JavaScript as their programming language.

Building apps that run in the browser is a completely different thing than building a Node.js application.

Despite the fact that it's always JavaScript, there are some key differences that make the experience radically different.

| Browser                                                                                                                                                                                                                                                           | Node.js                                                                                                                                        |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| Most of the time what you are doing is interacting with the DOM, or other Web Platform APIs like Cookies.                                                                                                                                                         | You don't have the `document, window` and all the other objects that are provided by the browser.                                              |
| We don't have all the nice APIs that Node.js provides through its modules, like the filesystem access functionality.                                                                                                                                              | Gives you access to filesytem                                                                                                                  |
| You don't get the luxury to choose what browser your visitors will use                                                                                                                                                                                            | In Node.js, you control the environment. This means that you can write all the modern ES6-7-8-9 JavaScript that your Node.js version supports. |
| Since JavaScript moves so fast, but browsers can be a bit slow to upgrade, sometimes on the web you are stuck with using older JavaScript / ECMAScript releases. You can use Babel to transform your code to be ES5-compatible before shipping it to the browser. | But in Node.js, you won't need that.                                                                                                           |
| In the browser, we are starting to see the ES Modules standard being implemented. In practice, this means that for the time being you use `require()` in Node.js and `import` in the browser.                                                                         | Node.js uses the CommonJS module system                                                                                                        |

<br><br>

## What happens when you type a URL in the address bar in the browser?

Let’s say you are visiting a website at the domain www.example.com. When you navigate to this URL, the web browser on your computer sends an HTTP request in the form of a text-based message, similar to the one shown here:

`GET /index.html HTTP/1.1` <br>
`Host: www.example.com`

This request uses the `GET` method, which asks for data from the host server listed after `Host:`.

In response to this request, the `example.com` web server returns an HTML page to the requesting client, in addition to any images, stylesheets, or other resources called for in the HTML.

- Note that not all of the resources are returned to the client in the first call for data.
- The requests and responses will go back and forth between the server and client until the web browser has received all the resources necessary to render the contents of the HTML page on your screen.

You can think of this exchange of requests and responses as a single application layer of the internet protocol stack, sitting on top of the transfer layer (usually using the Transmission Control Protocol, or TCP) and networking layers (using the Internet Protocol, or IP)
