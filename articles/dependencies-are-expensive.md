
## Dependencies are Expensive

Dependencies are a two-edged sword. On one hand, everything except God is dependent on something. Dependencies are essential.  But they are also expensive.

Dependencies add requirements to any component that depends on them. At minimum, dependencies add the requirement that they must be available. The component will not function as well or at all without its dependencies. Beyond that, dependencies can add additional requirements in the form of constraints. Constraints on how and where the component can be used. Some dependencies are incompatible with each other and force mutually exclusive selection.

Beyond the added constraints, dependencies can make a component harder to manage and reason about because each added dependency increases the complexity of that component.

Different dependencies have different costs.  In terms of weight, one heavy dependency can cost more than a dozen light dependencies.
