<!-- Do not edit this file. It is automatically generated by API Documenter. -->

[Home](./index.md) &gt; [@genesislcap/foundation-comms](./foundation-comms.md) &gt; [criteriaFiltersToFields](./foundation-comms.criteriafilterstofields.md)

## criteriaFiltersToFields() function

Criteria filters to fields.

**Signature:**

```typescript
export declare function criteriaFiltersToFields(filters: string): Record<string, string>;
```

## Parameters

|  Parameter | Type | Description |
|  --- | --- | --- |
|  filters | string | Concatenated criteria filters. |

**Returns:**

Record&lt;string, string&gt;

## Remarks

For filtering REQUEST\_SERVER resources. Maps concatenated criteria filters from a grid to a request fields object, eg: `foo == 'bar' && asd == 'zxc', into { foo: 'bar', asd: 'zxc' }`

