# Chapter 2 Organizing Domain Logic

1. Transaction Script

> A _Transaction Script_ is essentially a procedure that takes the input from the presentation, process it with validations and calculations, stores data in the data base, and invokes any operations from other systems. It then replies with more data to the presentation, perhaps doing more calculation to help organize and format the reply.

Advantages:

- It's a simple procedural model that most developers understand.
- It works well with a simple data source layer using _Row Data Gateway_ or _Table Data Gateway_.
- It's obvious how to set the transaction boundaries: Start with opening a transaction and end with closing it. It's easy for tools to do this behind the scenes.

Disvantages:
- Duplicate code
- The resulting application can end up being quite a tangled web of routines without a clear structure

Transaction Script -> Table Data Gateway

2. Domain Model

> With a Domain Model we build a model of our domain which, at least on a first approximation, is organized primarily around the nouns in the domain. Thus, a leasing system would have classes for lease, asset, and so forth. The logic for handling validations and calculations would be placed in to this domain model, so shipment object might contain the logic to calculate the shipping charge for a delivery. There might still be routines for calculating a bill, but such a procedure would quickly delegate to a Domain Model method.

Advantages:
- many techniques that allow you to handle increasingly complex logic in a wel-organized way

3. Table Module

