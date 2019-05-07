---
title: "Bibliography With CCK and Views"
date: 2009-01-05T16:49:42+01:00
draft: false
---

I recently finished a site for an author who has a fairly substantial bibliography. She has also been translated into many languages, has multiple publishers and a wide and active community of readers. A complex ask to create a site that manages all of this content in a relatively simple and not-too-techy way? Well, yes and no. 
Yes, in that the initial specification was detailed, necessarily, as it was the hook upon which the site would eventually hang. 
No, since the custom content management tools Views and CCK provides the wherewithal for Drupal to handle pretty much any content type you can throw at it. Couple this with the ease with which Drupal + CCK + Views allows you to create relationships between these content items and display them in many ways, and you have all you need to present detailed and complex information in a manageable way.

The custom types are Book, Review&Translation, and they are linked in two one to many relationship trees, with the Book being the primary type. In other words, for a given book, there can exist multiple reviews, and multiple translations. CCK handles the node links and Views handles the display of the items using Taxonomy to handle the grouping.

