
## ToolBox单元测试落地的思考

### 单元测试的优势

- 适应变化
单元测试可以延续用于准确反映当任何变更发生时可执行程序和代码的表现

- 简化集成
单元测试消除程序单元的不可靠，采用自底向上的测试路径。通过先测试程序部件再测试部件组装，使集成测试变得更加简单。这也算是为我们后面使用Cypress 提供基础。

- 文档记录
单元测试提供了系统的一种文档记录。借助于查看单元测试提供的功能和单元测试中如何使用程序单元，开发人员可以直观的理解程序单元的基础API, 这些特点可以指出正确使用和非正确使用程序单元.

### 单元测试原则

 宏观满足AIR原则，微观满足BCDE原则
 
 1. AIR
 - Automatic(自动化)
 - Independent(独立性)
 - Repeatable(可重复)
 
 2. BCED
 
 - Border, 边界值测试，包括循环边界、特殊取值、特殊时间点，数据顺序
 - Correct, 正确的输入，并得到预期的结果
 - Design, 与设计文档相结合，来编写单元测试
 - Error, 单元测试的目的是证明程序有错，而不是证明程序无错, 编写测试用例时有一些强制的错误输入（如非法数据、异常流程、非业务允许输入等）来得到预期的错误结果
 
 
 

### 单元测试规范

- 良好的命名规范- 测试代码也是写给人看的
- 保持测试是幂等的-不同时间 环境运行输出同样的结果
- 把测试类分类，放在不同的地方- 方便维护、快速定位错误
- 测试类应该只测试一个功能- 无论从粒度角度还是单一职责原则都需要这样

### 单元测试在ToolBox测试策略

### *selector 测试*
ToolBox大量使用了reselector, 这部分涉及处理state数据逻辑，也是需要测试的

```js
selector.js

import { createSelector } from 'reselect'

// for performant access/filtering in React component
export const labelArrayToObjectSelector = createSelector(
  [(store, ownProps) => store.products[ownProps.id].labels],
  (labels) => {
    return labels.reduce(
      (result, { code, active }) => ({
        ...result,
        [code]: active,
      }),
      {}
    )
  }
)
```

```js
selector.test.js
import { labelArrayToObjectSelector } from './selector'

test('should transform label array to object', () => {
  const store = {
    products: {
      10085: {
        labels: [
          { code: 'canvas', name: '帆布鞋', active: false },
          { code: 'casual', name: '休闲鞋', active: false },
          { code: 'oxford', name: '牛津鞋', active: false },
          { code: 'bullock', name: '布洛克', active: true },
          { code: 'ankle', name: '高帮鞋', active: true },
        ],
      },
    },
  }
  const expectedActiveness = {
    canvas: false,
    casual: false,
    oxford: false,
    bullock: true,
    ankle: false,
  }

  const productLabels = labelArrayToObjectSelector(store, { id: 10085 })

  expect(productLabels).toEqual(expectedActiveness)
})
```

### component 测试

组件这部分可以测试的东西比较多，没有统一的标准， 本着收益最大化的原则， 我们主要关注**是否正确渲染** 和 **是否正确调用事件** [React官网](https://zh-hans.reactjs.org/docs/testing-recipes.html) 已经给了指导

- 是否正确渲染

```js
// hello.js

import React from "react";

export default function Hello(props) {
  if (props.name) {
    return <h1>你好，{props.name}！</h1>;
  } else {
    return <span>嘿，陌生人</span>;
  }
}
```

```js
// hello.test.js

import React from "react";
import { render, unmountComponentAtNode } from "react-dom";
import { act } from "react-dom/test-utils";

import Hello from "./hello";

let container = null;
beforeEach(() => {
  // 创建一个 DOM 元素作为渲染目标
  container = document.createElement("div");
  document.body.appendChild(container);
});

afterEach(() => {
  // 退出时进行清理
  unmountComponentAtNode(container);
  container.remove();
  container = null;
});

it("渲染有或无名称", () => {
  act(() => {
    render(<Hello />, container);
  });
  expect(container.textContent).toBe("嘿，陌生人");

  act(() => {
    render(<Hello name="Jenny" />, container);
  });
  expect(container.textContent).toBe("你好，Jenny！");

  act(() => {
    render(<Hello name="Margaret" />, container);
  });
  expect(container.textContent).toBe("你好，Margaret！");
});
```

- 是否正确调用事件

```js
// toggle.js

import React, { useState } from "react";

export default function Toggle(props) {
  const [state, setState] = useState(false);
  return (
    <button
      onClick={() => {
        setState(previousState => !previousState);
        props.onChange(!state);
      }}
      data-testid="toggle"
    >
      {state === true ? "Turn off" : "Turn on"}
    </button>
  );
}
```

```js
/ toggle.test.js

import React from "react";
import { render, unmountComponentAtNode } from "react-dom";
import { act } from "react-dom/test-utils";

import Toggle from "./toggle";

let container = null;
beforeEach(() => {
  // 创建一个 DOM 元素作为渲染目标
  container = document.createElement("div");
  document.body.appendChild(container);
});

afterEach(() => {
  // 退出时进行清理
  unmountComponentAtNode(container);
  container.remove();
  container = null;
});

it("点击时更新值", () => {
  const onChange = jest.fn();
  act(() => {
    render(<Toggle onChange={onChange} />, container);
  });

  // 获取按钮元素，并触发点击事件
  const button = document.querySelector("[data-testid=toggle]");
  expect(button.innerHTML).toBe("Turn on");

  act(() => {
    button.dispatchEvent(new MouseEvent("click", { bubbles: true }));
  });

  expect(onChange).toHaveBeenCalledTimes(1);
  expect(button.innerHTML).toBe("Turn off");

  act(() => {
    for (let i = 0; i < 5; i++) {
      button.dispatchEvent(new MouseEvent("click", { bubbles: true }));
    }
  });

  expect(onChange).toHaveBeenCalledTimes(6);
  expect(button.innerHTML).toBe("Turn on");
});

```




### reducers
作为redux中唯一可以操作数据的一层, 整个应用全局状态都是在这处理，要求100%覆盖, 参考[这里](http://cn.redux.js.org//docs/recipes/WritingTests.html)


```js
// reducer.js

import { ADD_TODO } from '../constants/ActionTypes'
​
const initialState = [
  {
    text: 'Use Redux',
    completed: false,
    id: 0
  }
]
​
export default function todos(state = initialState, action) {
  switch (action.type) {
    case ADD_TODO:
      return [
        {
          id: state.reduce((maxId, todo) => Math.max(todo.id, maxId), -1) + 1,
          completed: false,
          text: action.text
        },
        ...state
      ]
​
    default:
      return state
  }
}
```


```js
// reducers.test.js
import reducer from '../../reducers/todos'
import * as types from '../../constants/ActionTypes'
​
describe('todos reducer', () => {
  it('should return the initial state', () => {
    expect(reducer(undefined, {})).toEqual([
      {
        text: 'Use Redux',
        completed: false,
        id: 0
      }
    ])
  })
​
  it('should handle ADD_TODO', () => {
    expect(
      reducer([], {
        type: types.ADD_TODO,
        text: 'Run the tests'
      })
    ).toEqual([
      {
        text: 'Run the tests',
        completed: false,
        id: 0
      }
    ])
​
    expect(
      reducer(
        [
          {
            text: 'Use Redux',
            completed: false,
            id: 0
          }
        ],
        {
          type: types.ADD_TODO,
          text: 'Run the tests'
        }
      )
    ).toEqual([
      {
        text: 'Run the tests',
        completed: false,
        id: 1
      },
      {
        text: 'Use Redux',
        completed: false,
        id: 0
      }
    ])
  })
})

```

### actions测试
我们重点关注异步actions


```js
// actions.js
import 'cross-fetch/polyfill'
​
function fetchTodosRequest() {
  return {
    type: FETCH_TODOS_REQUEST
  }
}
​
function fetchTodosSuccess(body) {
  return {
    type: FETCH_TODOS_SUCCESS,
    body
  }
}
​
function fetchTodosFailure(ex) {
  return {
    type: FETCH_TODOS_FAILURE,
    ex
  }
}
​
export function fetchTodos() {
  return dispatch => {
    dispatch(fetchTodosRequest())
    return fetch('http://example.com/todos')
      .then(res => res.json())
      .then(body => dispatch(fetchTodosSuccess(body)))
      .catch(ex => dispatch(fetchTodosFailure(ex)))
  }
}
```


```js
// actions.test.js

import configureMockStore from 'redux-mock-store'
import thunk from 'redux-thunk'
import * as actions from '../../actions/TodoActions'
import * as types from '../../constants/ActionTypes'
import fetchMock from 'fetch-mock'
import expect from 'expect' // 可以使用任何测试库
​
const middlewares = [thunk]
const mockStore = configureMockStore(middlewares)
​
describe('async actions', () => {
  afterEach(() => {
    fetchMock.reset()
    fetchMock.restore()
  })
​
  it('creates FETCH_TODOS_SUCCESS when fetching todos has been done', () => {
    fetchMock
      .getOnce('/todos', { body: { todos: ['do something'] }, headers: { 'content-type': 'application/json' } })
​
​
    const expectedActions = [
      { type: types.FETCH_TODOS_REQUEST },
      { type: types.FETCH_TODOS_SUCCESS, body: { todos: ['do something'] } }
    ]
    const store = mockStore({ todos: [] })
​
    return store.dispatch(actions.fetchTodos()).then(() => {
      // return of async actions
      expect(store.getActions()).toEqual(expectedActions)
    })
  })
})
```

### 工具方法
- Helper
由于我们项目重度使用immutable.js， 在js对象与不可变数据不能直接操作，需要自定义各种方法获取以及操作数据,这部分也是需要100%覆盖，这部分可以看做是reducer或者selector的延伸

- Utils
处理各种数据的工作方法  比如处理日期 字符串 数字也是需要测试

- 公共组件
常用的的Toast Input Button 类型这样的公共组件

### 总结
本文结合当前项目使用的技术栈 React + Redux + Immutable, 提供具体单元测试点。当前阶段，我们可以主要关注上面提到的测试点的覆盖率，后续再去再去关注细节以及整体的覆盖率。 mock, Cypress也是我们后面需要搞起来的。

 ### 参考
 
 - [单元测试](https://zh.wikipedia.org/wiki/%E5%8D%95%E5%85%83%E6%B5%8B%E8%AF%95)
 - [19条技巧教你更好的编写单元测试](https://www.techug.com/post/19-unit-test-code-tips.html)
 - [React 单元测试策略及落地](https://www.infoq.cn/article/asmlfdi3pi_vepxpo3lu)
 - [How to Start Testing Your React Apps Using the React Testing Library and Jest](https://www.freecodecamp.org/news/8-simple-steps-to-start-testing-react-apps-using-react-testing-library-and-jest/#8-testing-http-request)
 
    




