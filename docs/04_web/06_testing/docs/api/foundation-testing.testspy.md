<!-- Do not edit this file. It is automatically generated by API Documenter. -->

[Home](./index.md) &gt; [@genesislcap/foundation-testing](./foundation-testing.md) &gt; [testSpy](./foundation-testing.testspy.md)

## testSpy() function

Decorator: Used on a test harness class based on a `FoundationElement` to give it extra functionality which can be used during testing. \*Important\* this is to be used on a parent element compared to the element under test.

**Signature:**

```typescript
export declare function testSpy(constructor: Function): void;
```

## Parameters

|  Parameter | Type | Description |
|  --- | --- | --- |
|  constructor | Function |  |

**Returns:**

void

## Remarks

Access the test functionality using the type with [WithTestHarness](./foundation-testing.withtestharness.md)

Reset after each test with [resetTestHarness()](./foundation-testing.resettestharness.md)

## Example

// Testing the first function call async ({ element }) =&gt; {

assert.ok( element.layout.addItemFromChild.calledWith({ type: 'component', componentType: 'test', title: `Item test`, reorderEnabled: true, isClosable: false, size: undefined, }) );

// Reset the tester at the end of every test even if you don't assert on any of it! resetTestHarness(element.layout); }

