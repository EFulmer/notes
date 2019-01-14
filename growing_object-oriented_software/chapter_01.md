# Chapter 1


**Acceptance tests:** tests that test a specific feature of the system.

**Integration tests:** tests that check that the system _integrates_ with external systems properly. These systems can be databases that the maintainers don't own, external APIs, etc.

**Unit tests:** tests that check whether the system's internal interfaces behave as expected. Make a distinction between _internal interfaces_ and _private methods_. Private methods should not be tested directly; they get indirectly tested by ensuring the public interfaces that use them work properly. Internal interfaces are things like a class or function that filters or joins multiple data sources for use further along in a pipeline, etc.

_Note on unit tests and code quality_: If unit tests are difficult to read and/or write, that is often a sign that the internal interfaces or "units" of software aren't designed well. This could be because of suboptimal coding practices or that classes or functions aren't truly "units" of code that logically make sense.

**End-to-end tests:** tests that exercise the entire software system through its externally published entry points. **Acceptance tests should be end-to-end tests using external interfaces that users will interact with!**

When writing tests for a system, start with acceptance tests. It's tempting to start with unit tests, but unit tests are weaker guarantees than acceptance tests. When you write an acceptance test, it shouldn't care about any internal interfaces the software has, because it uses the "public" API/entrypoints. Writing the harder tests first front-loads the difficult work -- more on this later. 

You can view development and testing as a set of loops; each one is a stage where bugs can potentially be caught (ideally in development, of course!). The innermost loop is unit tests, because something can fail here that doesn't necessarily reflect what a customer sees. After that come the integration and acceptance tests, as these should be as close as possible to real world situations. Then, finally, is your software's behavior in that "real world". 
