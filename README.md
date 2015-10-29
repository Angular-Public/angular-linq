# angular-linq
linq.js library for AngularJS
http://linqjs.codeplex.com/

Latest Version: 1.0.0

Install:

```
bower install angular-linq
```

Injector: ``` $linq ```
Accessing Enumerable: ``` $linq.Enumerable() ```


Example Usage:

```
(function() {
  'use strict';

  angular.module('mymodule', [])
    .controller('mycontroller', MyController);

  MyController.$inject = [
    '$linq'
  ];

  function MyController(
    $linq
  ) {


    var jsonArray = [{
      "user": {
        "id": 100,
        "screen_name": "d_linq"
      },
      "text": "to objects"
    }, {
      "user": {
        "id": 130,
        "screen_name": "c_bill"
      },
      "text": "g"
    }, {
      "user": {
        "id": 155,
        "screen_name": "b_mskk"
      },
      "text": "kabushiki kaisha"
    }, {
      "user": {
        "id": 301,
        "screen_name": "a_xbox"
      },
      "text": "halo reach"
    }]

    var queryResult = $linq.Enumerable().From(jsonArray)
      .Where(function(x) {
        return x.user.id < 200
      })
      .OrderBy(function(x) {
        return x.user.screen_name
      })
      .Select(function(x) {
        return x.user.screen_name + ':' + x.text
      })
      .ToArray();

    console.log("queryResult : ", queryResult);

  }
})();

```
**Example Output:**

queryResult: ["b_mskk:kabushiki kaisha", "c_bill:g", "d_linq:to objects"]





Change History:

1.0.1:
    Fixes to support angular version 1.4.7

1.0.0:
    Initial Version