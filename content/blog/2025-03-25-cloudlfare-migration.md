+++
title = 'Migrating from Github Pages to Cloudflare'
date = 2024-03-25
draft = false
+++

Considering the trials and tribulations I went through configuring my [github pages](https://pages.github.com/) site,
I was expecting the move to [cloudflare pages](https://pages.cloudflare.com/) to be equally difficult and time-consuming.
However, I'm happy to report that this was actually a very simple switch over for me. 

As this new site is a rewrite from scratch of my [previous site](https://aaronrdodd.github.io/github-pages-website), I took the liberty to
change the tech stack as well as the deployment platform and infrastructure.

## The code

Originally I was using Astro.js for my static site generation, but with the new site I chose Hugo instead. The main reasons for
the switch is that I wanted to ensure that the site was being rendered statically, and with astro moving more and more focus into
server-side rendering and cloudflare pages also supporting workers I felt like it was safer to go with something which I knew could
only give me a static site.

As I'm not a front-end development wizard I decided to pick [missing.css](https://missing.style) for my styling framework and I've
created a couple of helpers using the hugo templating language which I'm sure I will add to over the coming days.

Once I was happy with an initial look of the site I pushed the code to a github repository so that I could connect it with cloudflare
pages.

## Deploying

To host on cloudflare pages I needed to:

1. Create a new pages deployment
2. Link my github and cloudflare accounts so that cloudflare can access the repository
3. Configure the default build framework to Hugo
4. Use the `hugo --baseURL $CF_PAGES_URL` build command to make sure that the baseURL referenced by hugo is up to date
5. Add a DNS CNAME record to point from my apex domain to the `pages.dev` subdomain given to me by cloudflare

All of this was very streamlined by the magical cloudflare wizard. I noticed that by default cloudflare DNS points to your apex domain rather
than `www`, so I spent some additional time configuring a redirect rule to route from `www.mydomain` to `mydomain`.
