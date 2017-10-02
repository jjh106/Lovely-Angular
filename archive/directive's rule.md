## directive's rule

#### 1. restrict

html에서 디렉티브를 사용하기 위한 DOM 엘리먼트의 속성을 설정.

(restrict 규칙을 생략할 경우 default값은 'A' 효과를 나타낸다.)

> E : element, <my-example>
>
> A : attribute, <div my-example>
>
> C : class, <div class=my-example>
>
> M : comment, <!-- directive: my-example -->

---

#### 2. template 

html의 디렉티브를 사용한 부분에 보여줄 내용으로 In-Line value를 설정.

---

#### 3. templateUrl

template이 길어질 경우 별도의 html파일로 분리해서 관리하기 위한 option.

이 때 index.html 위치를 기준으로 로드할 html의 상대위치를 정의한다.

---

#### 4. replace

디렉티브를 사용한 html의 태그에 template 또는 templateUrl에 포함된 내용을 추가할지 교체할지를 설정.

true로 설정할 경우 html의 디렉티브를 사용한 태그를 template 또는 templateUrl에 작성된 내용으로 교체한다.

---

#### 5. priority

디렉티브 별로 compile()과 link()의 호출 우선순위를 지정한다. (default 값은 0)

값이 클 수록 우선순위가 높고 먼저 호출된다.

---

#### 6. transclude

ng-transclude를 이용하여 template 또는 templateUrl에서 디렉티브 내의 원본 내용을 포함시킬지 결정.

true로 설정 시 디렉티브에 포함된 원본 내용을 template의 ng-transclude를 사용한 곳으로 포함.

```html
<html ng-app="exampleDirective">
  <body>
    <div ng-controller="Ctrl">
      <my-example>Hello AngularJS</my-example>
    </div>
  </body>  
</html>
```

```javascript
angular
  .module('exampleDirective', [])
  .controller('Ctrl', function($scope){
    $scope.person = {
      name: 'jason',
      address: 'Seoul'
    };
  })
  .directive('myExample', function(){
    return {
      restrict: 'E',
      template: '<div>Name: {{ person.name }} </br> Address: {{ person.address }} </br> <span ng-transclude></div>',
      transclude: true
    };
  });
```

```
<!-- 결과 -->
Name: jason
Address: Seoul
Hello AngularJS
```

---

#### 7. scope (어렵다..)

디렉티브의 scope를 설정

* scope : false는 새로운 scope 객체를 생성하지 않고 부모가 가진 같은 scope 객체를 공유 (default)
* scope : true는 새로운 scope 객체를 생성하고 부모 scope 개체를 상속.
* scope : {...}는 isolate/isolated scope를 새롭게 생성.

scope : {...}는 재사용 가능한 컴포넌트를 만들 때 사용하는데 컴포넌트가 parent scope의 값을 read/write하지 못하게 하기 위함이다. parent scope에 접근하고 싶을 경우 Binding전략(=, @, &)를 이용한다.

##### Binding 전략

* = : 부모 scope의 property와 디렉티브의 property를 data binding하여 부모 scope에 접근
* @ : 디렉티브의 attribute value를 {{}}방식을 이용해 부모 scope에 접근



*=을 이용한 예*

```html
<div ng-controller="Ctrl">
  <my-directive company-info="the"></my-directive>  
</div>
```

```javascript
angular
  .module('testDirective', [])
  .controller('Ctrl', function($scope){
    $scope.the = {name: 'the'};
  })
  .directive('myDirective', function(){
    return {
      restrict: 'E',
      scope: {
        myCompany: '=companyInfo'
      },
      template: 'Name: {{ myCompany.name }}'
    };
  });
```

1. 부모 scope의 the에 접근하기 위해 html에서 'company-info' attribute에 부모 scope의 data인 the를 세팅
2. 디렉티브 선언부에서는 scope: {...}옵션을 사용하여 isolate scope를 생성하고 '='을 이용하여 template에서 사용 할 local변수명을 myCompany로 지정하였다.
3. template에서는 scope 옵션에 설정한 myCompany로 부모 scope의 data접근이 가능하다.



*@을 이용한 예*

```html
<div ng-controller="Ctrl">
  <my-directive company-info="{{ the }}">
    {{ locate }}
  </my-directive>
</div>
```

```javascript
angular
  .module('testDirective', [])
  .controller('Ctrl', function($scope){
    $scope.name = 'the';
    $scope.locate = 'Seoul';
  })
  .directive('myDirective', function(){
    return {
      restrict: 'E',
      scope: {
        name: '@companyInfo'
      }
    };
  });
```

@방식은 scope의 내용을 string으로 치환한 것과 같은 효과를 가진다. (company-info='the')

---

계속 추가.............