---
layout: post
title:  "Hard as Two Month Old Bread"
date:   2016-11-29 03:18:51 +0000
---

![](http://i.cubeupload.com/GA7D0l.png)

**Recipe apps are hard**, don't let anyone tell you differently. Now you can do things to make them easier mind you, but for me to do something the way I thought it should be done, it was hard. When you sit down to think about a recipe you often forget about all of the little things that go into something so simple.

If we start with the simplest recipe form we end up with something like this:

``` ruby
Recipe
- Title
- Time
- Servings
- Ingredients
- Directions
```

Well that's a nice an easy recipe right? Sure it looks great, but there are a few questions I might ask. When you say time, what are we talking about here? Cooking time, prep time or is this just the total time for everything required in our recipe? What about our directions, is that just one giant block of text? What about Grandma's Fried Chicken that was 23 different steps? Are we supposed to try and remember where we were in a huge wall of text? That's just silly. So you can see the most basic recipe model we can have still needs a few adjustments to be functional. Let's check it out now ...

``` ruby
Recipe
- Title
- Prep Time
- Cooking Time
- Servings
- Ingredients
- Directions
- - Direction 1
- - Direction 2
- - Direction 3
- - etc
```

Now just those few changes our model has almost doubled in size and wait, what about our ingredients? Surely we can't expect it to just be a long list of ingredients in one block of text? What makes an ingredient though? I mean we surely can use store a whole bunch of strings that read `1 egg` or `1/2 cup milk` or even `3 tbsp sugar`. Those look fine right? What about if we wanted to make our directions more dynamic in the future? Say we wanted to change the servings to double or recipe, well now what do we do? We can't easily manipulate those strings to double them. Now we need to split that up into three more fields that contain our information such as **Quantity**, **Measurement**, and **Ingredient Name**.

Now our model has gotten even larger ...

``` ruby
Recipe
- Title
- Prep Time
- Cooking Time
- Servings
- Ingredients
- - Qty - Measurement - Ingredient Name
- - Qty - Measurement - Ingredient Name
- - Qty - Measurement - Ingredient Name
- - etc
- Directions
- - Direction 1
- - Direction 2
- - Direction 3
- - etc
```

Well now we are getting somewhere, but look how far we've had to come from our simple recipe model. Now we have to keep track of a list of directions, a list of ingredients plus all the rest of our recipe data.  Something as simple as a recipe has now grown into a large complex object.  We can create some different rails models for this object to help break it up a little, but it's no longer a simple recipe.

I say again, **recipes app's are hard**. Don't get me wrong, I've enjoyed creating this recipe app and my models got even more complicated at first. I had some tags to tag a recipe with different things like 'chicken', 'vegan', 'dairy free' or whatever a user might decide to tag it with. That got axed for now, it's a future feature for the kickstarter I'll never run. There was some user uploaded images that were going to take place, yea size constraints took care of that for me.

It's possible to create a simple recipe app with the basic recipe model we used at first, totally possible. It's just not very practical in the long term. So instead I opted to go for the complex models in an effort to help future development of this project.
