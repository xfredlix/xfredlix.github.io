# Design Patterns
https://sourcemaking.com/design_patterns

- A general reusable solution to a commonly occurring problem within a given context in software design

### Creational Patterns
- A way to create objects while hiding the creation logic, rather than instantiating objects directly using new operator

- Singleton: Ensure that only one instance of a class is created and provide a global access point to the object

- Factory: Creates objects without exposing the instantiation logic to the client and refers to the newly created object through a common interface

- Prototype: Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype


### Structural Patterns
- Class and object composition

- Module: Group several related elements, such as classes, singletons, methods, globally used, into a single conceptual entity


### Behavioral Patterns
- Concerned with communication between objects

- Observer: Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically

- MVC:   Uses  separate  programming  entities  to  store  the  data (model),  to  display  the  data (view) listens to changes/events,  and  to  modify  the  data (controller)
