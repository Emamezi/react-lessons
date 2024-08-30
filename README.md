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
