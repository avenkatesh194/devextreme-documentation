You can subscribe to an event using a configuration option. All event handling options are given names that begin with *on*.

    <!--HTML--><div dx-menu="{
        ...
        onItemClick: itemClickHandler,
        onInitializedHandler: initializedHandler
     }"></div>

    <!--JavaScript-->
    function Controller ($scope) {
        $scope.itemClickHandler = function (info) {
            // Handles the "itemClick" event
        };
        $scope.menuInstance = {};
        $scope.initializedHandler = function (info) {
            // Saves the widget instance
            $scope.menuInstance = info.component;   
            // Handles the "initialized" event
        }
    }

#include common-demobutton with {
    url: "https://js.devexpress.com/Demos/WidgetsGallery/Demo/Menu/Overview/AngularJS/Light/"
}

#####See Also#####
- [API Reference](/Documentation/ApiReference).**WidgetName**.**Events**

[tags]basics, angularjs, handle events, subscribe