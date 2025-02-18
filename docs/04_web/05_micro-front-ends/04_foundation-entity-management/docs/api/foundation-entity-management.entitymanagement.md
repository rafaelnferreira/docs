<!-- Do not edit this file. It is automatically generated by API Documenter. -->

[Home](./index.md) &gt; [@genesislcap/foundation-entity-management](./foundation-entity-management.md) &gt; [EntityManagement](./foundation-entity-management.entitymanagement.md)

## EntityManagement class

Main class which defines the entity management functionality

**Signature:**

```typescript
export declare class EntityManagement extends EntityManagement_base 
```
**Extends:** EntityManagement\_base

## Remarks

Connects to a backend resource and wraps up a grid which is populated with entities from that resource. The different interactions that the user can perform with the entities can be configured, examples being able to update and delete entities.

## Example

Example of using the entity management system to handle counterparties

```
<entity-management
  resourceName="ALL_COUNTERPARTYS"
  title="Counterparty Management"
  updateEvent="EVENT_COUNTERPARTY_MODIFY"
  deleteEvent="EVENT_COUNTERPARTY_DELETE"
  createEvent="EVENT_COUNTERPARTY_INSERT"
></entity-management>
```
Where:<br /> - the title of the grid is `Counterparty Management`<br /> - the name of the resource in the database to manage is `ALL_COUNTERPARTYS`<br /> - the name of the event handler for update events is `EVENT_COUNTERPARTY_MODIFY`<br /> - the name of the event handler for create events is `EVENT_COUNTERPARTY_INSERT`<br /> - the name of the event handler for delete events is `EVENT_COUNTERPARTY_DELETE`<br />

## Properties

|  Property | Modifiers | Type | Description |
|  --- | --- | --- | --- |
|  [columns](./foundation-entity-management.entitymanagement.columns.md) |  | ColDef\[\] | Array which holds the column definitions. |
|  [connect](./foundation-entity-management.entitymanagement.connect.md) | <code>protected</code> | Connect | DI connect object which is used to interact with the backend. |
|  [createEvent](./foundation-entity-management.entitymanagement.createevent.md) |  | string | Name of the event handler on the Genesis server which handles creating an entity |
|  [createFormUiSchema](./foundation-entity-management.entitymanagement.createformuischema.md) |  | any |  |
|  [datasourceConfig](./foundation-entity-management.entitymanagement.datasourceconfig.md) |  | [DatasourceConfiguration](./foundation-entity-management.datasourceconfiguration.md) | The configuration which is used when interacting with the resource on the backend |
|  [defaultEntityValues](./foundation-entity-management.entitymanagement.defaultentityvalues.md) |  | any |  |
|  [deleteEvent](./foundation-entity-management.entitymanagement.deleteevent.md) |  | string | Name of the event handler on the Genesis server which handles deleting the entity |
|  [editDialogTitle](./foundation-entity-management.entitymanagement.editdialogtitle.md) |  | string | String which contains the text of the popup modal when the user is adding or editing an entity |
|  [editedEntity](./foundation-entity-management.entitymanagement.editedentity.md) |  | any | Disables the form while enabled to stop the user dispatching a large number of duplicate events |
|  [editEntityModal](./foundation-entity-management.entitymanagement.editentitymodal.md) |  | any |  |
|  [editModalVisible](./foundation-entity-management.entitymanagement.editmodalvisible.md) |  | boolean |  |
|  [enableCellFlashing](./foundation-entity-management.entitymanagement.enablecellflashing.md) |  | boolean |  |
|  [enableFilterBar](./foundation-entity-management.entitymanagement.enablefilterbar.md) |  | boolean |  |
|  [entityLabel](./foundation-entity-management.entitymanagement.entitylabel.md) |  | string | Label for the entity which has usages such as being shown in the title of the modal wen editing the entity |
|  [formUiSchema](./foundation-entity-management.entitymanagement.formuischema.md) |  | any |  |
|  [gridOptions](./foundation-entity-management.entitymanagement.gridoptions.md) |  | GridOptions | GridOptions to be passed down from application |
|  [hideDelete](./foundation-entity-management.entitymanagement.hidedelete.md) |  | boolean |  |
|  [hideEdit](./foundation-entity-management.entitymanagement.hideedit.md) |  | boolean |  |
|  [modalPosition](./foundation-entity-management.entitymanagement.modalposition.md) |  | 'centre' \| 'left' \| 'right' | Determines where the modal dialog will appear on screen |
|  [persistColumnStateKey](./foundation-entity-management.entitymanagement.persistcolumnstatekey.md) |  | string | This attribute controls whether and how the entity manager stores the state of the columns when the user edits them. Omit this attribute to disable the functionality, set it to a unique value to enable it. |
|  [readEvent](./foundation-entity-management.entitymanagement.readevent.md) |  | string |  |
|  [readEventFn](./foundation-entity-management.entitymanagement.readeventfn.md) |  | (...args: any\[\]) =&gt; {} |  |
|  [readonly](./foundation-entity-management.entitymanagement.readonly.md) |  | boolean |  |
|  [resourceName](./foundation-entity-management.entitymanagement.resourcename.md) |  | string | Name of the backend resource which contain the entities to manage |
|  [selectedEntity](./foundation-entity-management.entitymanagement.selectedentity.md) |  | any | Reference to the currently selected entity from the grid. |
|  [sizeColumnsToFit](./foundation-entity-management.entitymanagement.sizecolumnstofit.md) |  | boolean |  |
|  [submitting](./foundation-entity-management.entitymanagement.submitting.md) |  | boolean |  |
|  [title](./foundation-entity-management.entitymanagement.title.md) |  | string | Title of the grid |
|  [updateEvent](./foundation-entity-management.entitymanagement.updateevent.md) |  | string | Name of the event handler on the Genesis server which handles updating the entity |
|  [updateFormUiSchema](./foundation-entity-management.entitymanagement.updateformuischema.md) |  | any |  |

## Methods

|  Method | Modifiers | Description |
|  --- | --- | --- |
|  [closeModal()](./foundation-entity-management.entitymanagement.closemodal.md) |  |  |
|  [confirmDelete()](./foundation-entity-management.entitymanagement.confirmdelete.md) |  |  |
|  [criteriaChanged(e)](./foundation-entity-management.entitymanagement.criteriachanged.md) |  |  |
|  [deepClone()](./foundation-entity-management.entitymanagement.deepclone.md) |  | Override the deepClone method to ensure that observable attributes are cloned |
|  [editModalVisibleChanged()](./foundation-entity-management.entitymanagement.editmodalvisiblechanged.md) |  |  |
|  [submitEntityChanges(e)](./foundation-entity-management.entitymanagement.submitentitychanges.md) |  | Event handler for when the user submits the action for the currently open form, either editing or adding the entity |

