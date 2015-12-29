# Ducks 1.0.0

## Introduction

When building a [Redux](TODO: add redux link) application, for each feature there is often a need to add a `{actionTypes, actions, reducer}` tuple for each use case. Therefore, it makes sense to put each of these into it's own self-contained module, which if needed could even be packaged into a library.

## Ducks Specification (Ducks)

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](http://tools.ietf.org/html/rfc2119).

1. Software using Ducks must use [Redux](TODO: link to redux), or a compatible equivalent.
2. A Duck MUST be a self contained module. It MAY be either a file, a directory, or a completely independent module.
3. A Duck MUST export default (ECMAScript 2015), or export a function called `reducer` (The "reducer").
4. The reducer MUST be a valid Redux reducer
    a) It MUST take two arguments, the current state and the action
    b) If the current state is `undefined`, the reducer MUST return it's default state.
    c) The reducer MUST NOT return `undefined`, ever.
    d) The reducer MAY NOT ever mutate the state. It must make a copy of it.
    e) If the reducer does not recognize the action, it is REQUIRED to return the state, unmodified
5. A Duck MUST export one or more action creators.
6. Each action creator:
	a) MUST be a function
	b) MUST return an plain object (the "action"). (created by an object literal).
	c) The action MUST have a type property (the "action type").
	d) The action type MUST always be the same for all actions returned by the action creator.
	d) The action type MUST be a string
	e) The reducer MUST handle actions of with a type of action type, but copying (NOT mutating), and updating the state.
7. Action types must be in the form of `<package name>/<duck name>/<ACTION_TYPE>`.
	- For example, if the package was called `super-awesome-package`, and the action was `update`, and the Duck was called `status`, the action type would be `super-awesome-package/status/UPDATE`
	- The action type MUST be in UPPER\_SNAKE\_CASE
8. All action types must be unique
    - It is RECCOMMENDED that for an application, the package name is either the URL, or if one is not available or otherwise not appropriate, the GitHub repository of the project, with the username and the repository name replaced with a `-` (as that is invalid for a github username).
9. // TODO: you may export ACTION_TYPES