---
layout: post
title: Dead Language
date: 2020-04-14
description:
img: posts/2020-04-14/img2.png
fig-caption:
tags: [JavaScript, PhaserJS, Google Firebase, Game Development, Language Learning, Zombies]
author: Seth
---

Dead Language is a zombie-themed language learning video game built using JavaScript and the PhaserJS game framework. It combines fast-paced zombie blasting gameplay and vocab study in a single package in a way that I hope is a little  more entertaining than flashcards.

**check the game out at [deadlanguage.io](https://www.deadlanguage.io).**

---

<div class="center">
  <iframe width="650" height="550" src="https://www.youtube.com/embed/JCvb46SomHg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Project Background

I've been doing game development as a hobby for 15+ years. In fact, game development is what first got me interested in programming. Tinkering with text adventures and quiz games in C++ is how I got my start in coding. I've worked on a number of game projects over the years. Unfortunately, like a lot of software side projects many of them were never completed. I'm very happy with my progress on this one, though.

I started thinking about this game when I was living in Mexico and struggling to learn Spanish. I was fully immersed in a Spanish language culture and I was really struggling to keep up with all the new vocabulary. Flashcards were helpful, but a little tedious. I started thinking about Math Blasters and the other educational games I used to play as a kid, and I wondered if I could make something similar to help myself and others learn Spanish.

I was curious about game development in JavaScript anyway, and this seemed like the perfect excuse to dive in. I tinkered with project for several months: developing features, adding language content, working on music and art work, fixing balance issues, etc. This experience also provided an excellent opportunity to learn more about Google Firebase and the services it provides, such as authentication, a document database, and cloud functions. Dead Language uses all of these for managing user profiles and storing language content.

## Technical Architecture

* [Dead Language GitHub Repo](https://github.com/sethpuckett/dead-language)
* [Dead Language Development Log](https://www.log.deadlanguage.io/)

The bulk of the Dead Language codebase is written in Javascript and leverages the [PhaserJS](https://phaser.io/) game library. The back-end of the system is housed entirely in [Google Firebase](https://firebase.google.com/). I've also developed a couple internal tools to make my life easier while integrating with Firebase, such the [Data Sync](https://github.com/sethpuckett/dead-language-data-sync) app.

PhaserJS is an incredible, fully-featured game library that integrates seamlessly with the canvas feature introduced with HTML 5. It has excellent support for audio, video, input, scene management, error handling, and many features that aren't even used in Dead Language. Development within the framework is based around "scenes", which can be thought of as screens or overlays that can be layered. For example DL has scenes such as the "Title Screen", the "Town Map Screen", the "Gameplay Screen", the "Vocab Study Screen", and so on. Scenes have callback functions that can be overridden to inject logic at different points in the scene lifecycle. Most important among these are `init`, which is called when the screen is initialized, `create`, which is called when the scene is started, and `updated` which is called one per update cycle in the main game loop. Within these functions additional hooks can be created to respond to user input, timers, collisions between game objects, etc. This is the 10,000 foot overview of Phaser and how DL is structured.

The DL backend is supported entirely by Google Firebase, and it uses a few of the included services. User setup, authentication, and password updates are handled by Google Authentication. Google is pretty good at this stuff so I was happy not to roll my own solution. Language content and user profiles are managed by Google Firestore. User profiles include information such as lessons completed, option settings, problem vocab (i.e. the words the player keeps missing), and stats around completed lessons. Firestore is a document database designed for speed. I chose it mostly for its robust JavaScript API and integration with other Firebase services. DL also leverages Google Cloud Functions to do some backend housekeeping based on event hooks.

Hosting is pretty simple for DL because the backend is based entirely on Google Firebase. The game is hosted using GitHub pages with a custom domain name. The deploy process involves an automated WebPack build step that compiles and packages all the resources so they are ready to be served up by GitHub pages. I will likely need to move to a more robust hosting strategy if traffic picks up, but GitHub suits my needs for now.

DL is integrated with Google Analytics so I can analyze traffic and see how people are finding the game.

One shortcoming of Google Firestore is the difficulty with managing data in the web UI. I needed to add, update, and rearrange a lot of language content in the process of making this game and doing it all in the Firestore UI was just not going to work. I developed a [data sync](https://github.com/sethpuckett/dead-language-data-sync) tool that allowed me to manage all the language content in a spreadsheet, which would then be converted to json and synced to FireStore documents for use within the game.

## Future Enhancements

* Offline/local gameplay support
* Mobile gameplay support
* Additional game modes, e.g. "endless mode"
* Additional gampelay features for grammar, gendered words, listening comprehension, etc.
* Support for additional languages and custom vocab
* Achievements

I hope this has been informative. If you have any questions or comments don't hesitate to reach out via Twitter or email!
