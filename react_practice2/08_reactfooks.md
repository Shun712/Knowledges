# useReducerの使い方

1. `rstate`に`state`の値が入る

2. `useReducer`の第一引数では、`dispatch`の関数が走る。また、`state`の更新をどのようにするか定義する。

3. `useState`との違いはコールバック関数に処理を記述するが、`useReducer`は定義の時点で処理を記述する。

4. `useReducer`の第2引数には初期値が入る。

[![Image from Gyazo](https://i.gyazo.com/2fdc321407d0080d3c7b98efd7969d25.png)](https://gyazo.com/2fdc321407d0080d3c7b98efd7969d25)

# useStateとuseReducerの違い

複雑度合いで決める。
`useState`->`useReducer`->`Redux`  
`useState`: 状態の更新の仕方は利用側に託す。
`useReducer`: stateと一緒に更新用の処理を保持。

[![Image from Gyazo](https://i.gyazo.com/c798f79debc30f3cc0e33feff9c8b2a4.png)](https://gyazo.com/c798f79debc30f3cc0e33feff9c8b2a4)

- 純粋性（純粋関数）
- 特定の引数に特定の戻り値
- 不変性

```javascript
import {useReducer} from "react";

const CALC_OPTIONS = ["add", "minus", "divide", "multiply"];

const reducer = (state, {type, payload}) => {
    switch (type) {
        case 'change':
            return {...state, [payload.name]: payload.value};
        case 'add':
            return {...state, result: state.a + state.b}
        case 'minus':
            return {...state, result: state.a - state.b}
        case 'multiply':
            return {...state, result: state.a * state.b}
        case 'divide':
            return {...state, result: state.a / state.b}
        default:
            throw new Error("不明なタイプです");
    }
}

const Example = () => {
    const initState = {
        a: 1,
        b: 2,
        result: 3,
    };

    const [state, dispatch] = useReducer(reducer, initState);

    const calculate = (e) => {
        dispatch({type: e.target.value});
    };

    const numChangeHandler = (e) => {
        dispatch({
            type: 'change',
            payload: {
                name: e.target.name,
                value: parseInt(e.target.value)
            }
        });
    }

    return (
        <>
            <div>
                a:
                <input
                    type="number"
                    name="a"
                    value={state.a}
                    onChange={numChangeHandler}
                />
            </div>
            <div>
                b:
                <input
                    type="number"
                    name="b"
                    value={state.b}
                    onChange={numChangeHandler}
                />
            </div>
            <select value={state.type} onChange={calculate}>
                {CALC_OPTIONS.map(type => {
                    return (
                        <option key={type} value={type}>{type}</option>
                    )
                })}
            </select>
            <h1>結果：{state.result}</h1>
        </>
    );
};
```