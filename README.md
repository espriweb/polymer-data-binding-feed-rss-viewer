# Polymer App Toolbox - Starter Kit - Amended as feed reader rss

[![Build Status](https://travis-ci.org/PolymerElements/polymer-starter-kit.svg?branch=master)](https://travis-ci.org/PolymerElements/polymer-starter-kit)

This template is a starting point for building apps using a drawer-based
layout. The layout is provided by `app-layout` elements.

In each view of this template the following block of code to accomplish a file viewer rss was added:

<template is='dom-bind'>
<google-feeds feed='http://www.yourfeedrsspage.com/rss-full.xml' results='{{result}}'></google-feeds>
<p>Feed title: <span>{{result.title}}</span></p>
    <template is="dom-repeat" items="[[result.entries]]">
        <div class="card">
            <h1>{{item.title}}</h1>
            <div>{{item.publishedDate}}</div>
            <div inner-h-t-m-l="{{item.content}}"></div>
            <div>
                <a href="{{item.link}}">{{item.link}}</a>
            </div>
        </div>
    </template>
</template>

The library used is as follows:

https://elements.polymer-project.org/elements/google-feeds
https://developers.google.com/feed/v1/devguide#resultJson

The combination of the Google Feed API and the Polymer databindig system (particularly Template repeater "dom-repeat") you can get applications with compact and efficient code.

For more details see the following link for the Template repeater (dom-repeat) of Polymer:

https://www.polymer-project.org/1.0/docs/devguide/templates



This template, along with the `polymer-cli` toolchain, also demonstrates use
of the "PRPL pattern" This pattern allows fast first delivery and interaction with
the content at the initial route requested by the user, along with fast subsequent
navigation by pre-caching the remaining components required by the app and
progressively loading them on-demand as the user navigates through the app.

The PRPL pattern, in a nutshell:

* **Push** components required for the initial route
* **Render** initial route ASAP
* **Pre-cache** components for remaining routes
* **Lazy-load** and progressively upgrade next routes on-demand

### Migrating from Polymer Starter Kit v1?

[Check out our blog post that covers what's changed in PSK2 and how to migrate!](https://www.polymer-project.org/1.0/blog/2016-08-18-polymer-starter-kit-or-polymer-cli.html)

### Setup

##### Prerequisites

Install [polymer-cli](https://github.com/Polymer/polymer-cli):

    npm install -g polymer-cli

##### Initialize project from template

    mkdir my-app
    cd my-app
    polymer init starter-kit

### Start the development server

This command serves the app at `http://localhost:8080` and provides basic URL
routing for the app:

    polymer serve --open


### Build

This command performs HTML, CSS, and JS minification on the application
dependencies, and generates a service-worker.js file with code to pre-cache the
dependencies based on the entrypoint and fragments specified in `polymer.json`.
The minified files are output to the `build/unbundled` folder, and are suitable
for serving from a HTTP/2+Push compatible server.

In addition the command also creates a fallback `build/bundled` folder,
generated using fragment bundling, suitable for serving from non
H2/push-compatible servers or to clients that do not support H2/Push.

    polymer build

### Preview the build

This command serves the minified version of the app at `http://localhost:8080`
in an unbundled state, as it would be served by a push-compatible server:

    polymer serve build/unbundled

This command serves the minified version of the app at `http://localhost:8080`
generated using fragment bundling:

    polymer serve build/bundled

### Run tests

This command will run
[Web Component Tester](https://github.com/Polymer/web-component-tester) against the
browsers currently installed on your machine.

    polymer test

### Adding a new view

You can extend the app by adding more views that will be demand-loaded
e.g. based on the route, or to progressively render non-critical sections
of the application.  Each new demand-loaded fragment should be added to the
list of `fragments` in the included `polymer.json` file.  This will ensure
those components and their dependencies are added to the list of pre-cached
components (and will have bundles created in the fallback `bundled` build).