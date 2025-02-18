<!-- Do not edit this file. It is automatically generated by API Documenter. -->

[Home](./index.md) &gt; [@genesislcap/foundation-testing](./foundation-testing.md) &gt; [WithTestHarness](./foundation-testing.withtestharness.md)

## WithTestHarness type

Type can be used to inform Typescript the object decorated with [testSpy()](./foundation-testing.testspy.md) has function spies which can be interacted upon their normal function reference

**Signature:**

```typescript
export type WithTestHarness<T extends {
    [k in keyof T]: any;
}> = T & SinonWrapper<SpiedFunctions<T>>;
```
**References:** [SinonWrapper](./foundation-testing.sinonwrapper.md), [SpiedFunctions](./foundation-testing.spiedfunctions.md)

