# ๐น๏ธ To do list๋ก ๋ณด๋ Storybook์ UI ๊ฐ๋ฐ ๋ฐ Test Flow

```bash
yarn create react-app ./ --template typescript
npx sb init
```

<br />

# ๐ผ Intro

![TODO](./docs/example.png)

Storybook์์ ์์๋ก ์ฌ์ฉํ๋ Todolist App์ ๋ง๋ค์ด๋ณด๊ฒ ์ต๋๋ค.

<br />

# UI Spec

![TODO](./docs/todo1.png)

Todo UI์ ๊ธฐ๋ฅ ๋ช์ธ๋ ์ด๋ ์ต๋๋ค.

- `TodoData`
  - `title` : Todo์ ๋ด์ฉ
  - `state` : Todo์ ์๋ฃ ์ฌ๋ถ
- `pinned` : Todo ์๋จ ๊ณ ์  ์ฌ๋ถ
- `onEditTitle` : Todo์ ์ ๋ชฉ์ ์์ ํ  ์ ์๋ค
- `onTogglePinTask` : ๋ชฉ๋ก ์ค์์ ์๋จ์ผ๋ก ๊ณ ์ ํ  ์ ์๋ค.
- `onArchiveTodo` : Todo๋ฅผ ์๋ฃ์ํฌ ์ ์๋ค.

๊ทธ๋ฆฌ๊ณ  `Todolist`๋ ์ด `Todo`์ ๋ชฉ๋ก์ ๋ถ๋ชจ ์ปดํฌ๋ํธ์๋๋ค.

Todo์ ๋ค์ด๊ฐ ๋ฐ์ดํฐ ๋ฐฐ์ด ์ํ๋ฅผ ์ฌ๊ธฐ์ ๊ด๋ฆฌํ  ์์ ์๋๋ค.

<br />

# ๊ฐ๋ฐ ํ๋ก์ธ์ค

## 1. ๋์์ธ์ ๋ง์ถฐ ์ปดํฌ๋ํธ ๊ฐ๋ฐ

```tsx
// component/todo/todo.stories.tsx
import React from "react";
import { ComponentStory, ComponentMeta } from "@storybook/react";
import Todo from ".";

export default {
  title: "component/Todo",
  component: Todo,
} as ComponentMeta<typeof Todo>;

const Template: ComponentStory<typeof Todo> = (args) => <Todo {...args} />;

export const Default = Template.bind({});
Default.args = {};
```

`Todo` ์ปดํฌ๋ํธ๋ฅผ ๊ฐ๋ฐํ๊ธฐ ์ํด ์คํ ๋ฆฌ ํ์ผ์ ์์ฑํด์ค๋๋ค.

react-app์์ ๋งค๋ฒ ์ผ์ผ์ด importํ์ฌ ๋์ผ๋ก ํ์ธํ๊ณ  State๋ฅผ ์ฒดํฌํ  ๊ฒ์ด ์๋๋ผ

์คํ ๋ฆฌ๋ถ ํ๊ฒฝ์์ ๊ฐํธํ๊ฒ UI๋ฅผ ๊ฐ๋ฐํ  ์ ์์ต๋๋ค.

![TODO](./docs/todo2.png)

์ฒซ ์คํ ๋ฆฌ๋ฅผ ์์ฑํ์ต๋๋ค! ์ด์  ๊ตฌํํด์ผ๋  ์ํ๋ค์ ์์ฑํด๋ด์๋ค!

<br />

## 2. ํ์คํธ ์ผ์ด์ค ์์ฑ

![TODO](./docs/todo3.gif)

์คํ ๋ฆฌ๋ถ์์๋ ํ์คํธ ์ผ์ด์ค๋ฅผ ์คํ ๋ฆฌ๋ผ๊ณ  ํฉ๋๋ค.

์คํ ๋ฆฌ๋ ์ปดํฌ๋ํธ์ ํน์  ์ํ, ์ฆ ๋ธ๋ผ์ฐ์ ์์ ์ค์  ๋ ๋๋ง๋ ์ํ๋ฅผ ํฌ์ฐฉํฉ๋๋ค.

ํ์ฌ `Todo` ์ปดํฌ๋ํธ์๋ ์ด๋ ๊ฒ ์ด ์ธ ๊ฐ์ง ์ํ๊ฐ ์์ต๋๋ค.

- ๊ธฐ๋ณธ ์ํ
- ๊ณ ์  ๋์์ ๋
- ์๋ฃํ์์ ๋

์ด ๊ฐ ์ํ์ ๋ํ ์คํ ๋ฆฌ๋ฅผ ์ถ๊ฐํด๋ด์๋ค.

<br />

## 3. ๊ฒ์ฆํ๊ธฐ

๊ฒ์ฆ์ ์ปดํฌ๋ํธ๊ฐ ์คํ ๋ฆฌ๋ถ์์ ์ด๋ป๊ฒ ๋ณด์ด๋์ง ๊ฐ๋ฐ์๊ฐ ์ง์  ํ๊ฐํ๋ ๊ณผ์ ์๋๋ค.

์ฆ, ๋์์ธ ๋ช์ธ์ ์ผ์นํ๋์ง ํ์ธํ๋ ์ผ์๋๋ค.

```tsx
// todo.stories.tsx
...

const mock: TodoData = {
	id: 0,
	title: "TODO",
	state: "NONE",
};

...

const longTextString =
	"Lorem, ipsum dolor sit amet consectetur adipisicing elit. Nulla libero accusamus magni harum optio eligendi, architecto iste vitae nesciunt officiis ea numquam possimus, debitis atque quidem corrupti, incidunt explicabo fugiat?";

export const LongText = Template.bind({});
LongText.args = {
	todo: {
		...mock,
		title: longTextString,
	},
};
```

์คํ ๋ฆฌ๋ฅผ ์์ฑํ๋ค ๋ณด๋ฉด ๊ทธ ์ด์ ์๋ ๋ฏธ์ฒ ๊ณ ๋ คํ์ง ๋ชปํ๋ ์๋๋ฆฌ์ค๋ ๋ ์ค๋ฆ๋๋ค.

์๋ฅผ ๋ค์ด ์ฌ์ฉ์๊ฐ ์ ๋ง ๊ธด ๋ด์ฉ์ Todo๋ฅผ ์๋ ฅํ๋ฉด ์ด๋ป๊ฒ ๋ ๊น์?

์ด๋ฐ ์์ธ์ผ์ด์ค ๋ํ ์คํ ๋ฆฌ๋ฅผ ์ถ๊ฐํด ๊ฒ์ฆํ  ์ ์์ต๋๋ค.

![TODO](./docs/todo4.png)

์์์น ๋ชปํ๊ฒ ์คํ์ผ์ด ๊นจ์ง ๊ฒ์ PR์ ์ฌ๋ฆฌ๊ธฐ ์ ์ ํ์ธํ๊ณ  ๋ฆฌ๋ทฐ์ด ๋ํ ๋์ผ๋ก ๋ฐ๋ก ํ์ธ๊ฐ๋ฅํฉ๋๋ค!

<br />

## 4. ๋์ ํ์คํธ

`Todo` ์ปดํฌ๋ํธ์์ ํด๋ฆญ ์ด๋ฒคํธ๋ฅผ ํ์ฉํ  ๋ถ๋ถ์ ์ด 3๊ฐ์๋๋ค.

- ์ฒดํฌ๋ฐ์ค๋ฅผ ํด๋ฆญํ์ ๋
- ํ์คํธ๋ฅผ ํด๋ฆญํ์ ๋
- ์ฆ๊ฒจ์ฐพ๊ธฐ(๋ณ) ๋ฒํผ์ ํด๋ฆญํ์ ๋

```tsx
const Todo = ({
  todo,
  pinned,
  onArchiveTodo,
  onEditTitle,
  onTogglePinTask,
}: TodoProps) => {
  return (
    <TodoWrapper>
      <TodoLeftBox>
        <TodoInput type="checkbox" checked={todo.checked} />

        <TodoCheckbox onClick={() => onArchiveTodo(todo.id)}>
          <FaCheck size={20} />
        </TodoCheckbox>

        <TodoContent onClick={() => onEditTitle(todo.title)}>
          {todo.title}
        </TodoContent>
      </TodoLeftBox>

      <FaStar
        onClick={() => onTogglePinTask(todo.id)}
        color={pinned ? "#FED049" : "#eee"}
      />
    </TodoWrapper>
  );
};
```

ํจ์๋ค์ ์ ๋ถ๋ชจ ์ปดํฌ๋ํธ์์ ์ฃผ์ํด์ค ๊ฒ์ด๊ธฐ ๋๋ฌธ์ ์ฌ๊ธฐ์๋ ์ธ์๊ฐ ๋ง๊ฒ ๋์ด๊ฐ๋์ง

์ด๋ฒคํธ๊ฐ ์ํ๋ ํ๊ฒ์์ ์ด๋ค์ก๋์ง ํ์ธํ  ์์ ์๋๋ค.

![TODO](./docs/todo9.gif)

์ด์  Storybook์ `action` addon์ ํ์ฉํด๋ณด๊ฒ ์ต๋๋ค. ํจ์๋ค์ด ์๋ง๊ฒ ํธ์ถ๋์๊ณ  ์ธ์ ๋ํ ํ์ธ๋์์ต๋๋ค.

## 5. ์๋์ผ๋ก ํ๊ท ํฌ์ฐฉํ๊ธฐ

์ผ๋จ ์์๋๋ก ๋ง๋ค์ด์ก์ต๋๋ค. ํ์ง๋ง ์์ผ๋ก๋ `CSS`๊ฐ ๊นจ์ง์ง ์๋๋ก ํ๋ ค๋ฉด ์ด๋ป๊ฒ ํด์ผ ๋ ๊น์?

๋งค๋ฒ ์๋์ผ๋ก ๋์ผ๋ก ํ์ธํ๊ธฐ๋ณด๋ค ์๊ฐ์  ํ๊ท ํ์คํธ ๋๊ตฌ๋ฅผ ์ฌ์ฉํ์ฌ ํ๊ท๋ฅผ ์๋์ผ๋ก ํ์ธํ๋ ๋ฐฉ๋ฒ์ ์ฌ์ฉํด๋ณด๊ฒ์ต๋๋ค.

์คํ ๋ฆฌ๋ถ์์ ๋ง๋  `chromatic`์ ์ฌ์ฉํด๋ณด๊ฒ ์ต๋๋ค.

https://www.chromatic.com/docs/setup

![TODO](./docs/todo7.png)

์ด์  ๋ก๊ทธ์ธ ํ ํ๋ก์ ํธ๋ฅผ ์์ฑํฉ๋๋ค. ํฌ๋ก๋งํฑ์ ์คํ ๋ฆฌ๋ถ์ฉ์ผ๋ก ํน๋ณํ ์ ์๋์์ผ๋ฉฐ ๋ฐ๋ก ๊ตฌ์ฑ์ด ์์ต๋๋ค.

์๋ ์ปค๋งจ๋๋ฅผ ์คํํด ํฌ๋ก๋งํฑ์ด ๊ฐ ์คํ ๋ฆฌ์ ์ค๋์ท์ ์บก์ฒํ๊ฒ ํด๋ด์๋ค.

```bash
yarn add -D chromatic

npx chromatic --project-token=[Token]
```

![TODO](./docs/todo6.png)

![TODO](./docs/todo5.png)

ํ๋ฒ ์ ์๋ํ๋์ง ํ์ธํด๋ณด๊ฒ ์ต๋๋ค.

```tsx
<TodoCheckbox onClick={onArchiveTodo}>
  <FaCheck size={20} />
</TodoCheckbox>
```

์์ด์ฝ์ ์ฌ์ด์ฆ๋ฅผ ์์ฃผ ์ฝ๊ฐ ์์ ํ๊ณ  ์ปค๋ฐํ๋ ค๊ณ  ํฉ๋๋ค. ์ด์  ํฌ๋ก๋งํฑ์์ ์ด๋ค ์์ผ๋ก ๋ณด์ฌ์ฃผ๋์ง ํ์ธํด๋ด์๋ค.

![TODO](./docs/todo8.png)

ํฌ๋ก๋งํฑ ์น์์๋ ์ปดํฌ๋ํธ๊ฐ ๋ฐ๋์๋ค๋ ๋ฉ์ธ์ง๊ฐ ์์ต๋๋ค.

![TODO](./docs/todo8-1.png)

์คํ ๋ฆฌ๋ค์ ๋ฆฌ๋ทฐํ  ์ ์๋ UI๊ฐ ๋์ต๋๋ค. ๋ง์น ๊นํ๋ธ์ PR์ฒ๋ผ ํ์ผ๋ก๋ ์ฌ์ฉ๊ฐ๋ฅํ๋ฉฐ

ํด๋น ๋ฆฌ๋ทฐ์ด๋ค์ Approve๊ฐ ์์ด์ผ๋ง Merge๋๋๋ก ํ๋ ๊ฒ๋ ๊ฐ๋ฅํฉ๋๋ค.

![TODO](./docs/todo8.gif)

์ ํฌ๊ฐ ์์ ํ ํ์ผ์ด ๋น์ฃผ์ผ์ ์ผ๋ก ์ด๋ป๊ฒ ๋ฐ๋์์ผ๋ฉฐ ์ฝ๋ ๋ํ ๊ฐ์ด ์ฌ๋ผ์ต๋๋ค.

<br />

## 6. Composition Test

    	์ปดํฌ๋ํธ ํ๋์ ๋ฒ๊ทธ๊ฐ ์ฃผ๋ณ์ ๋ค๋ฅธ ๋ถ๋ถ์๋ ์ ๋ถ ์ํฅ์ ๋ฏธ์นฉ๋๋ค.
    	๋ณตํฉ ์ปดํฌ๋ํธ๋ ๋จ์ํ ์ปดํฌ๋ํธ ์ฌ๋ฌ ๊ฐ๊ฐ ๋ชจ์ฌ ๊ตฌ์ฑ๋๋ฉฐ ์ ํ๋ฆฌ์ผ์ด์์ ์ํ์๋ ์ฐ๊ฒฐ๋ฉ๋๋ค.
    	๋ชจ๋ ํ๋์ ๊ฒฐํจ์ด ์ฌ๊ฐํ ์ค๋ฅ๋ก ํ๋๋  ์ ์์ต๋๋ค.

์ด์  ๋ง๋ค์ด์ง Todo ์ปดํฌ๋ํธ๋ค๋ก ๊ตฌ์ฑ๋  `TodoList` ์ปดํฌ๋ํธ๋ฅผ ๊ฐ๋ฐํ๋ ค ํฉ๋๋ค.

```tsx
export const TodoList = ({
  list,
  onArchiveTodo,
  onEditTitle,
  onTogglePinTask,
}: TodoListProps) => {
  const events = {
    onArchiveTodo,
    onEditTitle,
    onTogglePinTask,
  };

  return (
    <div>
      {list
        .filter((todo) => todo.pinned)
        .map((todo) => {
          return <Todo todo={todo} {...events} />;
        })}

      {list
        .filter((todo) => !todo.pinned)
        .map((todo) => {
          return <Todo todo={todo} {...events} />;
        })}
    </div>
  );
};
```

```tsx
import { ComponentStory, ComponentMeta } from "@storybook/react";
import { TodoList } from ".";
import Todo from "../todo/todo.stories";

export default {
  title: "component/Todo List",
  component: TodoList,
  argTypes: {
    ...Todo.argTypes,
  },
} as ComponentMeta<typeof TodoList>;

const Template: ComponentStory<typeof TodoList> = (args) => (
  <TodoList {...args} />
);

export const Default = Template.bind({});
Default.args = {
  list: [
    { id: "1", checked: false, title: "Build a date picker" },
    { id: "2", checked: false, title: "QA dropdown" },
    {
      id: "3",
      checked: false,
      title: "Write a schema for account avatar component",
    },
    { id: "4", checked: false, title: "Export logo" },
    { id: "5", checked: false, title: "Fix bug in input error checked" },
    { id: "6", checked: false, title: "Draft monthly blog to customers" },
  ],
};
```

๊ฐ์ props์ key์ ํ์์ด๋ผ๋ฉด ๋ค๋ฅธ ์คํ ๋ฆฌ์ argType์ ๋ณต์ฌํ  ์ ์์ต๋๋ค.

์ด์  ์คํ ๋ฆฌ์์ ๋ณตํฉ ์ปดํฌ๋ํธ์ ๋์์ด ์ ๋๋์ง ํ์ธํด๋ด์๋ค.

![TODO](./docs/todo10.gif)

<br />

## 7. ๋ณตํฉ ์ปดํฌ๋ํธ ์ํ Mocking

`TodoApp` ์ปดํฌ๋ํธ์์ fetchํ todo์ ๋ฐ์ดํฐ๋ฆฌ์คํธ๋ฅผ ์ํ๋ก ๊ด๋ฆฌํ๊ณ ์ ํฉ๋๋ค. 

API ์์ฒญ, ์ํ, ์ปจํ์คํธ, ํ๋ก๋ฐ์ด๋ ๋ฑ ์ปดํฌ๋ํธ๊ฐ ์์กดํ๋ ๋ชจ๋  ์ํฉ์ mockingํ  ์ ์์ต๋๋ค.

์ฌ๊ธฐ์๋ `Mock Service Worker` ์ ๋์จ์ ํตํด ๋คํธ์ํฌ ๋ ๋ฒจ์์ ์์ฒญ์ ๊ฐ๋ก์ฑ Mocking Response๋ฅผ ๋ฐํํ๊ฒ ํด๋ณด๊ฒ ์ต๋๋ค.

```bash
yarn add -D msw msw-storybook-addon
npx msw init public/ 
```

public ํด๋์์ `mockServiceWorker.js` ํ์ผ์ด ์์ฑ๋์์ผ๋ฉด ์คํ ๋ฆฌ๋ถ ํ๊ฒฝ์๋ ์ถ๊ฐ ์ธํ์ ํด์ค์ผ ํฉ๋๋ค.

```js
// .storybook/preview.js
import { initialize, mswDecorator } from 'msw-storybook-addon';

initialize();

export const parameters = {
  actions: { argTypesRegex: '^on[A-Z].*' },
  controls: {
    matchers: {
      color: /(background|color)$/i,
      date: /Date$/,
    },
  },
};

export const decorators = [Story => <Story />, mswDecorator];
```

```tsx
// todo-app.stories.tsx
import {rest} from "msw";
...
export const TodoDefault = Template.bind({});
TodoDefault.parameters = {
  msw: {
    handlers: [
      rest.get('/todo', (req, res, ctx) => {
        return res(ctx.json(TodoListDefault.args));
      }),
    ],
  },
};
```

ํด๋น ์ปดํฌ๋ํธ์์ ์ผ์ด๋๋ fetching์ `msw`๊ฐ ์ธํฐ์ํธํ์ฌ ๋ชจ์ ๋ฐ์ดํฐ๋ฅผ ๋์  ์ ๊ณตํด์ค๋๋ค.

![TODO](./docs/todo11.png)

Mocking๋ ๋ฐ์ดํฐ๊ฐ ๋ค์ด์จ ๊ฒ์ ๋คํธ์ํฌ ํญ๊ณผ ์ฝ์์์ ๋ ๋ค ํ์ธํ  ์ ์์ต๋๋ค!

## 8. ์ปดํฌ๋ํธ ์ธํฐ๋ ์ ํ์คํธํ๊ธฐ

    UI๋ ํ๋ฉด์์ผ๋ก ์ฌ์ฉ์๋ค์ด ๋์ผ๋ก ๋ณด๊ณ  ์ํธ์์ฉํฉ๋๋ค. ๋ํ ๊ทธ ์์ ๋ณด๋ฉด ์ ๋ณด์ ์ด๋ฒคํธ์ ํ๋ฆ์ด ์ ๋์๋๋๋ก ์ฐ๊ฒฐ๋์ด ์์ต๋๋ค.

`TodoApp`์์ ์ฌ์ฉ์๋ ์ผ์ ์ ๊ณ ์ ์ํค๊ธฐ ์ํด ๋ณ ์์ด์ฝ์ ํด๋ฆญํ  ์ ์์ต๋๋ค. ๋๋ checkbox๋ฅผ ํด๋ฆญํด ์๋ฌด๋ฅผ ์ํํ๋ค๊ณ  ์๋ฃํ  ์๋ ์์ต๋๋ค.

์ฌ์ฉ์๊ฐ ๋ฒํผ์ ๋๋ฌ ์ํธ์์ฉ์ ํ๋ฉด ์ด๋ฌํ ์ํ์ ๋ณํ์ ๋ ๋๋ง๋ UI๊ฐ ์๋ฐ์ดํธ๋๋ ๊ฒ์ด ํ๋์ ์ฃผ๊ธฐ์๋๋ค. 

์ฐ๋ฆฌ๋ ์ด๋ฌํ ๋ชจ๋  ์ํ์์ ์ปดํฌ๋ํธ๊ฐ ์ฌ๋ฐ๋ฅด๊ฒ ๋ณด์ด๊ณ , ํด๋นํ๋ ์ธํฐ๋ ์์ ๋ฐ์ํ๋์ง๋ ๋ณด์ฅํด์ผํฉ๋๋ค.

### Test Runner

์ํธ์์ฉ ํ์คํธ๋ ๋ชจ์ ๋ฐ์ดํฐ๋ฅผ ์ ๊ณตํ์ฌ ํ์คํธ ์๋๋ฆฌ์ค๋ฅผ ์ค์ ํ๊ณ  Testing Library๋ฅผ ์ฌ์ฉํ์ฌ ์ธํฐ๋ ์์ ์๋ฎฌ๋ ์ด์ํ๊ณ  ๊ฒฐ๊ณผ๋ก ๋ ๋๋ง๋ DOM์ ํ์ธํ๋ ๋ฐฉ์์ผ๋ก ์งํ๋ฉ๋๋ค.

```bash
yarn add -D @storybook/testing-library @storybook/jest @storybook/addon-interactions @storybook/test-runner
```

์ค์น ํ ์คํ ๋ฆฌ๋ถ `main.js`๋ ์์ ํด์ค๋๋ค.

```js
// .storybook/main.js
module.exports = {
    ...,
    addons: [
      ...
              '@storybook/addon-interactions',
    ],
    features: {
      interactionsDebugger: true,
    },
    ...
}
```

package.json์ ์คํฌ๋ฆฝํธ์๋ ์คํ ๋ฆฌ๋ถ์ ํ์คํธ ์คํ ์ปค๋งจ๋๋ฅผ ์ถ๊ฐํด์ฃผ์ญ์๋ค.

```json
...
"script": {
  "test-storybook": "test-storybook"
}
...
```

### testing-library / jest

ํ์คํ ๋ผ์ด๋ธ๋ฌ๋ฆฌ ๋ ํด๋ฆญ, ๋๋๊ทธ, ํญ, ํ์ดํ ๋ฑ ์ฌ์ฉ์ ์ํธ ์์ฉ์ ์๋ฎฌ๋ ์ด์ํ๊ธฐ ์ํ ํธ๋ฆฌํ API๋ฅผ ์ ๊ณตํฉ๋๋ค. 

๋ฐ๋ฉด์ Jest๋ ์ ์ธ ์ ํธ๋ฆฌํฐ๋ฅผ ์ ๊ณตํฉ๋๋ค.



### ํ์คํธ ์ฝ๋

```tsx
export const TodoAppPinTask = Template.bind({})
TodoAppPinTask.parameters = TodoDefault.parameters;
TodoAppPinTask.play = async ({ canvasElement }) => {
    const canvas = within(canvasElement);
    const getTask = (name: string) => canvas.findByRole('listitem', {name})

  // // Find the todo to pin
  const itemToPin = await getTask('Build a date picker')


  // Find the pin button
  const pinButton = await findByRole(itemToPin,'button' , { name: 'pin' });

  // Click the pin button
  await userEvent.click(pinButton);

  // Check that the pin button is now an unpin button
  const unpinButton = within(itemToPin).getByRole('button' , { name: 'unpin' });
  await expect(unpinButton).toBeInTheDocument();
}
```

storybook์ `play` ํจ์๋  ์คํ ๋ฆฌ์ ์ต์์ ์ปจํ์ด๋์ธ ์บ๋ฒ์ค ์์๋ฅผ ๋ฐ์ต๋๋ค. 

์ด ์์ ๋ด์์๋ง ์ฟผ๋ฆฌ์ ๋ฒ์๋ฅผ ์ง์ ํ์ฌ DOM ๋ธ๋๋ฅผ ์ฐพ์ ์ ์์ต๋๋ค. 

๋ํ `interaction` addon์์ ๋๋ฒ๊น์ด ๊ฐ๋ฅํ๋ฉฐ ์บ๋ฒ์ค์ ์ค์ ๋ก ๊ทธ๋ ค์ง DOM ๋ํ

ํ์คํธ์ step๋ณ๋ก ํ์ธ ๊ฐ๋ฅํฉ๋๋ค.


**๊ฒฐ๊ณผ๋ฌผ**

![TODO](./docs/todo12.gif)


### ํ์คํธ ์ฝ๋ ํ๋ก์ธ์ค ์๋ํ

์คํ ๋ฆฌ๋ถ์ ํด๋น ์คํ ๋ฆฌ๋ฅผ ๋ณผ ๋๋ง ์ธํฐ๋ ์ ํ์คํธ๋ฅผ ์คํํฉ๋๋ค. 

๋ณ๊ฒฝํ  ๋๋ง๋ค ์คํ ๋ฆฌ๋ถ์ ๊ฒํ ํ๋ ๊ฒ์ ํ๋ค๊ธฐ ๋๋ฌธ์ `Playwright`์์ ์ ๊ณต๋๋ ์ ํธ๋ฆฌํฐ๋ก 

ํ๋ฒ์ ํ์ธํด๋ด์๋ค.

```bash
yarn test-storybook --watch
```

![TODO](./docs/todo13.png)

์๋ฌ๊ฐ ๋ ์คํ ๋ฆฌ๋ก ๋งํฌ๊น์ง ์ ๊ณตํฉ๋๋ค! 


## 9. ์ ๊ทผ์ฑ ํ์คํธํ๊ธฐ

์๊ฐ, ์ฒญ๊ฐ, ์ด๋์ฑ, ์ธ์ง, ๋ฐํ ๊ทธ๋ฆฌ๊ณ  ์ ๊ฒฝํ์ ์ธ ์ฅ์ ๋ค๋ก ์ธํด ๋ค์๊ณผ ๊ฐ์ ์ฑ ์๊ตฌ์ฌํญ์ด ๋ฐ์ํฉ๋๋ค.

- โจ ํค๋ณด๋ ๋ค๋น๊ฒ์ด์
- ๐ฃ ์คํฌ๋ฆฐ ๋ฆฌ๋๊ธฐ ์ง์
- ๐ ํฐ์น ์นํ์ฑ
- ๐จ ์ถฉ๋ถํ ๋์ ์ ๋๋น
- โก๏ธ ๋ชจ์ ๊ฐ์
- ๐ ํ๋

๊ณผ๊ฑฐ์๋ ๋ธ๋ผ์ฐ์ , ์ฅ์น ๋ฐ ์คํฌ๋ฆฐ ๋ฆฌ๋๊ธฐ์ ์กฐํฉ์์ ๋ชจ๋  ์ปดํฌ๋ํธ๋ฅผ ๊ฒ์ฌํ์ต๋๋ค.

๊ทธ๋ฌ๋ ์ค์  ๊ฐ๋ฐ์์๋ ์์ค๊ธ์ ์ ๊ทผ์ฑ ์ง์์ ๊ฐ์ง ๊ฐ๋ฐ์์ ๊ทธ๋งํ ๊ณต์๋ฅผ ๋ค์ผ ์๊ฐ์ด ์ถฉ๋ถํ์ง ์๊ธฐ ๋๋ฌธ์ 

์ด๋ฅผ ์ํด ์๋ํ QA ๋๊ตฌ๋ค์ด ๋์์ต๋๋ค.

์ฌ๊ธฐ์ ์จ๋ณผ `Axe`์ ๊ฒฝ์ฐ์๋ WCAG ์ด์์ 57%๋ฅผ ์๋์ผ๋ก ๋ฐ๊ฒฌํ๋ค๊ณ  ์๋ ค์ ธ ์์ต๋๋ค.

๋๋ถ๋ถ์ ๊ธฐ์กด ํ์คํธ ํ๊ฒฝ๊ณผ ํตํฉ๋๋ฏ๋ก `jest-axe Intergation`, `Storybook` ์ ๋์จ ๋ฑ์ ์ฌ์ฉํ์ฌ ๊ฒ์ฌํฉ๋๋ค.

### code

```bash
yarn add -D @storybook/addon-a11y
```

์ค์น ํ `storybook/main.js`์ ์ ๋์จ ํญ๋ชฉ์๋ ์ถ๊ฐํด์ค์๋ค.

![TODO](./docs/todo14.png)

์ด์  ์คํ ๋ฆฌ๋ถ์ ํญ์์ ์ ๊ทผ์ฑ ์ ๋์จ์ด ๋์ค๋ ๊ฑธ ํ์ธํ  ์ ์์ต๋๋ค.


```bash
yarn add -D axe-playwright
```

์ด์  ํ์คํธ ๋ฌ๋๋ฅผ ์ด์ฉํ์ฌ ํ๊ท๋ก ์ ๊ทผ์ฑ์ด ๊นจ์ง๋์ง ์ค์๊ฐ์ผ๋ก ๊ฒ์ฌํ๋ฉฐ ๊ฐ๋ฐํด๋ด์๋ค.

```js
// .storybook/test-runner.js
const { injectAxe, checkA11y } = require('axe-playwright');

module.exports = {
 async preRender(page, context) {
   await injectAxe(page);
 },
 async postRender(page, context) {
   await checkA11y(page, '#root', {
     detailedReport: true,
     detailedReportOptions: {
       html: true,
     },
   })
 },
};
```

์๋ก์ด ํ์ผ์ ์์ฑํ์ฌ ์คํ ๋ฆฌ๋ถ์ด ํ์ฉํ  ํ์คํธ๋ฌ๋ ์ฝ๋๋ฅผ ์์ฑํด์ฃผ์ญ๋ค.

```bash
yarn test-storybook --watch

Watch Usage
 โบ Press a to run all tests.
 โบ Press f to run only failed tests.
 โบ Press q to quit watch mode.
 โบ Press p to filter by a filename regex pattern.
 โบ Press t to filter by a test name regex pattern.
 โบ Press Enter to trigger a test run.
No tests found related to files changed since last commit.
Press `a` to run all tests, or run Jest with `--watchAll`.
```

a๋ฅผ ๋๋ฌ ํ๋ฒ ์ ๊ฒํด๋ณด๋ฉด ์ ๋ ๋ฏธ์ฒ ์ด์ด๋ณด์ง ๋ชปํ ์คํ ๋ฆฌ๋ค์ ์ ๊ทผ์ฑ ์ด์๋ฅผ ํ์ธํ  ์ ์์ต๋๋ค.

![TODO](./docs/todo15.png)

<br />

## 10. USER FLOW ํ์คํธํ๊ธฐ

์ด์  ํ๋ก๋์์ ์ฌ๋ฆฌ๊ธฐ ์ ์ ์ ์ฒด์ ์ ํ๋ฆ์ ๊ฒ์ฆํ๊ณ  ํตํฉ ๋ฌธ์ ๋ค์ ํ์ํด๋ด์ผ ํฉ๋๋ค. (`E2E TEST`)

E2E ํ์คํธ๋ฅผ ์คํํ๋ ค๋ฉด ์์ฉ ํ๋ก๊ทธ๋จ์ ์ ์ฒด ์ธ์คํด์ค๋ฅผ ๊ฐ๋์ํค๋ ๊ฒ๋ถํฐ ์์ํฉ๋๋ค. 

๊ทธ๋ฐ ๋ค์ `Cypress`, `Playwright` ๋๋ `Selenium๊ณผ` ๊ฐ์ ๋๊ตฌ๋ฅผ ์ฌ์ฉํ์ฌ ์ฌ์ฉ์ ๋์์ ์๋ฎฌ๋ ์ด์ํ์ฌ ์ฌ์ฉ์ ํ๋ฆ์ ํ์ธํฉ๋๋ค.

E2E ํ์คํธ๋ฅผ ์ํด ํ์คํธ ์ธํ๋ผ์์ ์ดํ๋ฆฌ์ผ์ด์์ ๊ฐ๋ํ  ๋๋ ๋ณดํต ๋๊ฐ์ง ์ต์์ด ์์ต๋๋ค.


- **์ ์ฒด ํ์คํธ ํ๊ฒฝ์ ์ ์ง**: ์ฌ๊ธฐ์๋ ํ๋ฐํธ์๋, ๋ฐฑ์๋, ์๋น์ค ๋ฐ ์๋ ํ์คํธ ๋ฐ์ดํฐ๊ฐ ํฌํจ๋ฉ๋๋ค. ์๋ฅผ ๋ค์ด, O'Reilly ํ์ Docker๋ฅผ ์ฌ์ฉํ์ฌ ์ ์ฒด ์ฑ ์ธํ๋ผ๋ฅผ ๊ฐ๋ํ๊ณ  E2E ํ์คํธ๋ฅผ ์คํํฉ๋๋ค.

- **๋ชจ์ ๋ฐฑ์๋์ ์ง์ง์ด์ง ํ๋ฐํธ์๋ ์ ์ฉ ํ์คํธ ํ๊ฒฝ์ ์ ์ง**: ์๋ฅผ ๋ค์ด, Twilio๋ ๋คํธ์ํฌ ์์ฒญ์ ๋ชจ์ฌํ๊ธฐ ์ํด ์ฌ์ดํ๋ ์ค(Cypress)๋ฅผ ์ฌ์ฉํ์ฌ ํ๋ฆ์ ํ์คํธํฉ๋๋ค.

## code

```bash
yarn add -D cypress
```

https://storybook.js.org/tutorials/ui-testing-handbook/react/ko/user-flow-testing/



# ๋ง๋ฌด๋ฆฌ 


![TODO](./docs/todo16.png)

E2E ํ์คํธ๊น์ง ๋ง์น๊ณ  ๋์๋ CI ์๋ฒ์์ ๊นํ๋ธ ์ก์์ ํ์ฉํ์ฌ ํ์คํธ๋ฅผ ์๋ํํด์ฃผ๋ ๊ณผ์ ์ด ์์ต๋๋ค.

์  ๋ชจ๋  ํ์คํธ๋ฅผ ํต๊ณผํ๊ณ  ๋์์ผ PR์ด merge๋  ์ ์๊ฑฐ๋ ํจํค์ง๋ผ๋ฉด ํผ๋ธ๋ฆฌ์ฑ์ด ๊ฐ๋ฅํ  ๊ฒ์๋๋ค.










