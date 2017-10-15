### ng-class

```html
<span ng-class="warningLevel()">{{incompleteCount()}}</span>
```

```javascript
$scope.warningLevel = function(){
  return $scope.incompleteCount() < 3 ? "label-success" : "label-warning";
}
```

---

```javascript
angular.module('')
       .controller('...', fnName);
function fnName() {
  var selectedCategory = null;
  $scope.getCategoryClass = function(category){
    var activeClass = 'btn';
    return selectedCategory == category ? activeClass : "";
  }
}
```

```html
<a ng-repeat="item in data.products" ng-class="getCategoryClass(item)">{{item}}</a>
```

