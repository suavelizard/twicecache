# Twice #

_Twice is a proxy server that uses caching and partial rendering to reduce load on application servers._

## Features at a Glance: ##

  * In-memory cache
  * Basic templating language to render dynmaic page elements
  * Intelligent reverse proxy (Squid-like functionality)
  * HTTP header and cookie inspection
  * Written in Python using the Twisted event framework

## Detailed Overview: ##

Twice is a caching reverse-proxy webserver with a templating language and plugable page element rendering engine.  You can configure Twice on a per page basis by adding extra HTTP headers to your application server's responses.

It is best to run Twice behind a hardened web server (like Apache, Lighttpd, or Nginx).  These programs are better suited to serve static content like images and css files.  Other requests hit Twice, which serves cached responses when it can.  If Twice can't serve a page, it will proxy the request through to the application server(s) and intelligently cache the response.

## Case Study: ##

At Justin.tv we use Twice to serve the majority of dynamic page views (up to 25 million pages per day).  Here are some of the things it does:

  * Temporarily caches pages that update frequently
  * Renders cached pages in foreign languages by inspecting HTTP headers
  * Renders usernames at the top of every page by inspecting browser cookies
  * Renders page view counts into cached pages on demand by reading memcached keys

Twice cut our peak application server load by 78% and reduced our average page load time by 50% overnight.