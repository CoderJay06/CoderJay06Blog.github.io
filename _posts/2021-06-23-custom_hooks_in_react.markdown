---
layout: post
title:      "Custom Hooks in React"
date:       2021-06-24 01:20:14 +0000
permalink:  custom_hooks_in_react
---

![Hook](https://i.imgur.com/uRFtGLm.jpeg)

I'm going to assume you know the basics about hooks in React but if not or you'd like to dive a bit deeper into this concept check out the links at the end of this blog. So what are custom hooks? If you've used earlier versions of React you've probably come across patterns like higher-order components and render props (you can read about these in my previous blogs, [higher-order components](https://dev.to/coderjay06/higher-order-components-in-react-52d0), and [render props](https://dev.to/coderjay06/render-props-26m5) ). These patterns (just like hooks) let you reuse stateful logic in your React components, though hooks offer a less complex way to achieve the same result of reusability. With custom hooks, we can make our own hooks and customize them to contain whatever logic we choose to add to them. This gives us more flexibility to solve a specific problem we might have.
## Creating Custom Hooks
Let's start with an example of when you might feel the need to create a custom hook. Say we wanted to add a timer to our React application we're building. We can simply just build it within our component that needs to use it and we're good to go right!? But what if we needed to reuse our timer across several components? This would be a great opportunity for a custom hook! So to create our custom hook we should always start with the word *use* followed by a relevant name for it. In this case, we'll call it *useTimer*. Then we can import any of the built-in react hooks that we'll need inside of our custom one.
```
import {useState, useEffect} from "react"

export default function useTimer() {
    const [timer, setTimer] = useState(0)
    
    // use useEffect to update state when timer starts
    useEffect(() => {
        let timerId = setInterval(() => {
                setTimer(timer + 1) 
            }, 1000)
        
        // clean up after timer
        return () => clearInterval(timerId)
    
    })
    
    return timer
}

```
Now with this this code, anywhere a timer is needed within our app we just import our custom `useTimer()` hook and display it within our component. In this case the `Timer` component.

```
import React from "react"
import useTimer from "./useTimer"

function Timer() {
    const timer = useTimer()
    
    
    return (
        <>
            <h1>Seconds: {timer}</h1>
        </>
    )
}

export default Timer
```
Here we're just rendering the return value from the `useTimer()` hook we've just created. This timer updates each time the `setInterval()`  inside of  `useEffect()` is invoked. 
## Summary
Custom hooks are great for reusing the business logic across your React application. When you need something less abstract and a bit more tailored towards your component they can come in handy. Instead of just using built-in hooks we can have more flexibility by adding customized code into a reusable hook.
### More resources 
* [React Hooks](https://reactjs.org/docs/hooks-intro.html)
* [Building your own hooks](https://reactjs.org/docs/hooks-custom.html)
