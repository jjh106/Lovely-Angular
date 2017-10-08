### ng-class

```html
<span ng-class="warningLevel()">{{incompleteCount()}}</span>
```

```javascript
$scope.warningLevel = function(){
  return $scope.incompleteCount() < 3 ? "label-success" : "label-warning";
}
```

