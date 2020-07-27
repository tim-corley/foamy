## Unidirectional Data Flow

The concept that data has one, and only one, way to be transferred to other parts of the application.

Specifically, in React, this means:
 - state is passed to the view and to child components
 - actions are triggered by the view
 - actions can update the state
 - the state change is passed to the view and to child components

The view is a result of the application state. State can only change when actions happen. When actions happen, the state is updated. 

Due to one-way bindings, data cannot flow in the opposite way and this has some key advantages:
 - less error prone, more control over data
 - easier to debug, know what is coming from where
 - more effiecient, library know boundaries

A state is always owned by one component. any data that's affected by this state can only affect components below it - its children. this is the reason that the state is often moved up in the component tree - so that it can be shared between components that need to access it. 
