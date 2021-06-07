---
layout: post
title:      "Render Props"
date:       2021-06-07 12:00:42 +0000
permalink:  render_props
---


To follow my last blog where I talked about [Higher Order Components in React](https://coderjay06.github.io/higher_order_components_in_react), I'll now explain the more commonly used technique over HOCs(Higher Order Components)  called [render props](https://reactjs.org/docs/render-props.html#gatsby-focus-wrapper). Render props is a reusability technique in React for sharing common data across components through props using functions as values. The component receiving it has knowledge of what to render through this function prop. Going back to the example in my previous blog, which you can find [here](https://coderjay06.github.io/higher_order_components_in_react), I'll show how we can refactor this code to use render props instead of the higher-order component technique.

## Using render props
If you have more than one component with similar state and logic, you might want to think about how they can share it with each other. *Nobody likes greedy components! *To take our toggle feature for our like button and comment form component as an example, we realize this same reusability can be implemented through the render props technique. All we need to do is extract the logic from our components and place it in a single wrapper component.

```
class TogglerWrapper extends React.Component {
    state = {
        on: false
    }
		
    toggle = () => {
        this.setState(prevState => ({
            on: !prevState.on
        }))
    }
		
    render() {
        return (
            <div>
				{this.props.render({
                    on: this.state.on,
                    toggle: this.toggle
                })}
            </div>
        )
    }    
}

export default TogglerWrapper
```

I find this to be a much simpler approach than the HOC pattern which uses some extra functionality to accomplish the same task. All we're doing is returning `this.props.render` with all our toggle logic contained inside as an object. This can also be done by simply passing in the state and method like so:  `this.props.render(this.state.on, this.toggle)` . Now we can import our toggler wrapper component wherever we'd like to use it! 

```
// ./CommentForm.js
import TogglerWrapper from "./TogglerWrapper"

class CommentForm extends React.Component {
    render() {
        return (
            <TogglerWrapper render={
                ({on, toggle}) => (
                    <div>
                        <button onClick={toggle}>{on ? "Hide " : "Show "}Comment</button>
                        <form style={{ display: on ? "block" : "none" }}>
                            <input id="comment" type="text" />
                            <input type="submit" value="Add" />
                        </form>
                    </div>
                )
            }/>
        )
    }
}

export default CommentForm

// .LikeButton.js
import TogglerWrapper from './TogglerWrapper'

class LikeButton extends React.Component {
    render() {
        return (
            <TogglerWrapper render={
                ({on, toggle}) => (
                     <div onClick={toggle}>
                        { on ? "👍" : "👎" }
                    </div>
                )
            }/>
        )
    }
}

export default LikeButton
```
Here we are utilizing the `TogglerWrapper`  render prop to invoke a function within it when the outer component is mounted. The functions parameter list contains our `on` state and `toggle` method being destructured from the object passed in. So whenever the user clicks on either the like or comment form buttons, the toggle method will be triggered, updating our on state for that component. 

Another way we can implement the render props pattern for our toggle feature would be to render our components inside of the App component. Just Import our toggler wrapper, use it to wrap both components separately, and execute the render prop function to implicitly return each component. 

```
// ./App.js
import CommentForm from "./CommentForm"
import LikeButton from "./LikeButton"
import TogglerWrapper from "./TogglerWrapper"

function App() {
    return (
        <div>
            <TogglerWrapper render={
                ({on, toggle}) => <CommentForm on={on} toggle={toggle} /> 
            }/>
            <br/>
            <TogglerWrapper render={
                ({on, toggle}) => <LikeButton on={on} toggle={toggle} /> 
            }/>
        </div>
    )
}
export default App

// ./CommentForm.js
function CommentForm(props) {
    const { on, toggle } = props
    return (
        <div>
            <button onClick={toggle}>{on ? "Hide " : "Show "}Comment</button>
            <form style={{ display: on ? "block" : "none" }}>
                <input id="comment" type="text" />
                <input type="submit" value="Add" />
            </form>
        </div>
    )
}
export default CommentForm

// ./LikeButton.js
function LikeButton(props) {
    const { on, toggle } = props
    return (
        <div onClick={toggle}>
            { on ? "👍" : "👎" }
        </div>
    )
}
export default LikeButton
```
This gives us the same toggle functionality as the prior example so it is just a matter of preference for choosing one style over the other.

## Summary
Render props are usually preferred over higher-order components though they can both be used to achieve the same goal of reusability. A more common solution these days would be to use react hooks but all of these patterns have their place in React land so they can still be useful tools to have under your belt depending on what problem you're trying to solve.

### More resources
* [Render Props (React docs)](https://reactjs.org/docs/render-props.html)
* [React Render Props Made Simple!](https://www.youtube.com/watch?v=3IdCQ7QAs38)

