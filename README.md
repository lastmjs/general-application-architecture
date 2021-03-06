# A General Application Architecture

These are my thoughts on the major pieces of a well-architected software application. This will grow and be refined over time, with greater explanations and links to resources that offer justification and insight.

## High-level Components

### Application State

This is the global mutable state of the application. Any state that can change after it is created and that is read or written to in multiple places in the application is considered part of the application state. Any changes to the state must be managed carefully and explicitly. Redux is a great way to handle changes to this state.

### Data Types

These types represent all of the individually immutable plain data objects that the application needs.

### Modules

Collections of functions.

### Pure Services

Modules that perform a variety of pure computations (numeric calculations, data transformations, etc). Pure services do not change application state alone. Action creators may use services to prepare the changes that will eventually be applied to the application state.

### Impure Services

Modules that perform a variety of impure computations (filesystem access, database access, network requests, etc). Impure services do not change application state alone. Action creators may use services to prepare the changes that will eventually be applied to the application state.

### Actions

Plain data objects that describe intents to mutate the application state, with the necessary data to perform the mutation. Actions change application state.

### Action Creators

Functions that dispatch actions on the application store. Any side-effects needed to create an action can be performed here. Action creators usually end up changing application state.

### Components

Collections of functions and local mutable state. Components receive side-causes from the universe and cause side-effects in the universe. Components are the edges of the application. They are the interface to the universe. Events from the universe are received, then appropriate services or actions are invoked, usually causing the application state to change. All components update their corresponding local state in synchronization with the application state.

TODO
- [ ] Explain the concept of a store in more detail. Make Redux a suggestion on one implementation of that kind of store.
- [ ] Fill out each explanation more fully.
- [ ] Go over the explanations with friends and see what does and does not make sense
- [ ] Finish the diagram: https://www.draw.io/#G0B2XvotCal76YWDlrb1N4eXRLZ28
- [ ] Turn this into a beautiful website by using one of those static site generator things. Find the best one for software documentation
- [ ] Explain the use of the observer pattern or functional reactive patterns like Observables or RXJs to synchronize state in the components section
- [ ] Explain that in general Actions have as their purpose causing side-effects to the global application state in some way. Services however, even if they are impure (side-effects or side-causes within them, such as generating dates, random numbers, accessing databases), do not have as their end to change the application state. They do not mutate the application state. They are services to be used by the actions or components to help construct the data that will be used to change the application state.
