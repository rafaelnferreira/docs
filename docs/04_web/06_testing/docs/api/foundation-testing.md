<!-- Do not edit this file. It is automatically generated by API Documenter. -->

[Home](./index.md) &gt; [@genesislcap/foundation-testing](./foundation-testing.md)

## foundation-testing package

## Functions

|  Function | Description |
|  --- | --- |
|  [createComponentSuite(title, elementNameOrGetter, context, registrations)](./foundation-testing.createcomponentsuite.md) | Create component test suite. |
|  [createLogicSuite(title, context)](./foundation-testing.createlogicsuite.md) | Create logic test suite. |
|  [fixture(templateNameOrRegistry, options)](./foundation-testing.fixture.md) | Creates a test fixture suitable for testing custom elements, templates, and bindings. |
|  [resetTestHarness(wrapper)](./foundation-testing.resettestharness.md) | Resets the history of the spied functions on the objects so previous running tests don't affect the current test. Must be called at the end of every test even if not asserting on the spies. |
|  [restoreTestHarness(wrapper)](./foundation-testing.restoretestharness.md) | Restores the spied functions back to the original functions without the spies. |
|  [runCases(fn, cases, assertion)](./foundation-testing.runcases.md) | Assert a set of test cases. |
|  [testSpy(constructor)](./foundation-testing.testspy.md) | Decorator: Used on a test harness class based on a <code>FoundationElement</code> to give it extra functionality which can be used during testing. \*Important\* this is to be used on a parent element compared to the element under test. |

## Interfaces

|  Interface | Description |
|  --- | --- |
|  [ComponentContext](./foundation-testing.componentcontext.md) | Component suite context interface |
|  [Fixture](./foundation-testing.fixture.md) | Unit test fixture. |
|  [FixtureOptions](./foundation-testing.fixtureoptions.md) | Options used to customize the creation of the unit test fixture. |
|  [LogicContext](./foundation-testing.logiccontext.md) | Logic suite context interface |

## Variables

|  Variable | Description |
|  --- | --- |
|  [logger](./foundation-testing.logger.md) | Test logger |

## Type Aliases

|  Type Alias | Description |
|  --- | --- |
|  [ElementGetter](./foundation-testing.elementgetter.md) |  |
|  [Equal](./foundation-testing.equal.md) | Expects that the type parameter X is equal to Y, returning true or false |
|  [Expect](./foundation-testing.expect.md) | Expects that the type parameter T resolves to true, or will be a typescript error |
|  [FilterConditionally](./foundation-testing.filterconditionally.md) | Filters out key/value pairs from an object where they value does not match a condition |
|  [RunCases](./foundation-testing.runcases.md) |  |
|  [SinonWrapper](./foundation-testing.sinonwrapper.md) | Crates an object with a key value pair for each spied function where the key is the function name and the value is the sinon wrapped spy function |
|  [SpiedFunctions](./foundation-testing.spiedfunctions.md) | Filters out all key/value pairs which are not functions, and omits the constructor |
|  [SuiteCallback](./foundation-testing.suitecallback.md) | Defines the Generic type for a test Suite <code>T</code> the callback function required to assert on type <code>T</code>. |
|  [WithTestHarness](./foundation-testing.withtestharness.md) | Type can be used to inform Typescript the object decorated with [testSpy()](./foundation-testing.testspy.md) has function spies which can be interacted upon their normal function reference |

