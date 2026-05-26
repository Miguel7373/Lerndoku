
## What is it?

`dispatchEvent` is a method used to trigger events on `EventTarget` objects (like DOM elements or custom classes). It notifies all listeners registered for the event.  
## Syntax 
```typescript target.dispatchEvent(event);``

- **`target`**: Object to dispatch the event (e.g., `document`, custom class).
- **`event`**: An instance of `Event` or `CustomEvent`.

## Use Cases

- Triggering custom events like `change`, `input`, or other user-defined events.
- Notifying components or listeners about state changes.