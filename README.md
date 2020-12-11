# react-render-xstate
Bind an xstate statemachine to your UI

Usage:

Given a well typed xstate statemachine you can use this component to bind them to react elements.

For example. A statemachine with three states A B and C can be rendered as follows:

```
ReactDOM.render(
    <div>
        {StateMachineComponent(interpreter, {
            A: ({state}) => <div>The A state</div>,
            B: ({state}) => <div>The A state</div>,
            C: ({state}) => <div>The A state</div>,
        })}
    </div>,
    document.getElementById('root')
);

```

This will give a typescript error if a state is missing. That can be prevented by adding a generic wildcard state:

```
ReactDOM.render(
    <div>
        {StateMachineComponent(interpreter, {
            A: ({state}) => <div>The A state</div>,
            B: ({state}) => <div>The A state</div>,
            C: ({state}) => <div>The A state</div>,
            "" ({state}) => <div>The state {state.value} has not yet been defined</div>
        })}
    </div>,
    document.getElementById('root')
);

```

FIXME: document nested and parallel states
