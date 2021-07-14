## 模型 model

模型 `Model` 是一个拥有 **state** 属性的 **class** 或普通 **object** 对象， state 属性用于存储需要持续维护的数据，而**模型上的方法皆用于根据不同的业务场景重制（重新生成） state 数据。**

1. 属性 `state` 用于存储需要持续维护的数据，它的数据类型可以任意选择。
2. 方法 `method` 用于提供生成 state 数据的方案，**其返回值可被认为是最新的 state 数据**。**reducer**模式下的状态管理则是通过**dispatch**触发**action**来达到改变**state**的效果。相比之下，直接调用某个方法来改变**state**和通过比对**action**的**type**改变**state**会更加直接

















## use-agent-reducer 提供的方法

### useAgentReducer

获取数据模型的state和method

```tsx
const { state } = useAgentReducer(menuSelectionRef.current);
```

### useAgentSelector

获取数据模型的state,回调函数的参数就是state

```tsx
const { itemCodeDesc, invalidDays, wangwangNick } = useAgentSelector(
    loginUserRef.current, (state) => state,
  );
```

### useAgentMethods

获取数据模型的method

```tsx
const { saveLocalTimeArr,search } = useAgentMethods(shopInspectionRef.current);
```

## agent-reducer 提供的方法

### weakSharing

### sharing

```tsx
export const loginUserRef = sharing(() => LoginUserModule);
```

### createAgentReducer