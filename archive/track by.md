## track by

```html
<ul>
  <li ng-repeat="value in array track by $index">
    <p>{{ value.title }}</p>
    <p>{{ value.date }}</p>
  </li>
</ul>
```

> 자바스크립트에서 배열은 중복값을 허용한다.
>
> 예를 들어 [0,0,1]에 중복되는 0이 존재한다. track by를 작성해 주지 않으면 별개의 값으로 인식되나 키값은 
>
> 중복값을 허용하지 않는다. 따라서 순회를 3번 하지만 값은 두 개 밖에 없다.
>
> $index(위치)를 사용하자.