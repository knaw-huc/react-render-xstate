# react-render-xstate
Bind an xstate statemachine to your UI

Usage:

Given a well typed xstate statemachine you can use this component to bind them to react elements.

For example. A statemachine with three states A B and C can be rendered as follows:

```ts
ReactDOM.render(
    <div>
        {StateMachineComponent(interpreter, {
            A: ({state}) => <div>The A state</div>,
            B: ({state}) => <div>The B state</div>,
            C: ({state}) => <div>The C state</div>,
        })}
    </div>,
    document.getElementById('root')
);

```

The above example will give a typescript error when you do not map all states in the state machine. Alternatively you can provide a generic wildcard state:

```ts
ReactDOM.render(
    <div>
        {StateMachineComponent(interpreter, {
            A: ({state}) => <div>The A state</div>,
            B: ({state}) => <div>The B state</div>,
            C: ({state}) => <div>The C state</div>,
            "" ({state}) => <div>The state {state.value} has not yet been defined</div>
        })}
    </div>,
    document.getElementById('root')
);

```

Nested states translate to nested mappings:

```ts
ReactDOM.render(
  <div>
      {StateMachineComponent(interpreter, {
          A: ({state}) => <div>The A state</div>,
          B: ({state}) => <div>The B state</div>,
          C: ({state}) => <div>The C state</div>,
          D: {
            D-first: ({state}) => <div>The first D state</div>,
            D-alt: ({state}) => <div>The alternative D state</div>,
          },
          "": ({state}) => <div>The state {state.value} has not yet been defined</div>
      })}
  </div>,
  document.getElementById('root')
);
```

Parallel states (often used for the position in the application and the logged in state for example) are handled by merging the components:

```ts

ReactDOM.render(
  <div>
      {StateMachineComponent(interpreter, {
          A: {
            B: () => <div>B state</div>,
            C: () => <div>C state</div>,
            ":merge": (state, {B, C}) => <div>{B} {C}</div>
          }
      })}
  </div>,
  document.getElementById('root')
);
```
