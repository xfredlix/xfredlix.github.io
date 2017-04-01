# React

- Views contained in the application, translates app data into something that is displayed and user interacts with
- Class components when we want state in our component, must have render method, use this.props
- Functional components are simple that takes props and returns static jsx, never changes and is always the same
- Functional takes props as arguments which uses props.videos, or { videos } in argument which uses videos
- Whenever we change our state, the component instantly rerenders along with its children
- This.state = {} is set in constructor, and this.setState({}) everywhere else
- Import/export, relative path for files we wrote './', whenever use library just use name of library
- Each component has their own state
- State is reserved only for interactivity, that is, data that changes over time
- There are two types of "model" data in React: props and state, props are immutable and states are mutable
- Controlled field is a form element where the value of the input is set by the state of the input, not the other way around
- onChange, onClick, on* all have an event object as an argument
- Use .map to render an array, and always add a key property key={books.id} to the top level element in the list
- ComponentWillMount, call action creator for API/axios request
- Use ternary in render

### React Router

- browserHistory, an object, works behind the scenes and watches the URL path / (after .com), and can update it when required. It takes the URL when it changes and passes it to react router. React router takes the URL and and depending on the URL, need to show components. It sends it to react and then react puts out HTML and renders the components on the screen
- React router is a component, render(<Router/>, document.getElementById('app'))
- Nest routes to allow them to persist, and render {this.props.children} in parent route
- Parent routes are active when child routes are active, / is the parent of everything
- If using browerHistory, change relative paths to absolute paths in index.html <script src="/bundle.js"></script> and add --history-api-fallback in package.json
- IndexRoute will be shown whenever the URL matches with the path defined by the parent but not one of the children. If URL is / show App and IndexRoute

# Redux

- Data contained in the application
- State is application level
- Less frequently pass down callbacks to manipulate data for parent child communication

### Reducers

- Pure function that returns a piece of the application's state
- Two arguments, the previous state (not application state) from the reducer and an action
- Index.js combineReducers has 1:1 pairing of key to reducer, books: booksReducer which is available as state.books in container
in mapStateToProps, return { books: state.books }
- Only ever called when an action occurs
- Never mutates state, use Object.assign to copy and return

### Containers

- React component that has a direct connection to the state from redux
- Only the most parent component that cares about a piece of state should be a container
- mapStateToProps takes application's state as argument and returns an object that will be available to the component as this.props; return {a: 123} this.props.a //123 {books: state.books}
- connect takes mapStateToProps as first argument (if no mapStateToProps pass in null) and mapDispatchToProps as second argument, and a component and produces a container, which is a component that is aware of the state by redux
- Whenever application state changes, the container/component will instantly re-render with the new list of books
- mapDispatchToProps to bind action creator to container, return bindActionCreators({selectBook: selectBook}), the value is the action creator, takes object as first argument, dispatch as second argument
- Anything returned from mapDispatchToProps will end up as props on the container, this.props.selectBook calls the action creator
- bindActionCreators: whenever action creator is called, the result flows through dispatch, which receives all the actions and  passes them to all of our reducers

### Actions

- Lifecycle of an action in a redux application: starts with an event triggered by a user directly like clicking a button, or indirectly like an ajax request and page loading up. These events can optionally call an action creator, which is a function that returns an action object. That action object is then automatically sent to all reducers in our app. Reducers has the option to return a different piece of state/data as payload, if the action type matches. The new state goes into all containers and reruns mapStateToProps, which causes all our containers to re-render.
- Save action type as const in action and export it to reducer
- Return promise as the payload

### Middleware

- Functions that take an action and depending on the action, can choose to let the action pass through, manipulate, console log, or stop it before it reaches any reducers
- Redux promise sees an action and checks the payload property, if it's a promise (like axios get request), it stops the action and after the promise resolves, create a new action of same type and send it to reducers, but now payload is the response data
- Only care about action.payload.data in reducer

https://www.dropbox.com/sh/zfmi8quyuz6gjv3/AABrZHrWXKw0anymsjeXHUzEa?dl=0
https://www.robinwieruch.de/the-soundcloud-client-in-react-redux/#reduxLoop
https://www.youtube.com/watch?v=Ru3Rj_hM8bo&feature=youtu.be
