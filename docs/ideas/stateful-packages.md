# Stateful Packages

- State can be represented as function input
- With this approach data points need to be pushed down to where they are used
  - The data-flow goes from parent functions towards child functions
- Function composition works in the opposite direction: 
  - Outputs of child functions are composed together to produce the result of parent functions
- This bi-directionality of the dataflow creates strong-coupling between functions
  - The signature of the parent function depends on the inputs of the child functions it ends up calling 
- Languages that allow side-effects don't have a problem with this since you can pull-in state anywhere and you 
don't have to pass it through all the components
  - As a result you can compose components without passing around all the state they require

- Can we achieve the same with FP?
- What would happen if we didn't pass inputs to a function?
  - It could only call other functions without input.
  - Where does the state come from?
  - Values are state that doesn't change, except

