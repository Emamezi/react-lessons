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

