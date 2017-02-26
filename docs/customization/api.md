# API

We have learned a lot regarding how people use Material-UI.
The 1.x.x rewrote allowed us to completely rethink our components API.

> API design is hard because you can make it seem simple but it's actually deceptively complex, or make it actually simple but seem complex.

[@sebmarkbage](https://twitter.com/sebmarkbage/status/728433349337841665)

As Sebastian Markbage [pointed out](http://2014.jsconf.eu/speakers/sebastian-markbage-minimal-api-surface-area-learning-patterns-instead-of-frameworks.html), no abstraction is superior to wrong abstractions.
We are providing low-level components to maximize composition capabilities.

## Composition

You may have noticed some inconsistency in our API regarding composing components.
To provide some transparency, we have been using the following rules when designing the API:

1. Using the `children` property is the idiomatic way to do composition with React.
2. Something, we only need a limited children composition.
For instance, when we don't need to allow children order permutation.
Under this condition, providing explicit properties is making the implementation simpler and more performant.
For example, the `<Tab />` takes an `icon` and a `label` property.
3. API consistency matters.

## Rules

Aside from the above composition trade-off, we use the following rules:

- Undocumented properties supplied are spread to the root element.
- Internal components have:
 - their own `xxxClassName` property when style customization makes sense. For instance, we expose an `inputClassName` property.
 - their own `xxxProps` property when users might need to tweak internal render method's components. For instance, we expose an `inputProps` property.
 - their own flattened properties when they are key to the abstraction. For instance, we expose a `value` property.
- The name of the boolean properties should be chosen based on the default value. We are following the HTML specification. For instance, the `disabled` attribute on an input element. This choice allows the shorthand notation.