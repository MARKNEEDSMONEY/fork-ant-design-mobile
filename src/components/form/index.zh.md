# Form 表单

<code src="./demos/demo1.tsx"></code>

<code src="./demos/demo3.tsx"></code>

<code src="./demos/demo5.tsx"></code>

<code src="./demos/demo2.tsx"></code>

## Form

### 属性

| 属性              | 说明                                                         | 类型                                               | 默认值       |
| ----------------- | ------------------------------------------------------------ | -------------------------------------------------- | ------------ |
| mode              | 支持默认和卡片两种模式                                       | `'default' \| 'card'`                              | `'default'`  |
| layout            | 布局模式                                                     | `'vertical' \| 'horizontal'`                       | `'vertical'` |
| disabled          | 是否禁用                                                     | `boolean`                                          | `false`      |
| hasFeedback       | 是否展示错误反馈                                             | `boolean`                                          | `true`       |
| requiredMarkStyle | 必填选填的标记样式                                           | `'asterisk' \| 'text-required' \| 'text-optional'` | `'asterisk'` |
| footer            | 表单尾部的内容，常常用来放置提交按钮                         | `ReactNode`                                        | -            |
| form              | 经 `Form.useForm()` 创建的 form 控制实例，不提供时会自动创建 | `FormInstance`                                     | -            |
| initialValues     | 表单默认值，只有初始化以及重置时生效                         | `object`                                           | -            |
| name              | 表单名称，会作为表单字段 `id` 前缀使用                       | `string`                                           | -            |
| preserve          | 当字段被删除时保留字段值                                     | `boolean`                                          | `true`       |
| validateMessages  | 验证提示模板，说明见下                                       | `ValidateMessages`                                 | -            |
| validateTrigger   | 统一设置字段触发验证的时机                                   | `string \| string[]`                               | `'onChange'` |
| onFieldsChange    | 字段更新时触发                                               | `(changedFields, allFields) => void`               | -            |
| onFinish          | 提交表单且数据验证成功后触发                                 | `(values) => void`                                 | -            |
| onFinishFailed    | 提交表单且数据验证失败后触发                                 | `({ values, errorFields, outOfDate }) => void`     | -            |
| onValuesChange    | 字段值更新时触发                                             | `(changedValues, allValues) => void`               | -            |

### FormInstance

| 属性            | 说明                                                                                                       | 类型                                                                                                        |
| --------------- | ---------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| getFieldValue   | 获取对应字段名的值                                                                                         | `(name: NamePath) => any`                                                                                   |
| getFieldsValue  | 获取一组字段名对应的值，会按照对应结构返回。默认返回现存字段值，当调用 `getFieldsValue(true)` 时返回所有值 | `(nameList?: NamePath[], filterFunc?: (meta: { touched: boolean, validating: boolean }) => boolean) => any` |
| getFieldError   | 获取对应字段名的错误信息                                                                                   | `(name: NamePath) => string[]`                                                                              |
| getFieldsError  | 获取一组字段名对应的错误信息，返回为数组形式                                                               | `(nameList?: NamePath[]) => FieldError[]`                                                                   |
| isFieldTouched  | 检查对应字段是否被用户操作过                                                                               | `(name: NamePath) => boolean`                                                                               |
| isFieldsTouched | 检查一组字段是否被用户操作过，`allTouched` 为 `true` 时检查是否所有字段都被操作过                          | `(nameList?: NamePath[], allTouched?: boolean) => boolean`                                                  |
| resetFields     | 重置一组字段到 `initialValues`                                                                             | `(fields?: FieldData[]) => void`                                                                            |
| setFields       | 设置一组字段状态                                                                                           | `(fields: FieldData[]) => void`                                                                             |
| setFieldsValue  | 设置表单的值（该值将直接传入 form store 中。如果你不希望传入对象被修改，请克隆后传入）                     | `(values) => void`                                                                                          |
| submit          | 提交表单，与点击 `submit` 按钮效果相同                                                                     | `() => void`                                                                                                |
| validateFields  | 触发表单验证                                                                                               | `(nameList?: NamePath[]) => Promise`                                                                        |

### validateMessages

Form 为验证提供了[默认的错误提示信息](https://github.com/react-component/field-form/blob/master/src/utils/messages.ts)，你可以通过配置 `validateMessages` 属性，修改对应的提示模板。一种常见的使用方式，是配置国际化提示信息：

```jsx
const validateMessages = {
  required: "'${name}' 是必选字段",
  // ...
};
<Form validateMessages={validateMessages} />;
```

### CSS 变量

| 变量名          | 描述                   | 默认值                              |
| --------------- | ---------------------- | ----------------------------------- |
| --border-inner  | 表单项之间的边框样式   | `solid 1px var(--adm-border-color)` |
| --border-top    | 表单容器顶部的边框样式 | `solid 1px var(--adm-border-color)` |
| --border-bottom | 表单容器底部的边框样式 | `solid 1px var(--adm-border-color)` |

## Form.Item

### 属性

| 属性                                               | 说明                                                                                                         | 类型                                          | 默认值                                             |
| -------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ | --------------------------------------------- | -------------------------------------------------- |
| label                                              | 标签名                                                                                                       | `ReactNode`                                   | -                                                  |
| help                                               | 提示文本                                                                                                     | `ReactNode`                                   | -                                                  |
| required                                           | 是否必选                                                                                                     | `boolean`                                     | `false`（如有设置 `rules`，则会根据 `rules` 判断） |
| disabled                                           | 是否禁用                                                                                                     | `boolean`                                     | 父级 Form 的 `disabled`                            |
| noStyle                                            | 不使用样式，只使用字段管理                                                                                   | `boolean`                                     | `false`                                            |
| hidden                                             | 是否隐藏整个字段                                                                                             | `boolean`                                     | `false`                                            |
| layout                                             | 布局模式                                                                                                     | `'vertical' \| 'horizontal'`                  | 父级 Form 的 `layout`                              |
| childElementPosition <Experimental></Experimental> | 表单控件部分的位置                                                                                           | `'normal' \| 'right'`                         | `'normal'`                                         |
| hasFeedback                                        | 是否展示错误反馈                                                                                             | `boolean`                                     | `true`                                             |
| dependencies                                       | 设置依赖字段，说明见下                                                                                       | `NamePath[]`                                  | -                                                  |
| valuePropName                                      | 子节点的值的属性，如 Switch 的是 'checked'。该属性为 `getValueProps` 的封装，自定义 `getValueProps` 后会失效 | `string`                                      | `value`                                            |
| name                                               | 字段名，支持数组                                                                                             | `NamePath`                                    | -                                                  |
| rules                                              | 校验规则，设置字段的校验逻辑                                                                                 | `Rule[]`                                      | -                                                  |
| messageVariables                                   | 默认验证字段的信息                                                                                           | `Record<string, string>`                      | -                                                  |
| trigger                                            | 设置收集字段值变更的时机                                                                                     | `string`                                      | `onChange`                                         |
| validateTrigger                                    | 设置字段校验的时机                                                                                           | `string \| string[]`                          | `onChange`                                         |
| shouldUpdate                                       | 自定义字段更新逻辑，说明见下                                                                                 | `boolean \| (prevValue, curValue) => boolean` | `false`                                            |
| initialValue                                       | 设置子元素默认值，如果与 Form 的 `initialValues` 冲突则以 Form 为准                                          | `any`                                         | -                                                  |

Form.Item 的布局是基于 List.Item 实现的，所以它还支持 [List.Item](./list#listitem) 的以下属性：

`onClick` `extra` `clickable` `arrow` `description`

被设置了 `name` 属性的 `Form.Item` 包装的控件，表单控件会**自动添加** `value`（或 `valuePropName` 指定的其他属性） `onChange`（或 `trigger` 指定的其他属性），数据同步将被 Form 接管，因此，如果你给 `Form.Item` 设置了 `name` 属性，**那么请确保它的 `children` 是一个有效的 `ReactElement` 控件**，并且能够接受上文中提到的 `value` 和 `onChange` 属性（或指定的其他属性），例如：

```jsx
<Form.Item name='foo'>
  <Input />
</Form.Item>
```

而下面这些写法都是错误的：

```jsx
<Form.Item name='foo'>
  <Input />
  <div>hello</div>
</Form.Item>
// 错误：Form.Item 的 children 中包含了多个元素
```

```jsx
<Form.Item name='foo'>
  hello
  <Input />
</Form.Item>
// 错误：同上，Form.Item 的 children 中包含了多个元素
```

```jsx
<Form.Item name='foo'>
  <div>
    <Input />
  </div>
</Form.Item>
// 错误：Form.Item 的 children 其实是 div，而 div 并不能接受 value 和 onChange 属性
```

同时请注意：

1. 你**不再需要也不应该**用 `onChange` 来做数据收集同步（你可以使用 Form 的 `onValuesChange`），但还是可以继续监听 `onChange` 事件。
2. 你不能用控件的 `value` 或 `defaultValue` 等属性来设置表单域的值，默认值可以用 Form 里的 `initialValues` 来设置。注意 `initialValues` 不能被 `setState` 动态更新，你需要用 `setFieldsValue` 来更新。
3. 你不应该用 `setState`，可以使用 `form.setFieldsValue` 来动态改变表单值。

举个例子，下面的这种写法是错误的：

```jsx
<Form.Item name='foo'>
  <Input
    value={myInputValue} // 错误：value 不应该被手动控制
    onChange={(v) => { setMyInputValue(v) }} // 错误：虽然你可以监听 onChange 事件，但是你不应该在这里去维护自己的状态
  />
</Form.Item>
```

### dependencies

当字段间存在依赖关系时使用。如果一个字段设置了 `dependencies` 属性。那么它所依赖的字段更新时，该字段将自动触发更新与校验。一种常见的场景，就是注册用户表单的“密码”与“确认密码”字段。“确认密码”校验依赖于“密码”字段，设置 `dependencies` 后，“密码”字段更新会重新触发“校验密码”的校验逻辑。

`dependencies` 不应和 `shouldUpdate` 一起使用，因为这可能带来更新逻辑的混乱。

### shouldUpdate

Form 通过增量更新方式，只更新被修改的字段相关组件以达到性能优化目的。大部分场景下，你只需要编写代码或者与 [`dependencies`](#dependencies) 属性配合校验即可。而在某些特定场景，例如修改某个字段值后出现新的字段选项、或者纯粹希望表单任意变化都对某一个区域进行渲染。你可以通过 `shouldUpdate` 修改 Form.Item 的更新逻辑。

当 `shouldUpdate` 为 `true` 时，Form 的任意变化都会使该 Form.Item 重新渲染。这对于自定义渲染一些区域十分有帮助：

```jsx
<Form.Item shouldUpdate>
  {() => {
    return <pre>{JSON.stringify(form.getFieldsValue(), null, 2)}</pre>;
  }}
</Form.Item>
```

当 `shouldUpdate` 为方法时，表单的每次数值更新都会调用该方法，提供原先的值与当前的值以供你比较是否需要更新。这对于是否根据值来渲染额外字段十分有帮助：

```jsx
<Form.Item shouldUpdate={(prevValues, curValues) => prevValues.additional !== curValues.additional}>
  {() => {
    return (
      <Form.Item name="other">
        <Input />
      </Form.Item>
    );
  }}
</Form.Item>
```

### messageVariables

你可以通过 `messageVariables` 修改 Form.Item 的默认验证信息。

```jsx
<Form>
  <Form.Item messageVariables={{ another: 'good' }} label="user">
    <Input />
  </Form.Item>
  <Form.Item messageVariables={{ label: 'good' }} label={<span>user</span>}>
    <Input />
  </Form.Item>
</Form>
```

## 自定义表单字段

自定义或第三方的表单控件，也可以与 Form 组件一起使用。只要该组件遵循以下的约定：

- 提供受控属性 `value` 值同名的属性。
- 提供 `onChange` 事件。

<code src="./demos/demo4.tsx"></code>

## Form.Header

你可以通过 `Form.Header` 来对表单项进行分组。

### 属性

| 属性     | 说明                                                 | 类型        | 默认值 |
| -------- | ---------------------------------------------------- | ----------- | ------ |
| children | 分组标题，如果不传的话，则会渲染为一个没有内容的分隔 | `ReactNode` | -      |

## Form.Subscribe

### 属性

| 属性     | 说明                           | 类型                                                                    | 默认值 |
| -------- | ------------------------------ | ----------------------------------------------------------------------- | ------ |
| to       | 同 Form.Item 的 `dependencies` | `NamePath[]`                                                            | -      |
| children | 渲染函数                       | `(changedValues: Record<string, any>, form: FormInstance) => ReactNode` | -      |

### 示例

<code src="./demos/demo-subscribe.tsx"></code>

### useWatch

<code src="./demos/demo-use-watch.tsx"></code>

## Form.Array <Experimental></Experimental>

为字段提供数组化管理。

| 属性         | 说明                                                                | 类型                                                                          | 默认值 |
| ------------ | ------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ------ |
| name         | 字段名，支持数组                                                    | `NamePath[]`                                                                  | -      |
| children     | 渲染函数                                                            | `(fields: FormArrayField[], operation: FormArrayOperation) => ReactElement[]` | -      |
| renderHeader | 渲染每一项的头部内容                                                | `(field: FormArrayField, operation: FormArrayOperation) => ReactNode`         | -      |
| renderAdd    | 渲染添加按钮的文案                                                  | `() => ReactNode`                                                             | -      |
| onAdd        | 自定义添加方法                                                      | `(operation: FormArrayOperation) => void`                                     | -      |
| initialValue | 设置子元素默认值，如果与 Form 的 `initialValues` 冲突则以 Form 为准 | `any[]`                                                                       | -      |

### FormArrayField

| 属性  | 说明                | 类型     |
| ----- | ------------------- | -------- |
| index | 当前 Field 是第几项 | `number` |
| key   | 唯一标识            | `number` |

### FormArrayOperation

Form.Array 渲染表单相关操作函数。

| 属性   | 说明       | 类型                       |
| ------ | ---------- | -------------------------- |
| add    | 新增表单项 | `(initValue: any) => void` |
| remove | 删除表单项 | `(index: number) => void`  |

### 示例

<code src="./demos/demo-array.tsx"></code>

## 一些通用的类型定义

### NamePath

`string | number | (string | number)[]`

### FieldData

| 属性       | 说明             | 类型         |
| ---------- | ---------------- | ------------ |
| errors     | 错误信息         | `string[]`   |
| name       | 字段名称         | `NamePath[]` |
| touched    | 是否被用户操作过 | `boolean`    |
| validating | 是否正在校验     | `boolean`    |
| value      | 字段对应值       | `any`        |

### Rule

Rule 支持接收 object 进行配置，也支持 function 来动态获取 form 的数据：

```tsx
type Rule = RuleConfig | ((form: FormInstance) => RuleConfig);
```

| 属性            | 说明                                                                                                                                | 类型                       |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------- | -------------------------- |
| defaultField    | 仅在 `type` 为 `array` 类型时有效，用于指定数组元素的校验规则                                                                       | `rule`                     |
| enum            | 是否匹配枚举中的值（需要将 `type` 设置为 `enum`）                                                                                   | `any[]`                    |
| len             | string 类型时为字符串长度；number 类型时为确定数字； array 类型时为数组长度                                                         | `number`                   |
| max             | 必须设置 `type`：string 类型为字符串最大长度；number 类型时为最大值；array 类型时为数组最大长度                                     | `number`                   |
| message         | 错误信息，不设置时会通过[模板](#validatemessages)自动生成                                                                           | `string`                   |
| min             | 必须设置 `type`：string 类型为字符串最小长度；number 类型时为最小值；array 类型时为数组最小长度                                     | `number`                   |
| pattern         | 正则表达式匹配                                                                                                                      | `RegExp`                   |
| required        | 是否为必选字段                                                                                                                      | `boolean`                  |
| transform       | 将字段值转换成目标值后进行校验                                                                                                      | `(value) => any`           |
| type            | 类型，常见有 `string` \|`number` \|`boolean` \|`url` \| `email`。更多请参考[此处](https://github.com/yiminghe/async-validator#type) | `string`                   |
| validateTrigger | 设置触发验证时机，必须是 Form.Item 的 `validateTrigger` 的子集                                                                      | `string \| string[] `      |
| validator       | 自定义校验，接收 Promise 作为返回值。[示例](#自定义表单字段)参考                                                                    | `(rule, value) => Promise` |
| warningOnly     | 仅警告，不阻塞表单提交                                                                                                              | `boolean`                  |
| whitespace      | 如果字段仅包含空格则校验不通过，只在 `type: 'string'` 时生效                                                                        | `boolean`                  |
