# PerfectTemplateFCGI

[![Perfect logo](http://www.perfect.org/github/Perfect_GH_header_854.jpg)](http://perfect.org/get-involved.html)

[![Perfect logo](http://www.perfect.org/github/Perfect_GH_button_1_Star.jpg)](https://github.com/PerfectlySoft/Perfect)
[![Perfect logo](http://www.perfect.org/github/Perfect_GH_button_2_Git.jpg)](https://gitter.im/PerfectlySoft/Perfect)
[![Perfect logo](http://www.perfect.org/github/Perfect_GH_button_3_twit.jpg)](https://twitter.com/perfectlysoft)
[![Perfect logo](http://www.perfect.org/github/Perfect_GH_button_4_slack.jpg)](http://perfect.ly)


[![Swift 3.0](https://img.shields.io/badge/Swift-3.0-orange.svg?style=flat)](https://developer.apple.com/swift/)
[![Platforms OS X | Linux](https://img.shields.io/badge/Platforms-OS%20X%20%7C%20Linux%20-lightgray.svg?style=flat)](https://developer.apple.com/swift/)
[![License Apache](https://img.shields.io/badge/License-Apache-lightgrey.svg?style=flat)](http://perfect.org/licensing.html)
[![Twitter](https://img.shields.io/badge/Twitter-@PerfectlySoft-blue.svg?style=flat)](http://twitter.com/PerfectlySoft)
[![Join the chat at https://gitter.im/PerfectlySoft/Perfect](https://img.shields.io/badge/Gitter-Join%20Chat-brightgreen.svg)](https://gitter.im/PerfectlySoft/Perfect?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![Slack Status](http://perfect.ly/badge.svg)](http://perfect.ly)

Perfect Empty Starter FastCGI Project

This repository holds a blank Perfect project which can be cloned to serve as a starter for new work. It builds with Swift Package Manager and produces a FastCGI based server executable.

## Issues

We are transitioning to using JIRA for all bugs and support related issues, therefore the GitHub issues has been disabled.

If you find a mistake, bug, or any other helpful suggestion you'd like to make on the docs please head over to [http://jira.perfect.org:8080/servicedesk/customer/portal/1](http://jira.perfect.org:8080/servicedesk/customer/portal/1) and raise it.

A comprehensive list of open issues can be found at [http://jira.perfect.org:8080/projects/ISS/issues](http://jira.perfect.org:8080/projects/ISS/issues)

=====

**The master branch of this project currently compiles with *DEVELOPMENT-SNAPSHOT-2016-06-20-a* released June 20th, 2016 using Swift Package Manager.**

Ensure that you have installed the few dependencies which Perfect requires for your platform:

[Dependencies](https://github.com/PerfectlySoft/Perfect/wiki/Dependencies)

This server can run with any FastCGI enabled webserver over either UNIX socket files or TCP.

## Apache 24
To run with Apache 2.4, build and install the mod_perfect FastCGI module:

[Perfect-FastCGI-Apache2.4](https://github.com/PerfectlySoft/Perfect-FastCGI-Apache2.4)

## NGINX
Instructions for running with NGINX:

[NGINX](https://github.com/PerfectlySoft/Perfect/wiki/NGINX)

## Building & Running

The following will clone and build an empty starter project and launch the server.

```
git clone https://github.com/PerfectlySoft/PerfectTemplateFCGI.git
cd PerfectTemplateFCGI
swift build
.build/debug/PerfectTemplateFCGI
```

You should see the following output:

```
Starting FastCGI server on named pipe /Library/WebServer/VirtualHosts/perfect.fastcgi.sock
```

This means the server is running and waiting for connections.

## Starter Content

The template file contains a very simple "hello, world!" example. Note that you must install mod_perfect or otherwise configure your web server for FastCGI and change the namedPipe path such that it points one level above your server's document root.

```swift
import PerfectLib
import PerfectFastCGI

// Initialize base-level services
PerfectServer.initializeServices()

Routing.Routes["/**"] = {
    req, resp in
    let path = req.path
    resp.appendBody(string: "<html><title>Hello, world!</title><body>Hello, world!</body></html>")
    resp.completed()
}

do {
    // Launch the FastCGI server
    // The path to the sock file must point to a directory one level up from the site's document root.
    // The file must be called "perfect.fastcgi.sock"
    // For example, the following path would suffice for a server whose document root is:
    // /Library/WebServer/VirtualHosts/wwwroot/
    try FastCGIServer().start(namedPipe: "/Library/WebServer/VirtualHosts/perfect.fastcgi.sock")
} catch {
    print("Error thrown: \(error)")
}
```



## Further Information
For more information on the Perfect project, please visit [perfect.org](http://perfect.org).
