---
outdated: true
title: 'BindableTransition'
date: "2012-12-31"
author: hendrik
categories: [General, JavaFX]
excerpt: 'JavaFX supports a lot of transition and animation classes. But sometimes you need a special animation for that no default transition is provided by JavaFX.'
---
JavaFX supports a lot of [transition and animation](http://docs.oracle.com/javafx/2/animations/basics.htm#CJAJJAGI) classes for Node properties like the [`javafx.animation.ScaleTransition`](http://docs.oracle.com/javafx/2/api/javafx/animation/ScaleTransition.html). But sometimes you need a special animation for that no default transition is provided by JavaFX. Currently the best pratice is to extend [`javafx.animation.Transition`](http://docs.oracle.com/javafx/2/api/javafx/animation/Transition.html) and override the `interpolate(double frac)` method:

{{< highlight java >}}
protected void interpolate(double frac) {
  myProperty.set(frac);
}
{{< / highlight >}}

Because JavaFX offers [PropertyBinding](http://docs.oracle.com/javafx/2/binding/jfxpub-binding.htm) I created a `BindableTransition` which current fraction is a `Property` and can be bind to any other `NumberProperty`. Here is an example:

{{< highlight java >}}
Button button = new Button("BindableTransition");
DropShadow shadow = DropShadowBuilder.create().build();
button.setEffect(shadow);

final Duration duration = Duration.millis(1200);
BindableTransition transition = new BindableTransition(duration);
transition.setCycleCount(1000);
transition.setAutoReverse(true);

shadow.offsetXProperty().bind(transition.fractionProperty().multiply(32));
shadow.offsetYProperty().bind(transition.fractionProperty().multiply(32));
button.translateXProperty().bind(transition.fractionProperty().multiply(-32));

transition.play();
{{< / highlight >}}

The `fractionProperty` of the `BindableTransition` is bound to three different properties and the result will look like this:

{{< vimeo 56550389 >}}

The [BindableTransition](https://github.com/JFXtras/jfxtras-labs/blob/master/src/main/java/jfxtras/labs/animation/BindableTransition.java) class and a [demo](https://github.com/JFXtras/jfxtras-labs/blob/master/src/test/java/jfxtras/labs/animation/BindableTransitionTrial.java)are commited to the [JFXtras project](http://jfxtras.org).
