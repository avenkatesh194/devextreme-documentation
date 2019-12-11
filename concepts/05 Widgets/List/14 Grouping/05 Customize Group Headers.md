By default, group headers contain the text of the **key** field in a bold font. You can define a custom template for group headers if you need to. For AngularJS and Knockout apps, DevExtreme provides a markup component called [dxTemplate](/api-reference/10%20UI%20Widgets/Markup%20Components/dxTemplate '/Documentation/ApiReference/UI_Widgets/Markup_Components/dxTemplate/'). The following code shows how you can use **dxTemplate** to define a template for group headers.

---

#####Angular

    <!--HTML-->
    <dx-list
        [dataSource]="listDataSource"
        [grouped]="true"
        groupTemplate="group"
        itemTemplate="item">
        <div *dxTemplate="let itemObj of 'item'">
            <p style="margin:0px">{{itemObj.name}} | {{itemObj.count}}</p>
        </div>
        <div *dxTemplate="let groupObj of 'group'">
            <p>{{itemObj.key}} | {{itemObj.overallCount}}</p>
        </div>
    </dx-list>

    <!--TypeScript-->
    import { DxListModule } from 'devextreme-angular';
    import DataSource from 'devextreme/data/data_source';
    // ...
    export class AppComponent {
        fruitsVegetables = [{
            key: "Fruits",
            items: [
                { name: "Apples", count: 10 },
                { name: "Oranges", count: 12 },
                { name: "Lemons", count: 15 }
            ]
        }, {
            key: "Vegetables",
            items: [
                { name: "Potatoes", count: 5 },
                { name: "Tomatoes", count: 9 },
                { name: "Turnips", count: 8 }
            ]
        }];
        listDataSource = new DataSource({
            store: fruitsVegetables,
            map: function(groupedItem) {
                var overallCount = 0;
                groupedItem.items.forEach(function(item) {
                    overallCount += item.count;
                })
                return Object.assign(groupedItem, { overallCount: overallCount });
            }
        });
    }
    @NgModule({
        imports: [
            // ...
            DxListModule
        ],
        // ...
    })

#####AngularJS

    <!--HTML-->
    <div ng-controller="DemoController">
        <div dx-list="{
            dataSource: listDataSource,
            grouped: true,
            groupTemplate: 'group',
            itemTemplate: 'item'
        }" dx-item-alias="itemObj">
            <div data-options="dxTemplate: { name: 'group' }">
                <p>{{ itemObj.key }} | {{ itemObj.overallCount }}</p>
            </div>
            <div data-options="dxTemplate: { name: 'item' }">
                <p style="margin:0">{{ itemObj.name }} | {{ itemObj.count }}</p>
            </div>
        </div>
    </div>

    <!--JavaScript-->
    angular.module('DemoApp', ['dx'])
        .controller('DemoController', function ($scope) {
            var fruitsVegetables = [{
                key: "Fruits",
                items: [
                    { name: "Apples", count: 10 },
                    { name: "Oranges", count: 12 },
                    { name: "Lemons", count: 15 }
                ]
            }, {
                key: "Vegetables",
                items: [
                    { name: "Potatoes", count: 5 },
                    { name: "Tomatoes", count: 9 },
                    { name: "Turnips", count: 8 }
                ]
            }];
            $scope.listDataSource = new DevExpress.data.DataSource({
                store: fruitsVegetables,
                map: function(groupedItem) {
                    var overallCount = 0;
                    groupedItem.items.forEach(function(item) {
                        overallCount += item.count;
                    })
                    return $.extend(groupedItem, { overallCount: overallCount })
                }
            });
        });

[note] The `dx-item-alias` directive specifies the variable that is used to access the item object.

#####Knockout

    <!--HTML-->
    <div data-bind="dxList: {
        dataSource: listDataSource,
        grouped: true,
        groupTemplate: 'group',
        itemTemplate: 'item'
    }">
        <div data-options="dxTemplate: { name: 'group' }">
            <p data-bind="text: key + ' | ' + overallCount"></p>
        </div>
        <div data-options="dxTemplate: { name: 'item' }">
            <p data-bind="text: name + ' | ' + count" style="margin:0"></p>
        </div>
    </div>

    <!--JavaScript-->var fruitsVegetables = [{
        // ...
        // omitted for brevity
        // see the AngularJS code
    }];

    var viewModel = {
        listDataSource: new DevExpress.data.DataSource({
            store: fruitsVegetables,
            map: function(groupedItem) {
                var overallCount = 0;
                groupedItem.items.forEach(function(item) {
                    overallCount += item.count;
                })
                return $.extend(groupedItem, { overallCount: overallCount })
            }
        })
    };

    ko.applyBindings(viewModel);

---

If you use jQuery alone, combine the HTML markup for group headers manually with jQuery [DOM manipulation methods](https://api.jquery.com/category/manipulation). To apply this markup, use the [groupTemplate](/api-reference/10%20UI%20Widgets/dxList/1%20Configuration/groupTemplate.md '/Documentation/ApiReference/UI_Widgets/dxList/Configuration/#groupTemplate') callback function as shown in the following code.

    <!--JavaScript-->var fruitsVegetables = [{
        // ...
        // omitted for brevity
        // see the AngularJS code
    }];

    $(function() {
        $("#listContainer").dxList({
            dataSource: new DevExpress.data.DataSource({
                store: fruitsVegetables,
                map: function(groupedItem) {
                    var overallCount = 0;
                    groupedItem.items.forEach(function(item) {
                        overallCount += item.count;
                    });
                    return $.extend(groupedItem, { overallCount: overallCount })
                }
            }),
            grouped: true,
            groupTemplate: function(groupData, _, groupElement) {
                groupElement.append(
                    $("<p>").text(groupData.key + " | " + groupData.overallCount)
                )
            },
            itemTemplate: function(data, _, element) {
                element.append(
                    $("<p>").text(data.name + " | " + data.count).css("margin", 0)
                )
            }
        });
    });

#include common-demobutton with {
    url: "https://js.devexpress.com/Demos/WidgetsGallery/Demo/List/GroupedList/jQuery/Light/"
}

In addition, you can use a 3rd-party template engine to perform the needed customizations. For more information, see the [Use an Alternative Template Engine](/concepts/05%20Widgets/zz%20Common/05%20UI%20Widgets/30%20Customize%20Widget%20Element%20Appearance/5%20Use%20an%20Alternative%20Template%20Engine.md '/Documentation/Guide/Widgets/Common/UI_Widgets/Customize_Widget_Element_Appearance/#Use_an_Alternative_Template_Engine') article.

#####See Also#####
- [Customize Widget Element Appearance](/Documentation/Guide/Widgets/Common/UI_Widgets/Customize_Widget_Element_Appearance/#Customize_Widget_Element_Appearance/)
- [Customize Widget Element Appearance - MVVM Approach](/concepts/05%20Widgets/zz%20Common/05%20UI%20Widgets/35%20Customize%20Widget%20Element%20Appearance%20-%20MVVM%20Approach '/Documentation/Guide/Widgets/Common/UI_Widgets/Customize_Widget_Element_Appearance_-_MVVM_Approach/')
- [List API Reference](/api-reference/10%20UI%20Widgets/dxList '/Documentation/ApiReference/UI_Widgets/dxList/')

[tags]list, group headers appearance, customize, templates, template