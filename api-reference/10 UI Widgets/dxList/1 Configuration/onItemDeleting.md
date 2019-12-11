---
hidden: false
default: null
type: function(e)
---
---
##### param(e): Object
Information about the event.

##### field(e.component): Object
Provides access to the widget's instance.

##### field(e.element): jQuery
The widget's container.

##### field(e.model): Object
The model data. Available only if you use Knockout.

##### field(e.itemData): object
The data of the to-be-deleted item.

##### field(e.itemElement): jQuery
The item's container.

##### field(e.itemIndex): number | object
The index of the to-be-deleted item. </br>
In a grouped list, the index represents an object defining group and item indexes: { group: 0, item: 0 }.

##### field(e.cancel): boolean | Promise
Allows you to cancel the item deletion.

---