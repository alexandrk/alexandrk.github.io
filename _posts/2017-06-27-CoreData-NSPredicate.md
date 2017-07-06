---
layout: post
title: "Core Data Predicate"
tags:
  - swift
  - ios
  - CoreData
  - predicate
published: true
---

Uses its own syntax, please refer to the [documentation](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/Predicates/Articles/pSyntax.html#//apple_ref/doc/uid/TP40001795-CJBDBHCB)

e.g., checking for nil or empty fields:
	
	let fr:NSFetchRequest<EntityType> = EntityType.fetchRequest()
	fr.predicate = NSPredicate(format: "fieldName == nil OR fieldName.length == 0")

More complex example:

	let notebooksRequest: NSFetchRequest<Notebook> = Notebook.fetchRequest()
	        
	        let keyPath = "title"
	        let searchString = "y"
	        notebooksRequest.predicate = NSPredicate(format: "%K CONTAINS[c] %@", keyPath, searchString)

>Note:
- **%K** - is a variable argument substitution for key path
- **%@** - is a variable argument substitution for an object value—often astring, number, or date.
- **[c]** - makes `CONTAINS` seach case-insensitive