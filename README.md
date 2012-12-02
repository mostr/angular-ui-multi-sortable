AngularJS multi-sortable directive
=======

This AngularJS directive allows effectively using JQuery UI sortable plugin with `connectWith` option giving ability to create portlet-like UIs.
It was built partially on angular-ui "uiSortable" directive and it keeps its core functionality.

Usage
-----
For complete example see `example` directory.

Suppose model (in AngularJS) is defined as follows

    $scope.items = {
      todo: [
        {name: 'todo 1'},
        {name: 'todo 2'},
        {name: 'todo 3'},
        {name: 'todo 4'}
      ],
      done: [
        {name: 'done 1'},
        {name: 'done 2'},
      ]
    };


Define UI part as below, using `ui-multi-sortable` directive and `model-subset` attribute to point actual items' subset.

    <body ng-controller="TaskboardController">
        <div ui-multi-sortable ng-model="items" model-subset="todo" class="column">
            <div class="item" ng-repeat="item in items.todo">{{ item.name }}</div>
        </div>        
        <div ui-multi-sortable ng-model="items" model-subset="done" class="column">
            <div class="item" ng-repeat="item in items.done">{{ item.name }}</div>
        </div>
    </body>
