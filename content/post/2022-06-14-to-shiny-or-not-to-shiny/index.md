---
title: To Shiny or Not to Shiny
author: Grace Acton
date: '2022-06-14'
categories:
  - research
tags:
  - R
  - Rufus Porter
  - summer 2022
publishdate: '2022-06-14T11:19:15-04:00'
comments: yes
---
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />

## That is the question...


**Shiny is one of my favorite R packages.**

For those who aren't R enthusiasts (or those who are but haven't yet been introduced to Shiny), Shiny is an R package that allows you to create interactive applications. With a single script, you can super easily create a UI and server that will take user input and generate graphs, tables, text, and even maps. 

So far, I've mostly used Shiny to level up my `leaflet` game. With Shiny, you can let users filter points and polygons on a `leaflet` map by pretty much any variable in your data set. In my Short Term course, Community Engaged Data Science, we used the interactivity of Shiny to make a Lyme disease dashboard for the Maine Medical Center Vector-Borne Disease Lab. The app lets you choose which polygon overlays you want to see, so you can toggle between potential indicators of Lyme disease outbreaks. 

Shiny is a great tool for upgrading `leaflet` maps and making other interactive apps, but...

**Hosting Shiny apps kind of sucks.**

The only reasonably straightforward way to do it, to the best of my knowledge, is through [shinyapps.io]("https://www.shinyapps.io/). The [shinyapps](https://www.shinyapps.io/) hosting is good in theory, but in practice, it's been incredibly frustrating. Let's look at some pros and cons:

<table class="table" style="font-family: Georgia; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> Pros </th>
   <th style="text-align:left;"> Cons </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;border-right:1px solid;"> Host for free. </td>
   <td style="text-align:left;"> Free version limits you to 1 GB of memory. </td>
  </tr>
  <tr>
   <td style="text-align:left;border-right:1px solid;"> Designed to work with and deploy directly from the RStudio console. </td>
   <td style="text-align:left;"> Figuring out how to deploy for the first time is super confusing. </td>
  </tr>
  <tr>
   <td style="text-align:left;border-right:1px solid;"> Lets you deploy to multiple different accounts. </td>
   <td style="text-align:left;"> If you don't check which account is currently linked, you can deploy to the wrong account without noticing (sorry, Dr. Baker!) </td>
  </tr>
</tbody>
</table>


My main qualm is the limited memory. Here's the aforementioned Lyme disease dashboard:


<div class="figure">
<iframe src="https://laurie-the-student-baker.shinyapps.io/lyme_indicators/?showcase=0" width="75%" height="500px" data-external="1"></iframe>
<p class="caption">Figure 1: Lyme disease Shiny app. Apologies if it doesn't work - guess that's proof that Shiny hosting is super inconsistent.</p>
</div>

This is dramatically pared down from what we intended to include. We had two other diseases that we were looking at (Anaplasmosis and Babesiosis, in case there are any tick scholars present), but adding the polygon layers made it too big to host. We also had passive tick submission data, but, again, couldn't add it to the dashboard because it got too big. I'm still happy with how this turned out, but because we were making this dashboard for researchers rather than the public, I really wanted to include all of the data they gave us, instead of one out of six of their data sets. 

## My current Shiny project

As I talked about in my [last post](https://dressing-up-data.netlify.app/blog/rpm-week-one/), my research project during my time at Rufus Porter is to make an interactive map of the art of the Rufus Porter School. When I last wrote about this project, I was completely fed up with Shiny, and was going to stop using it. But, I have since fixed many issues, and am now back on track with Shiny. 

### A Problem and Solution

When my app wasn't running, I immediately assumed that it was because I was using `leaflet` again and `leaflet` maps get big very quickly. But, it turns out that was not the case! I have been using the `fontAwesome` package to make `awesomeIcons` for my map, and I had forgotten to call `library(fontAwesome)` at the beginning of my app script. It was such a simple solution, but it took forever to figure it out! The package was already loaded in RStudio, so there were no error messages or anything when I ran the app locally. And, because the package was already _installed_, I didn't get an error when I deployed it; I just got an "Application failed to start" message on the `shinyapps` page that was hosting it. This message has like a dozen potential causes, but, luckily, I found [this article](https://support.rstudio.com/hc/en-us/articles/229848967-Why-does-my-app-work-locally-but-not-on-shinyapps-io-) in the `shinyapps` FAQs, and when through each potential cause until I figured it out. So, if you're using Shiny, **make sure you have a `library()` call for every single package you're using**. 

### Preview

So, now that my Shiny map app is successfully deployed, here is a little preview! Right now I'm using the `sidebarPanel` layout with the main panel being a `tabsetPanel`, but I've also been playing around with the fluid grid system that underlies all Shiny layouts. 

This is far from a finished product - there are still a lot of images missing that I know I can find, and the artist information pages are all just quick little drafts I wrote from memory. 

Feel free to let me know what you think in the comments!

<iframe src="https://gkacton.shinyapps.io/art-map/?showcase=0" width="75%" height="500px" data-external="1"></iframe>

