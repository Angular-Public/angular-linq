# angular-linq
linq.js library for AngularJS
http://linqjs.codeplex.com/

**Latest Version:** 1.0.2

**Install:**

```
bower install angular-linq
```

Injector: ``` $linq ```
Accessing Enumerable: ``` $linq.Enumerable() ```


**Example Usage:**

```
	(function () {
		'use strict';

		// 1) Include angular-linq module to app 
		angular.module('AngularLinqTestApp', [
			'angular-linq'
		]);
		
		angular.module('AngularLinqTestApp')
			.controller('AngularLinqTestAppController', AngularLinqTestAppController);

		// 2) Inject $linq to controller
		AngularLinqTestAppController.$inject = [
			'$linq'
		];

		function AngularLinqTestAppController($linq) {

			/* jshint validthis: true */
			var vm = this;
			
			vm.activate = function() {
			
				var jsonArray = [{
					"user": {
						"id": 100,
						"screen_name": "Smith Jhon"
					},
					"text": "jsmith"
				}, {
					"user": {
						"id": 130,
						"screen_name": "Stephen Kriston"
					},
					"text": "kstephen"
				}, {
					"user": {
						"id": 155,
						"screen_name": "Emma Watson"
					},
					"text": "wemma"
				}, {
					"user": {
						"id": 301,
						"screen_name": "Winona Ryder"
					},
					"text": "rwinona"
				}]
				
				// 3) Start using $linq
				vm.queryResult = $linq.Enumerable().From(jsonArray)
					.Where(function (x) {
						return x.user.id < 200
					})
					.OrderBy(function (x) {
						return x.user.screen_name
					})
					.Select(function (x) {
						return x.user.screen_name + ':' + x.text
					})
					.ToArray();
				console.log("vm.queryResult : ", vm.queryResult);
			}
			vm.activate();
		}
	})();

```
**Example Output:**

vm.queryResult :  ["Emma Watson:wemma", "Smith Jhon:jsmith", "Stephen Kriston:kstephen"]





**Change History:**

1.0.2:
Fixes to bower install

1.0.1:
Fixes to support angular version 1.4.x

1.0.0:
Initial Version