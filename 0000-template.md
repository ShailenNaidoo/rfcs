- Start Date: 2019-09-16
- Target Major Version: (2.x / 3.x)
- Reference Issues: (fill in existing related issues, if any)
- Implementation PR: (leave this empty)

# Summary

A way to kill / remove event bindings if given a "falsy" value

# Basic example

```vue
<button @click="null">Click Me!</button>

<button v-on="{ input: null, change: null }">Click Me!</button>
```

# Motivation

When binding events to a component it would be great to remove the event if it is given a "falsy" value instead of throwing an error when not given a function.

It would come in handy when binding functions to events that can be undefined.

**Without feature**

```vue
<template functional>
  <button
    v-on="{
      input: props.inputHandler || (() => {}),
      change: props.changeHandler || (() => {}),
    }"
  >
    Click me
  </button>
</template>
```

**With feature**

```vue
<template functional>
  <button
    v-on="{
      input: props.inputHandler,
      change: props.changeHandler,
    }"
  >
    Click me
  </button>
</template>
```

# Detailed design

This is the bulk of the RFC. Explain the design in enough detail for somebody
familiar with Vue to understand, and for somebody familiar with the
implementation to implement. This should get into specifics and corner-cases,
and include examples of how the feature is used. Any new terminology should be
defined here.

# Drawbacks

Why should we *not* do this? Please consider:

- implementation cost, both in term of code size and complexity
- whether the proposed feature can be implemented in user space
- the impact on teaching people Vue
- integration of this feature with other existing and planned features
- cost of migrating existing Vue applications (is it a breaking change?)

There are tradeoffs to choosing any path. Attempt to identify them here.

# Alternatives

What other designs have been considered? What is the impact of not doing this?

# Adoption strategy

If we implement this proposal, how will existing Vue developers adopt it? Is
this a breaking change? Can we write a codemod? Can we provide a runtime adapter library for the original API it replaces? How will this affect other projects in the Vue ecosystem?

# Unresolved questions

Optional, but suggested for first drafts. What parts of the design are still
TBD?
