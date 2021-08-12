# Udemy Clone - Proxy

![Sidebar on page load](/readme_assets/sidebar_on_page_load.png)

## Table of Contents

1. [Overview](#overview)
2. [Installation](#installation-and-start)

## Overview

### Background

This is a reverse proxy for a Udemy clone. It is part of a group project on service-oriented architecture; you can find the other relevant repositories at https://github.com/Charlotte-Badger. The proxy includes the navbar at the top of the page and the other static elements at the bottom of the page, and manages the location and some aspects of the appearance of the Overview, Sidebar, Course Content, Reviews, and Instructor services. This includes handling a variety of screen sizes via media queries, and the animation and some elemnts of the scrolling behavior of Sidebar. I attempted to match the appearance of the real Udemy website as closely as possible, including the somewhat abrupt-feeling resizing at width 1180 and a few other things that one might otherwise have been tempted to change. Logos and some SVG elements were borrowed directly from the true Udemy website (and in the case of logos, hosted in my S3). But in general I tried to re-create rather than copy as much as possible.

### Technologies

* React
* Node.js
* Express
* AWS S3
* AWS EC2

### Highlights

* Works with Sidebar to handle relatively complex behaviors on scroll
  * Starts positioned at top of page in line with other elements
  * Joins fixed overview bar as user scrolls down
  * Attaches to other content behind fixed overview bar as user reaches the end of the page

![Sidebar top transition on scroll](/readme_assets/sidebar_top_transition.gif)
![Sidebar bottom transition on scroll](/readme_assets/sidebar_bottom_transition.gif)

* Handles many media queries, including changing the width and margins of most elements at 1180px, hiding the sidebar at 1080px, and adjusting which navigation elements are visible as the screen gets smaller (before changing to a mobile-friendly menu at 800px)

![Proxy handling media queries](/readme_assets/proxy-media-queries.gif)

## Installation and Start

1. From root directory: `npm install`.
2. Create file named `.env`, using the template provided at `.env-sample`.
   * NODE_ENV defaults to "development"; "production" is the other possible choice (which will tell Webpack to build a more efficent client, at the expense of some helpful development features).
   * PRIVATE_HOST should either be set to `localhost` or (if deployed to EC2) your EC2 private host URL.
3. index.html pulls scripts for the various services from S3 instances; in the likely case some or all of those aren't working at the time you're trying to run this, you'll need to change those to your own local or hosted copies of those scripts (which themselves will need to refer to your own local or hosted copies of the relevant databases).
4. Proxy.jsx assumes my S3 will be up with copies of the primary Udemy logos available; I've included those files under client/assets just in case.
5. Build the client with `npm run build` or (if you want to put in in watch mode) `npm run dev`.
6. Start the server with `npm start`.
7. Open your browser and navigate to localhost:6012 (or whatever URL and port you specified in `.env`).
8. Add `?courseId=` and then a number between 1 and 100, inclusive, to see it render with information from the different records in the various service databases.