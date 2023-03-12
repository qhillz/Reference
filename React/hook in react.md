What can you do if you want to use Hooks logic inside a class component, but there’s no option to rewrite that class to Hook?

If you’re impatient and want to jump straight to the solution, click [here](https://infinum.com/blog/how-to-use-react-hooks-in-class-components/#solution). Otherwise, just keep reading.

## Introduction

When I first heard about Hooks, I couldn’t be more excited. I was reading the documentation, and it seemed like magic – a function component that is feature-packed like an actual class component? Problems like no lifecycle methods nor a state in functions; or complex syntax and low reusability of some internal logic in classes are gone.

Complex patterns like render-props or HOCs (Higher Order Components) also aren’t necessary anymore. Not only that makes the code cleaner, it also makes it much less prone to errors. The decision of a wrong approach when picking a component type isn’t a problem anymore – Hook function is everything that you’ll ever need.

Reusability of complex logic also drastically improves, since we now have an option to pack features like state, and ‘lifecycle methods’ (quotes will be explained later in the article) directly into a function. This creates much needed space for something that was impossible to implement before Hooks. Util functions become much more powerful, and they’re also reusable not only in the whole project but also across many different projects. The logic they’re implementing can be totally generic.

What I was most excited about is combining various Hook functions into more powerful ones. Those functions can also be combined, again, into ones even more powerful. There’s literally no limit! Believe me, after you start using Hooks, you’ll wonder how were you ever able to live, and code, without them.

## The problem

If everything is so beautiful and magical, what’s the problem? I don’t see any problems in the future when the community adopts Hooks. But what about now?

Your situation is that you want to use some Hook logic in your project which is mostly class-based, and it’s **not an option to rewrite those class components to Hooks at the moment**. Your classes can just be too complex, or it could break many other things across the project if you change it. Business value of such an approach is also questionable.

![Hooks official docs](https://wp-assets.infinum.com/uploads/2019/06/how-to-use-react-hooks-in-class-components-1.png)

This implies Hooks **aren’t just a small feature** to make your project development a bit easier. Hooks are a new **core concept**. The mindset about their usage is different than the one from classes, and you have to shift your mindset to understand it. But hey, once you start doing that, you’ll see that the new approach makes much more sense, and that staying on class components won’t have a huge value in the future.

React team is also talking about the upcoming function optimizations, so the decision of a class component instead of a function one might have a bad performance impact on your app in the long run.

That still doesn’t solve our problem. Let’s say you somehow have to use that **Hook logic inside of a class**. That’s totally in conflict with the statement in their docs. But, as with everything in JavaScript world, there is a solution. You can use Hooks logic inside classes in a valid way, without breaking any of React rules.

## Solution

I’ve created a simple `useScreenWidth` Hook as an example. As you can see from the Hook name, its purpose is getting the actual screen width. So, let’s jump into the code:

```typescript
import { useEffect, useState } from ’react’;

export function useScreenWidth(): number {
  const [width, setWidth] = useState(window.innerWidth);

  useEffect(() => {
    const handler = (event: any) => {
      setWidth(event.target.innerWidth);
    };

    window.addEventListener(’resize’, handler);

    return () => {
      window.removeEventListener(’resize’, handler);
    };
  }, []);

  return width;
}
```

`useState` and `useEffect` are some of the React built-in Hooks. `useState` works in a way that it returns two values: one is the state value, and the other one is its setter. By array destructuring, you can set the name of those two values to anything you like. `<variable_name>` and `set<variable_name>` is the common naming. As an argument, you pass in an initial value – in our case, that’s the current screen width.

`useEffect` is a hook function which takes two arguments as input: the first one is a function to call, and the second one is an array of ‘Calling objects’. This means we can pass a number of objects in that array, and the effect will be applied (or in other words, argument function will be called) only if at least of the values inside an array changes on the next render. E.g. we can pass several values as a second argument:

- No argument at all – `useEffect` will be called on every render.
- `[]` – `useEffect` will be called only at the first render, since empty brackets can never change.
- `[arg1, arg2, … , argN]` – `useEffect` will be called if any of the values inside of an array has changed. (처음 렌더링 될때는 무조건 실행됨.)

Depending on the second parameter, `useEffect` can imitate class lifecycle methods. E.g. if we put `[]` as a second argument, function will be called only after the first render, and that way it imitates `componentDidMount`. Now’s the perfect time to explain the quotes in the ‘lifecycle methods’ from the introduction.

As written above, **mindset about hooks is different than in classes**, and that’s why there are no lifecycle methods at all, and one should not look at Hooks in that way. `useEffect` should be considered more as a side effect, which takes effect when some variable changes. That why it’s OK to say that putting `[]` as a second argument will imitate `componentDidMount`, and give your app the same behavior, but it’s important to understand these two are **not the same** thing.

`useEffect` can have a blog post for itself. Luckily, Dan Abramov wrote a nice [article](https://overreacted.io/a-complete-guide-to-useeffect/) about it, so check it out later for more information.

## Using Hook as HOC

HOC is advanced React technique for reusing component logic, and its concept gives us the ability to use Hook logic inside our existing class component. The idea is to get a component as an input, and return that same component with some additional props. In our case, we will pass our Hook function as a prop.

```js
<span data-es-language="js"></span>x
import React from ’react’;
import { useScreenWidth } from ’../hooks/useScreenWidth’;

export const withHooksHOC = (Component: any) => {
  return (props: any) => {
    const screenWidth = useScreenWidth();

    return <Component width={screenWidth} {...props} />;
  };
};
```

The final step is to simply wrap our existing class component with that HOC. And then, we simply use `width` prop as any other prop passed to the component.

```js
<span data-es-language="js"></span>x
import React from ’react’;
import { withHooksHOC } from ’./withHooksHOC’;

interface IHooksHOCProps {
  width: number;
}

class HooksHOC extends React.Component<IHooksHOCProps> {
  render() {
    return <p style={{ fontSize: ’48px’ }}>width: {this.props.width}</p>;
  }
}

export default withHooksHOC(HooksHOC);
```

This doesn’t break any of the Hooks rules because we’re using an actual Hook in a function – just as we should. There’s nothing wrong with passing that logic as a prop.

## Using Hook as render prop

There’s another legit way to accomplish the goal:

```typescript
import { FunctionComponent } from ’react’;
import { useScreenWidth } from ’../hooks/useScreenWidth’;

type ScreenWidthChildren = (screenWidth: number) => any;

interface IScreenWidthProps {
  children: ScreenWidthChildren;
}

export const ScreenWidth: FunctionComponent<IScreenWidthProps> = ({
  children,
}) => {
  const screenWidth: number = useScreenWidth();

  return children(screenWidth);
};
```

We’ve now created a FunctionComponent, which takes children as an argument. After using the Hook logic inside of it, we return the desired result as a children function. After that, the logic is quite simple: import the created FunctionComponent inside your existing class, and pass down its children as render prop.

```js
<span data-es-language="js"></span>x
import React from ’react’;
import { ScreenWidth } from ’./ScreenWidth’;

export class HooksRenderProps extends React.Component {
  render() {
    return (
      <ScreenWidth>
        {(width) => <p style={{ fontSize: ’48px’ }}>width: {width}</p>}
      </ScreenWidth>
    );
  }
}
```

## Final words

Hooks are a powerful change in the React world, and they will definitely change our mindset about React development. It might not seem so straightforward right now, but in a couple of years, class usage will slowly decrease. It’s great that React team doesn’t force us to rewrite all our projects, and also encourages us to use Hooks side by side with classes. They won’t deprecate classes in the near future, so we certainly have the time to experiment with Hooks.

Having ways to use Hooks logic directly in classes (like those shown in this article) is just another plus for experimenting with Hooks. Thanks for reading and happy coding!

We’re also hooked on the clever cover illustration by Marijana Šimag.