---
layout: post
title:      "Higher Order Components in React"
date:       2021-05-31 07:33:11 -0400
permalink:  higher_order_components_in_react
---

There are several patterns for implementing reusability with react components. One such pattern that's considered a bit more of an advanced technique is the higher-order component pattern. In this blog I'll refer to them as HOCs. 


## What's a HOC?
Before hooks and render props, the HOC pattern was more commonly used then they are now but it's still a useful technique to have in your toolbox as a React developer. So what are Hocs? For a basic definition of HOCs, the React docs state, *"a higher-order component is a function that takes a component and returns a new component" - reactjs.org* . The HOC technique comes from the prefered way to utilize code reuse in React which is composition over inheritence.

An example of when the HOC technique can be useful to you is if you have several components with similar logic to each other. 
Say you have a comment form that is hidden until the user clicks on the show button and a like button that also changes its state when the user clicks. For this example we'll have a CommentForm and LikeButton component.

```
// ./CommentForm.js
class CommentForm extends React.Component {
    state = {
        on: false
    }
		
    toggleForm = () => {
        this.setState(prevState => ({
            on: !prevState.on
        }))
    }
		
    render() {
        return (
            <div>
                <button onClick={this.toggleForm}>{this.state.on ? "Hide " : "Show "}Comment</button>
                <form style={{ display: this.state.on ? "block" : "none" }}>
                    <input id="comment" type="text" />
                    <input type="submit" value="Add" />
                </form>
            </div>
        )
    }
}

// ./LikeButton.js
class LikeButton extends React.Component {
    state = {
        on: false
    }
		
    toggleLike = () => {
        this.setState(prevState => ({
            on: !prevState.on
        }))
    }
		
    render() {
        return (
            <div onClick={this.toggleLike}>
                { this.state.on ? "👍" : "👎" }
            </div>
        )
    }
}
```

Here we have duplicated methods for our toggle functionality, breaking the rule of Dont repeat yourself (DRY). The HOC technique could be a handy solution to this situation. If we instead make a component that contains this repeated logic,  takes in each of our components as an argument and returns a new one we could solve our problem.

```
// ./withToggler.js
class Toggler extends React.Component {
    state = {
        on: false
    }
		
    toggle = () => {
        this.setState(prevState => ({
            on: !prevState.on
        }))
    }
		
    render() {
        const WrappedComponent = this.props.component
        return (
            <div>
                    {/* here we render the wrapped compnent with the new data */}
                    {/* any additional props are passed through with ...this.props */}
                <WrappedComponent on={this.state.on} toggle={this.toggle} {...this.props} />
            </div>
        )
    }    
}

export function withToggler(component) {
    return (props) => {
        return (
            <Toggler component={component} {...props} />
        )
    }
}
```

Then all we need to do is import our HOC into each of our components so they can be passed in as the component to be wrapped by our `withToggler` giving them access to the toggle logic.

```
// ./CommentForm.js
import {withToggler} from "./withToggler"

class CommentForm extends React.Component {
    render() {
        return (
            <div>
                <button onClick={this.props.toggle}>{this.props.on ? "Hide " : "Show "}Comment</button>
                <form style={{ display: this.props.on ? "block" : "none" }}>
                    <input id="comment" type="text" />
                    <input type="submit" value="Add" />
                </form>
            </div>
        )
    }
}

export default withToggler(CommentForm)

// ./LikeButton.js
import {withToggler} from './withToggler'

class LikeButton extends React.Component {
    render() {
        return (
            <div onClick={this.props.toggle}>
                { this.props.on ? "👍" : "👎" }
            </div>
        )
    }
}

export default withToggler(LikeButton)
```

Now our toggle logic is contained within one component and it can be easily shared across multiple other components. This gives our application much more flexibility. And since HOCs are also pure functions we don't have to worry about mutating the passed in component because we're returning a brand new one!
## Summary 
If you've used functions like [connect](https://react-redux.js.org/api/connect) in Redux or [withRouter](https://reactrouter.com/web/api/withRouter) from the React Router library than you've already been working with higher-order components even if you didn't realize it. The concept of higher-order functions in which HOCs are inspired by might also sound familiar to you. Although everything we can do with HOCs can be done using the [render props](https://reactjs.org/docs/render-props.html) technique or [react hooks](https://reactjs.org/docs/hooks-intro.html) these days, they can still be a good pattern to know if you're working with legacy code or just want to become a more versatile React developer.


### Resources:
* [React docs (Higher-Order Components)](https://reactjs.org/docs/higher-order-components.html)
* [Never write another HoC](https://www.youtube.com/watch?v=BcVAq3YFiuc&t=2606s)
* [Higher order function](https://en.wikipedia.org/wiki/Higher-order_function)









