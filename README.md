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





