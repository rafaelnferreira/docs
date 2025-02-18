<!-- Do not edit this file. It is automatically generated by API Documenter. -->

[Home](./index.md) &gt; [@genesislcap/foundation-testing](./foundation-testing.md) &gt; [FilterConditionally](./foundation-testing.filterconditionally.md)

## FilterConditionally type

Filters out key/value pairs from an object where they value does not match a condition

**Signature:**

```typescript
export type FilterConditionally<Source, Condition> = Pick<Source, {
    [K in keyof Source]: Source[K] extends Condition ? K : never;
}[keyof Source]>;
```
