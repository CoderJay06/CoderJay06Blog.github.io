---
layout: post
title:      "An Overview of React Context API"
date:       2021-07-23 22:50:04 +0000
permalink:  an_overview_of_react_context_api
---


*"Context provides a way to pass data through the component tree without having to pass props down manually at every level."- React Docs*

## Why Context?
In your average React application, there are always parent and child components included. The main flow would be to pass down state data from the parent to the child. This brings up the problem of prop drilling. You might have heard of this term if you've been using React for a while. It describes the concept of handling your data by passing it down as props from parent to child over and over until it reaches the component you want to use it in. This causes some problems that might seem obvious like performance issues and just having to keep track of where the data is being passed down from can be an unnecessary hassle. This is where React's Context API comes in. Context supplies us with a better way to handle the flow of our application's data without passing it down manually through every component.
## How to use Context
To begin using Context, we first need to create a new Context object and assign it to a variable usually including the name Context like the following:
```
const ExampleContext = React.createContext()
```
This will give us access to two properties, a Consumer and a Provider property. The Consumer is what we use to read the data that gets passed down by the Provider. After creating our new Context object we can now setup the Provider:
```
// the value gets passed down as children props by the Provider
<ExampleContext.Provider value={"Hello!"}>
  {props.children}
</ExampleContext.Provider>
```
Now as you can see here the provider has a value prop, it contains whatever data we want to be used by the consumer. We also need to render the *props .children* in the provider so any component that wishes to handle the data can subscribe to it. After setting up the provider we can move on to the component that needs to utilize our data. Here we just import our context to use the consumer property in the return part of our class or function component. Then we create a render prop which will take the value passed from the provider and handle it however we see fit.
```
// the Consumer uses a render prop to handle the passed down data
<ExampleContext.Consumer>
  {(value) => console.log(value)}
</ExampleContext.Consumer>
```
Now we can import our context anywhere we want and make use of the provider for any component that needs to use the data.
```
<ExampleContext.Provider>
  <Component />
</ExampleContext.Provider>
```
## Context in action
Let's see an example of React Context api being used in a more real world scenerio. We'll build a stock traking application. For this app we need a way to use our array of ticker symbols across multiple components of our app. This is a good time to create a new context so we don't have to manually keep passing down our ticker symbols.
```
import React from "react"

const StocksContext = React.createContext()
const { Provider, Consumer } = StocksContext

function StocksContextProvider({children}) {
    const tickers =  ["TSLA", "AMZN", "GME", "COIN"]
    
    return (
        <Provider value={{tickers}}>
            {children}
        </Provider>
    )
}

export {StocksContextProvider, Consumer as StocksContextConsumer}
```
At the bottom of this file that we're creating the context in, we're exporting the provder and consumer. Make sure not to use a default export here as it will throw an error. We can now just import the consumer part of context and bring it into our Stocks component to display our ticker symbols.
```
import React from "react"
import {StocksContextConsumer} from "./stocksContext"

class Stocks extends React.Component {
   render() {
       return (
           <StocksContextConsumer>
            {({tickers}) => (
                tickers.map(ticker => <p key={ticker}>{ticker}</p>)
            ) }
          </StocksContextConsumer>
       )
   }
}

export default Stocks
```
Now with the following we just bring in the provider to wrap our Stocks component and we'll have our stock ticker symbols rendering properly.
```
import React from "react"
import Stocks from "./Stocks"
import {StocksContextProvider} from "./stocksContext"
function App() {
    return (
        <StocksContextProvider>
            <Stocks />
        </StocksContextProvider>
    )   
}

export default App
```
## Conclusion
Using React's Context Api we can globally share our data across several components that may be nested many levels down the React tree. Do keep in mind though that context should not be used everytime we have to share data. If you're app is small and only using context for a couple of components and not across a larger app with multiple components in need of that data, then you might want to rethink using context. 


### React Context Resources
* [React Context Docs](https://reactjs.org/docs/context.html)
* [Wes Bos How React Context API Works](https://www.youtube.com/watch?v=XLJN4JfniH4&t=606s)
