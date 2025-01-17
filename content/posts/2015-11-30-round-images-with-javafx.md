---
outdated: true
title: 'Round images with JavaFX'
date: "2015-11-30"
author: hendrik
categories: [JavaFX, Layout & UI]
excerpt: 'This post gives an example for creating round image controls with JavaFX'
---
In modern UI you can often find round avatar images like shown in this image:

![example](/posts/guigarage-legacy/round-images-example.png)

Creating this special UI nodes with JavaFX isn't that hard. The most important JavaFX features to create such a rounded image is clipping. By using clipping you can define the area in that a control can draw it's content. A clip can be any shape and you only need to set the `shape property` of a JavaFX `Node` instance to define its clipping. You can find an additional clipping description [here](https://dlemmermann.wordpress.com/2015/02/18/javafx-tip-18-path-clipping/).

Let's start creating the component. As a first step we will define a `Circle` shape as a clip and define it for an `ImageView` instance:

![clip](/posts/guigarage-legacy/clip-1024x389.png)

In addition a border should be added to the component. To do so we add one (or several) `Circle` shapes on top of the `ImageView`:

![border](/posts/guigarage-legacy/border-1024x378.png)

In the JavaFX code you can simply bind the bounds of the image to the bounds of the clip and the circle instances that are used as a border.
