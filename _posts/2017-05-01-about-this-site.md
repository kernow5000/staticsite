---
layout: post
title: About this site
description: "Static hosting in S3 buckets"
modified: 2017-04-30
tags: [ aws, s3, serverless ]
---

As I talked about for a little bit in a previous post, this site is hosted on AWS using no webservers, and completely static code. 

*"How does this work?"* I hear you ask..maybe

* I have a domain *shaunb.co.uk*, and the DNS is hosted in Amazon Route 53. This costs around 50c a month for the zone, and a few pennies for lookups monthly.
* I have an S3 bucket which is named *shaunb.co.uk*. I've turned on static site hosting on the bucket and set it to reduced redundancy storage so it's cheaper. 
* I have pointed a DNS CNAME record in my R53 zone, to the AWS resource name of the S3 bucket.

Now when I put any files in the S3 bucket I can serve them directly from *http://shaunb.co.uk*

<figure>
	<img src="/images/inf.png" alt="This site on AWS">
</figure>


I now had to decide what I was going to put up there, so was going to write a static blogging engine in bash scripts or something similar. 
Instead, and having a moment of common sense, I looked around for frameworks that could provide way better functionality. 

I ended up with [jekyll](https://jekyllrb.com/), which is a parsing engine you can use to create blog sites and such specifically for hosting in static environments. 

Then it was just a case of getting a nice looking theme and editing the config accordingly for the site name pretty much.

### Making posts

All posts are plain Markdown text and it's simply a case of writing a new text file, rebuilding the site and pushing it to S3.
I need to iron out the process of building and creating new posts at the moment. 

Currently I am editing the Markdown posts and then running a 
couple of bash scripts to build the site and sync it to the S3 bucket using the AWS command line interface. 

By the way, the AWS diagram in this post were created on the wonderful [draw.io](https://www.draw.io/), it's a wonderful free version of Visio pretty much. 
And it has AWS stencils built in!


