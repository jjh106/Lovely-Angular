### getDay

```javascript
var dayNames = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
 $scope.day = dayNames[new Date().getDay()];
```

> new Date().getDay()의 반환값은 0~6이 나와 dayNames의 인덱스로 결과값을 반환한다.

자주 쓰자.