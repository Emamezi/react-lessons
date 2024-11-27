# react-lessons

React is a declarative component base state driven JS library for building user interfaces. Declarative in the sense that we tell react what a component should look like base on the data/ current state using a declarative syntax called JSX

#Components, instances and react elements

A component is a javascript function that returns react elements usually written as JSX. It is blueprint or template
Instances are created when we "use"  the component. Using a component in our code react then creates instances of the component.
Each instance holds it's own state and props and has it's own lifecycle

Diffing notes

Diffing is comparing elements step by step between two renders based on their position in the tree

Diffing assumptions

2 elements with different types will produce different trees

elements with a stable key prop stay the same between renders

considerations

same position different element --> react destroys and removes from the DOM the initial element, its children including state. Tree might be rebuilt if children stays the same (state is reset)

same position same element-->element would be kept including its children and also state. new props/attributes are passed if they change between renders. want to create a brand new component with new state then use the key props

the key props helps us tell the diffing algorithm that an element is unique. it allows react to distinguish multiple component instances of the same component type from the other instances
When a key stays the same across renders the element would be kept in the DOM even if the position in the tree changes eg using keys in lists
If the key changes between renders the element would be destroyed and a new one created even if the position in the tree is the same as before eg using keys to reset state
Use cases
in lists (key stays the same between renders)
using key prop to reset state (key changes between renders)
If you need to reset state make sure your give the element a key and the key changes between renders
summary: use key prop when you have multiple child elements of the same type


side effects are basically any interaction between a react component and the outside world. can also be thought of as a code that does something eg data fetching, subscription setup, setting timers or manually accessing the DOM
Effects exists not just to run code at different lifecycle points but to keep a code synchronised with some external system

Effects exists not just to run code at different lifecycle points but to keep a code synchronised with some external system. event handlers are the preferred way of creating side effects.
By default the effect runs after every pre-render. We can prevent that by passing in a dependency array.
The use effects have a dependency array that runs every time a prop or state used inside the use effect changes.
Each time one of the dependencies changes the effect will be executed again.
Every state variable and prop used inside th euseffect MUST be included in the dependency array
Clean up functions are run on re-renders and when the component unmounts.. They are optional

**Runs on 2 different occasions:**
-runs before the effect is executed again
-after the component is unmounted
Clean up functions are needed whenever the side effect keeps happening after the component has been pre-rendered or unmounted. Potential Clean ups eg Stop timers, cancel request,cancel subscription, remove listeners.

we use a callback function when we want to update state based on the current state and also can be used to initialise state (lazy initial state)

**UseRef hook:**
used to create a ref...it is like a box that we can put any data that we want to preserve (persist data) between renders. I can write and read from the ref using the .current property
**2 use cases:**
Create variable to stay same between renders eg previous state, set timeouts
-selecting and storing DOM elements
-Refs are for data that are NOT rendered.
DO NOT WRITE OR READ .CURRENT IN RENDER LOGIC(LIKE STATE) INSTEAD DO SO IN USEEFFECT HOOKS

**UseReducer hook:**
Its is a more complex way of managing state when compared to the useState hooks. It is also used to manage related pieces of state. it need a reducer function that stores all the logic to update state. the reducer function also decouples the state logic from the component.
A reducer must be a pure function with no side effects that takes the current state and action and returns the next state. The action is an object that describes how state should be updated. it contains an action  type and payload(basically input data)  property.
State update is triggered but the dispatch function that the useReducer returns

**Routing-React-router
Routing is simply matching different URL'S to different UI views

SPA are web apps that are executed only on the client (web browser). The pages  are never reloaded

:global() functions is usually used when we are working with classes from external sources
We use nested routes when we want a part of the UI to be controlled by a part of the URL

An index route is the default child route that is going to be matched if none of the other declared routes matches

The Outlet component renders the matching child route with its respective component  from the parent Routes' component collection of Route components.

For nested routes relative paths (cities)  are preferred and for top level routes absolute paths (/product) are preferred

Storing state in the URL is an alternative to use state in some situations. it is an easy way to store state in a global space an accessible to all components. it is s also a good way to pass data between pages form one page to the next and makes it possible to bookmark and share page with exact UI the state had at the time.



For storing state in the URL, we use two methods.

1.) Params- pass data to the next page

2.) Query String- store some global state that should be accessible everywhere

to get data from the URL we use the useParams hook

UseParams: lets me access the route parameters form the URL.

useSearchParams: to access query string parameters from the URL.

You can use programmatic navigation using the useNavigate hook. Eg submitting a form. it allows for the user to move to a new UI or route without clicking on any link

Also the Navigate components can be thought of as a redirect

<Route index element={<Navigate replace to="cities" />} />

**Authentication**
User Authentication setps:

-Get users email and password from a form and check with an API end point

-if correct, redirect to main application and sav euser object in state

-Protect application from unauthorized access (users that are not logged in)

***Performance Optimisations***
Performance Optimisation focus:

-- Prevent wasted renders - memo, useMemo, useCallback, passing elements as children or regular prop

-- Improve app speed and responsiveness- useMemo, useCallback, useTransition

-- Reduce bundle size-fewer 3rd party packages, code splitting and lazy loading

Component instance only get re-rendered in 3 different situations

state changes

context in which component subscribe to changes

parent re-renders

A render does not mean that the DOM is updated. It just means that the component function gets called and is usually and expensive operation.

A wasted render is a render that did not produce any change in the DOM

Components passed as children do not re-render since they are just props.

**Memoization** is an optimisation technique that executes a pure function once and saves the result in memory. trying to execute the function again with the same arguments as before the previously saved result will be returned without the function being executed again

components-memo

objects-useMeo

functions-useCallback

We can use the memo function to create a component that will not re-render when it's parent component re-renders as long as the passed props stays the same between renders.

Memoizing a component only really affect props. Means a memoised component will still re-render when it's own state changes or context in which it is subscribed to changes.

For memo to make semse on a component it should do so frequently and also does so witht he same props. if the props update, then the memoised component re-renders and is of no use

In react everything is re-created on every render (objects and functions). With that in mind, functions or objects that are passed as props to child component would also be created on as new props on each re-render. And hence, memo will not work because the props are different in memory. Remember, for memo to work effectively as a performance optimisation technique, the props should stay same between re-render

Solution: we memoised objects and functions to make them stable (preserve) between renders using useMemo and useCallbacks.

Values passed into the useMemo or useCallbacks would be cached in memory and returned on subsequent re-renders as long as the dependencies (inputs) stays the same. The useMemo and useCallbacks have a dependency array like useEffect. Whenever one of the dependency changes the value will be recreated.

**Use cases:**

- prevent wasted re-renders (used together with memo)

- avoid expensive calculations on every re-render e.g expensive derived state

- values that are used in the dependency array of another hook

useMemo caches (memoize) a value or a result while useCallback caches/ memoize a function

state setter functions are automatically memoised. This is a valid reason to omit them from the dependency array of the hooks -useEffect, useCallback, useMemo.

Context can be optimised only if these 3 things are true
-state in the context need to change all the time
-contextt has many consumers
-App is slow or laggy


Bundle is simply a JS file that contains the entire application code. Downloading the bundle will load the entire app at once. Bundle size is the most important thing we need to optimise, because the bundle size ia the amount of JS users have to download to start using the app. A most efficient way to reduce bundle size is code splitting into multiple parts (Lazy Loading)... splitting bundle into multiple files that can be downloaded over time

The most common lazy loading technique is to split the code at the route level(page level)

It is always better to have one effect for each side effect you want to have in the code

In JS a closure means that a function captures all the variables from its lexical scope (from the place that is was defined at the time the function was created).

Definition of stale closure: Stale closure is the referencing towards an outdated variable in between renders.

***REDUX****
The goal of the reducer is to calculate the next state based on the current state and received action. No side effects or async operations allowed in the reducer
Actions creators are really just function that return actions. It is not a redux thing but really a conventional approach to writing redux code
Reducers need to be pure functions with no side effects. therefore no async operations in a reducer or the store. We make use of a redux middleware--> Thunks

A middleware is a functions that sits between the dispatch action and the store. it allows us to run code after dispatching but before reaching the reducer in the store.

the middleware is a perfect place for side effects (setting timers, fetching data, logging, asynchronous code etc)

Steps for using middleware

1)install middleware

2)apply it to the store

3)Use middleware in action creator functions

When using thunks, instead of returning an action object in the action creators function we return a new function

**REACT ROUTER V6***** DATALOADINF FEATURE
The  <Outlet/> component of react router tell the root route where we want to render it child routes.
With useEffect we used a fetch on render approach ( render fetch and then start fetching data). It creates data loading waterfalls.....while with loader in react-router-v6, we use a render on fetch approach (render as you fetch the data)

Best was of reusing tailwind css styles is not with @apply but with react components

Redux by nature is synchronous and we cannot call an async code in a reducer therefore we have to make use of thunks. Thunk is a middleware that sits between the dispatching and the reducer itself. it does something to the dispatch action before updating the store

In react router, if i want to fetch data without actually navigation to a page i can use the useFetcher hook (fetch data without navigation). It also used for fetching data from another route i.e data that is not associated with the current page
Using replace in navigation is typically used when you don't want the user to navigate back to the previous route after a navigation action eg submitting a form,, logging in, error page etc.

It allows you navigate without pushing a new entry into the history stack which affects the browsers back behaviour.  The current URL is replaced with the new one, and the user cannot hit the "Back" button to go back to the previous URL.

React Query;

Used for managing remote (server) state. all remote state (data) is cached ie data is stored in other to be reused in other areas of the application. It also re-fetches the data in certain situations to keep state synced. Also pre-fetches data eg for pagination. Also offline support using the cached data.



Note: Remote state is fundamentally different from UI state.

In react query after mutations data is refetched but not automatically. The best way to do that is to invalidate the data in the stored cache as soon as the mutation is done, that way react query knows that the data has changed and then refetches the data from the remote server



 const { mutate, isPending } = useMutation({
    mutationFn: deleteCabin,
    onSuccess: () => {
      toast.success("Cabin successfully deleted");
      queryClient.invalidateQueries({ queryKey: ["cabins"] });
    },
    onError: (error) => toast.error(error.message),
  });
*****Advanced React Patterns******
  Components Reusability:

Another way of making components reusable asides from passing in props or children is using the render props pattern. What happens in this case is to pass in a render prop to the component that needs to be reused. The render prop takes in a function that renders JSX syntax /Element in the way two similar component can have two different render props but still share the same logic.

The component itself does not render anything besides the render prop. Instead, the component simply calls the render prop, instead of implementing its own rendering logic.

A HOC is a component that takes in another component and returns a new component that is a better or enhanced component of the initial component
Compound component pattern is creating a set of related components that together achieve a  useful component.

steps:

-create context

-create parent component

-create child components that help implementing the common task of the compound component

-add child component as properties to the parent component (optional)
