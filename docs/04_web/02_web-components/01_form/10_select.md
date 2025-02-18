---
title: 'Web Components - Select'
sidebar_label: 'Select'
id: select
keywords: [web, web components, select]
tags:
    - web
    - web components
    - select
---

<div class="select-examples">

An implementation of an [HTML select element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select) as a form-connected Web Component. It is very similar to the [combo-box](../combobox/), but with some differences such as:

- Users can only select from the list provided.
- There is no auto-completion.
- Users can select multiple options.
- The value of the selected option can be different from its label.

## Set-up

```ts
import { provideDesignSystem, alphaSelect, alphaOption } from '@genesislcap/alpha-design-system';

provideDesignSystem().register(alphaSelect(), alphaOption());
```

## Attributes

This component needs to be used in combination with `<alpha-option>`. You can define the following attributes when you declare an `<alpha-select>`: 

| Name     | Type      | Description                                                                                                                              |
|----------|-----------|------------------------------------------------------------------------------------------------------------------------------------------|
| disabled | `boolean` | Similar to `readonly`, but with a blur on the component                                                                                  |
| form     | `string`  | Associates this component with a form. Form `id` needs to be passed. If no Id is provided, then it will be associated with the ancestor form  |
| multiple | `boolean` | Enables the user to select more than one option; this automatically opens the selection and removes the side arrow. **Default:** `false` | 
| name     | `string`  | Gives this component a name                                                                                                              |
| open     | `boolean` | Defines whether the list starts opened or not. **Default:** `false`                                                                      |
| position | `string`  | Places the list **above** or **below** the component; can be `above` or `below`. **Default:** it will try to fit with the page           | 
| size     | `number`  | Defines the maximum number of options to be displayed. **Default:** it will try to fit with the page                                     | 
| value    | `string`  | Sets a value for this component                                                                                                          | 


### Option attributes

In order to use the select component, you need to create a list of options for the user to select from. You create this list using `<alpha-option>`. You can define the following attributes for an `<alpha-option>`:

| Name     | Type      | Description                                                                                  |
|----------|-----------|----------------------------------------------------------------------------------------------|
| disabled | `boolean` | Disables an option so that the user cannot interact with it, but the option is still visible |
| selected | `boolean` | Selects the option, so it turns to the selected mode                                         |

:::note
- If you specify a `selected` or `value` to more than one `option` while `multiple = false`, then the component selects only the first in the `alpha-option` list
:::

## Usage
All examples below use the `alpha-design-system`. If you are using any other design system, change the declaration of this component accordingly.

- **Example 1**: a select displaying 2 options at a time; users can scroll up or down to see other options in the list
```html title="Example 1"
<alpha-select size="2" open>
    <alpha-option value="s">Small</alpha-option>
    <alpha-option value="m">Medium</alpha-option>
    <alpha-option value="l">Large</alpha-option>
    <alpha-option value="xl">Extra Large</alpha-option>
</alpha-select>
```
- **Example 2**: a disabled select greyed out so that users can not select an option; 2 options selected: "s" and "l"
```html title="Example 2"
<alpha-select disabled multiple>
    <alpha-option selected value="s">Small</alpha-option>
    <alpha-option value="m">Medium</alpha-option>
    <alpha-option selected value="l">Large</alpha-option>
    <alpha-option value="xl">Extra Large</alpha-option>
</alpha-select>
```
- **Example 3**: a select with a starting value of `xl`; when the user clicks, the list is displayed above the select
```html title="Example 3"
<alpha-select position="above" value="xl">
    <alpha-option value="s">Small</alpha-option>
    <alpha-option value="m">Medium</alpha-option>
    <alpha-option value="l">Large</alpha-option>
    <alpha-option value="xl">Extra Large</alpha-option>
</alpha-select>
```

### Get the user input
Once the user has input a value to this component, you need to make it accessible to the application:

1. Create an `@observable` variable where you want to use this value:

```html {1,5}
import {... , observable} from '@microsoft/fast-element';
...
export class TEMPLATE extends FASTElement {
...
@observable select_value: string
...
}
```

2. Use the `sync` function to insert the value from the component into the variable `select_value`:

```typescript tile="Example 4" {1,4-9}
import {sync} from '@genesislcap/foundation-utils';
...
    ...
        <alpha-select :value=${sync((x) => x.select_value)}>
            <alpha-option value="1">Small</alpha-option>
            <alpha-option value="2">Medium</alpha-option>
            <alpha-option value="3">Large</alpha-option>
            <alpha-option value="4">Extra Large</alpha-option>
        </alpha-select>
    ...
...    
```

From this point, you can access the value of the component in your application.

### Create a list dynamically
When you're developing your application, you normally want to generate the list instead of creating each option manually.

To do this, follow the steps below:

1. Create an `@observable Array<{value: string, label: string}>` with the options to be available in your select:

```html {1,5}
import {... , observable} from '@microsoft/fast-element';
...
export class TEMPLATE extends FASTElement {
    ...
    @observable options: Array<{value: string, label: string}> = []
    ...
}
```

Note that we are creating a complex array with two attributes: `value` and `label`. That way, it is easier to assign it in the `repeat` directive.

With this variable created, you can generate any array you wish using a loop. Here is a simple example:

``` typescript
    for (let i = 0; i < 4; i++) {
      this.options.push({value:"v" + i, label: "Label " + i});
    }
```

2. Use the `repeat` directive to create an `<alpha-option>` for each element you have in `options`

```html {1,5}
import {... , repeat} from '@microsoft/fast-element';
...
    ...
        <alpha-select>
            ${repeat(x => x.options, html` <alpha-option value=${x => x.value}>${x => x.label}</alpha-option>`)}
        </alpha-select>
    ...
...    
```

The `repeat` directive takes two arguments:
- The first one is the array/object to be iterated. In the code above, we have `x => x.options` because the variable we created is an array named `options`.
- The second is the component to be repeated for each element in the array/object passed in the first argument. In this case, we are repeating the component `alpha-option`.


If you are not familiar with the `repeat` directive, take a look at the [Microsoft Fast documentation](https://www.fast.design/docs/fast-element/using-directives/#the-repeat-directive).

## Try yourself

```html title="try yourself" live
<alpha-select>
  <alpha-option value="s">Small</alpha-option>
  <alpha-option value="m">Medium</alpha-option>
  <alpha-option value="l">Large</alpha-option>
  <alpha-option value="xl">Extra Large</alpha-option>
</alpha-select>
```

## Use cases

- Selecting from a list of options
- Selecting multiple options
- Sorting
- Filtering

## Additional resources

- [W3C Component Aria Practices](https://www.w3.org/TR/wai-aria-practices-1.1/#Listbox)

</div>
