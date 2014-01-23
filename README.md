AngularJS multi-sortable directive
=======

__This directive development will be discontinued which means it is usable only in Angular 1.x.
If you are looking for Angular 1.2 compatible version, [Angular-UI](https://github.com/angular-ui/ui-sortable) `ui-sortable` directive does exactly the same thing.__


*Starting from version 0.0.2 this component is available via [Bower](http://twitter.github.io/bower/) package manager.*

This AngularJS directive allows effectively using JQuery UI sortable plugin with `connectWith` option giving ability to create portlet-like UIs.
It was built partially on angular-ui-sortable "uiSortable" directive and it keeps its core functionality.

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


Define global `sortable` options that will be provided to underlying jQuery sortable plugin. Here we need to provide `connectWith` option to link several sortables together.

    angular.module('ui.sortable').value('uiSortableConfig', {
      sortable: {
        connectWith: '.column',
        update: 'itemsChanged',
      }
    });
	
Define UI part as below, using `ui-multi-sortable` directive and `model-subset` attribute to point actual items' subset.

    <body ng-controller="TaskboardController">
        <div ui-multi-sortable ng-model="items" model-subset="todo" class="column">
            <div class="item" ng-repeat="item in items.todo">{{ item.name }}</div>
        </div>        
        <div ui-multi-sortable ng-model="items" model-subset="done" class="column">
            <div class="item" ng-repeat="item in items.done">{{ item.name }}</div>
        </div>
    </body>

`model-subset` can be more sophisticated expression that Angular can evaluate, e.g.:
    
    columns[{{ $index }}].items
    
See `example` directory for such use-case.


It is possible to hook up own callbacks into `update`, `start` and `stop` events in sortable. Callbacks can be either Angular `$scope` functions or regular functions (outside Angular context).
To invoke `$scope` function, name of this function should be provided instead of function reference.
Example of defining callbacks:

    angular.module('ui.sortable').value('uiSortableConfig', {
	  sortable: {
		connectWith: '.column', 
		update: 'changed',	// $scope function called 'changed' will be invoked within Angular context
		start: function() { console.log('modification started');	// regular function will be invoked
	  }
	});

Changelog
-----

### 0.0.2

First version of component. Works with older versions of Angular-UI components (before project was split)

### 0.1.0

Dependencies updated to `1.0.7`for AngularJS itself and `0.0.1` for angular-ui-sortable. This version isn't backward compatible due to changes in foundation components (angular-ui-sortable).
        
