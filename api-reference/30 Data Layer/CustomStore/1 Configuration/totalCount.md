---
type: function(loadOptions)
---
---
##### shortDescription
The user implementation of the [totalCount(options)](/api-reference/30%20Data%20Layer/Store/3%20Methods/totalCount(options).md '/Documentation/ApiReference/Data_Layer/CustomStore/Methods/#totalCountoptions') method.

##### param(loadOptions): Object
An object specifying filtering and grouping options.

##### field(loadOptions.filter): Object
Data filtering conditions.

##### field(loadOptions.group): Object
Data grouping options.

##### return: Promise
A Promise of the jQuery.Deferred object resolved after data has been loaded.

---
The method passed to this option should return either the [jQuery.Deferred](https://api.jquery.com/jQuery.Deferred) promise or **jQuery.Deferred** compatible object.