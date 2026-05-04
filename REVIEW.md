# Code Review

Good code review requires human skills and technical skills alike. Therefore, alongside actual
technical findings I am going to present also my thoughts and strategy. Unfortunately I have no
additional information about the person like seniority, character, personal rapport, etc.

## Strategy

This PR has many issues. It is critical to approach the review without antagonising the author
and avoid the impression of gating (many review rounds). It is a delicate balance to strike.
My strategy would be to provide general direction in first review pass and then provide details
in the second pass.

## Delivery

Ideally I would deliver both review passes in writing. With the exception of very junior staff
or if there exists additional information about the author (like higher sensitivity to feedback).
In the later case I would first opt for a 30 minute call *before* publishing any feedback any
feedback in writing.

## Review pass #1

The goal is to make the author realize as many faults in their code without overwhelming them.
Natural place to start is to point to the test coverage, so as many defects are fixed along
the way as possible.

- `test_app:14` Great, thank you for adding a test! What do you think about extending the
test suite to also cover more complex cases and corner cases (request/response failures,
bad input, etc)?
- `app.py:17` I see you have changed the function called here. Is there any existing code
that will become obsolete as a result?
- `npm_deps/package.py:11` I see that old code uses `max_satisfying`, is the switch to
`min_satisfying` is deliberate or a typo?

## Raw Findings

The following list of findings are my raw notes of what I see could be improved in the PR.
In that raw form they are not to be provider to another person.

`npm_deps/package.py:8`
- Missing exception handling. A single failed dependency request, wrong format returned causes.
  complete request failure. Is that desired behavior?
- Default does not seem used. Why would we accept None?
- Consider caching get_package result for specific name + range combination.
- Missing docstring

`npm_deps/package.py:9`
- There already is a helper function in package_request.py that can be re-used.
- `request_package` should also consider retry, exponential backoff etc.
- Errors not checked - immediate call of .json()

`npm_deps/package.py:11`
- Should not be max_satisfying?




