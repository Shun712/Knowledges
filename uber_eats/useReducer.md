# useReducerの全体像

```javascript
const initialState = {count: 0};

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
    </>
  );
}
```

```javascript
const [state, dispatch] = useReducer(reducer, initialState);
```

`useReducer()`に対して、第一引数に`reducer`、第二引数に`initialState`を渡している。そして、その**返り値**を`[state, dispatch]`というかたちで受け取る。

# reducerとは

```javascript
function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}
```

`reducer()`は第一引数に`state`、第二引数に`action`を受け取る。

