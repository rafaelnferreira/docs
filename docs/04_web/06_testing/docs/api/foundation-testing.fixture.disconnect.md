<!-- Do not edit this file. It is automatically generated by API Documenter. -->

[Home](./index.md) &gt; [@genesislcap/foundation-testing](./foundation-testing.md) &gt; [Fixture](./foundation-testing.fixture.md) &gt; [disconnect](./foundation-testing.fixture.disconnect.md)

## Fixture.disconnect() method

Removes the [Fixture.parent](./foundation-testing.fixture.parent.md) from the DOM, causing the disconnect lifecycle to begin.

**Signature:**

```typescript
disconnect(): Promise<void>;
```
**Returns:**

Promise&lt;void&gt;

## Remarks

Yields control to the caller one Microtask later, in order to ensure that the DOM has settled.

