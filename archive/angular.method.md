## angular.method

*angularJS 유틸리티 메서드.*

#### 1. angular.forEach

```javascript
$scope.incompleteCount = function(){
  var count = 0;
  angular.forEach($scope.todo.items, function(item){
    if(!item.done){
      count++
    }
  });
  return count;
}
```

> $scope.todo.items 배열 내 항목을 순회하며 done 값이 false인 항목의 개수를 계산.

---

#### 2. angular.isString

```javascript
angular.isString("hello");
```

> 문자열인지를 판별하는 메서드로 true, false를 반환.

---

#### 3. angular.lowercase & uppercase

```javascript
console.log("I am " + angular.lowercase("WhiSpeRing"));
```

---

#### 4. angular.extend 

```javascript
var myData = {
  name: "Adam",
  weather: "sunny"
};

var myExtendedObject = {
  city: "London"
};

angular.extend(myExtendedObject, myData);

// Adam London
console.log(myExtendedObject.name);
console.log(myExtendedObject.city);
```

> myData 객체의 모든 속성과 함수를 myExtendedObject로 복사한다.

---

##### *자주 사용하는 것만 추가하고 공식문서 보자.

