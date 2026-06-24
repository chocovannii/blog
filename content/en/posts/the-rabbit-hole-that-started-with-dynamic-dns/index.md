+++
date = '2026-06-24T18:36:56+03:00'
draft = true
title = 'The Rabbit Hole That Started With Dynamic Dns'
+++

# The Rabbit Hole that Started with Dynamic DNS

When I first started hosting a Minecraft server, my friends connected using my public IP address.

It worked, but it wasn't exactly convenient. Nobody wants to memorize a string of numbers every time they join a game.

I started looking for alternatives and quickly discovered Dynamic DNS services. The idea was simple: instead of sharing an IP address, I could use a hostname that automatically updated whenever my ISP changed my public IP.

My router happened to support No-IP integration out of the box. After creating an account, I entered my credentials into the router configuration and forgot about it.

From that point on, the router automatically updated my DNS records whenever my public IP changed. My friends could connect using a hostname instead of an address, and everything worked exactly as intended.

At the time, I considered the problem solved.

I had no idea it would become my introduction to web hosting.

## My First Website

Not long after, I fell down the self-hosting rabbit hole.

Like many people, I started with a simple goal: host a website from home.

It seemed easy enough. Create an `index.html`, add some CSS, install Nginx, and point it to the correct directory.

The website itself took almost no time.

TLS, on the other hand, was a completely different story.

I followed Certbot’s documentation and expected everything to work automatically. Instead, my browser returned an `SSL_RECORD_EXCEEDED_MAX_SIZE` error.

After some digging, I realized the root cause was a misconfigured TLS setup: Nginx was effectively serving plain HTTP on a port expected to speak HTTPS. Fixing the SSL directives resolved the issue.

Seeing the padlock finally appear in the browser was oddly satisfying.

My website was now accessible from anywhere in the world over HTTPS.

If I could host a website, I thought, surely I could host other services too.

## The Reverse Proxy Problem

I started deploying small self-hosted applications: a photo gallery, a music streaming service, and various other projects.

Everything worked well until I tried running several of them simultaneously.

Suddenly I was dealing with routing conflicts, rewrite rules, incorrect redirects, and applications that assumed they were running at the root of a domain.

I eventually got everything working, but each new application required additional configuration and troubleshooting.

The setup was becoming increasingly difficult to maintain.

## Buying a Real Domain

The turning point came when I purchased my own domain name.

Instead of exposing services through different paths on a single hostname, I could assign each application its own subdomain.

The configuration became much simpler.

Applications that struggled behind path-based routing worked without modification, and services such as CryptPad—which require dedicated subdomains—became easy to deploy.

More importantly, I gained a much deeper understanding of how DNS, domains, reverse proxies, and web applications interact.

## Looking Back

What started as a simple attempt to make a Minecraft server easier to join eventually turned into a deep dive into self-hosting infrastructure.

Along the way I learned how Dynamic DNS works, how to configure HTTPS correctly, how reverse proxies route traffic, and why domain structure matters when hosting multiple services.

Today those concepts feel routine, but at the time each problem forced me to understand another layer of how the web actually works.

All because I wanted to avoid sharing a raw IP address.

## Lessons Learned

- DNS can solve usability problems just as effectively as technical ones.
- TLS is easy when it works and educational when it doesn't.
- Hosting a single service is simple; hosting multiple services introduces entirely new challenges.
- Reverse proxies become increasingly important as infrastructure grows.
- Choosing the right domain structure early can significantly simplify future deployments.
