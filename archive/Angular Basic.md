## Angular Basic

***Module** 

기능적으로 비슷한 것들을 모아 하나의 모듈로 만든다. 모듈끼리 서로 의존관계가 있는 경우엔 다른 모듈을 주입해서 사용할 수 있다.

***Controller는 반드시 view의 비즈니스 로직을 다룰 때만 사용해야한다.

***Service** 

Controller와 다르게 재사용할 수 있는 비즈니스로직을 서비스라고 한다.

어플리케이션의 데이터를 관리하는 용도로 사용하는 것이 좋다.

---

### # Directive

#### **ng-app**

> "여기서 부터 앵귤러 코드가 사용된다" 라고 선언하는 디렉티브.

#### **ng-init**

> 자바스크립트 변수나 함수를 초기화하는데 사용 하는 디렉티브.
>
> ng-init는 프로토타입 만들 때 주로 사용하고 아래의 경우는 모듈과 컨트롤러를 사용해 구조를 변경해야 함.

```html
<body ng-app ng-init="name = 'Jason'">
  <h1>Hello {{ name }}!</h1>
</body>
```

---

### # module && controller

```javascript
// script.js
// 필요한 모듈과 컨트롤러를 생성하자.

(function(){
  var app = angular.module('todo', []);
})();
```

> angular.module() - 모듈을 정의하는 함수로 첫 번째 파라미터에는 모듈의 이름을 지정해준다.
>
> ng-app="todo"라는 모듈명을 할당해 적용해준다.



```javascript
// script.js
// 필요한 모듈과 컨트롤러를 생성하자.

(function(){
  var app = angular.module('todo', []);
  
  app.controller('TodoCtrl', ['$scope', function($scope){
   
  }]);
})();
```

> app.controller()의 첫 파라미터는 컨트롤러의 이름, 두 번째 파라미터는 함수를 지정하고 배열로 감싼다.
>
> angular에서 컨트롤러를 만들 때 보통 첫 문자를 대문자로 시작한다.
>
> $scope변수는 컨트롤러와 view(html파일) 사이의 연결고리 같은 역할을 한다.



```javascript
// script.js
app.controller('TodoCtrl',['$scope', function($scope){
  $scope.name = 'Jason';
}]);
```

```html
<!-- index.html -->
<body ng-app="todo" ng-controller="TodoCtrl">
  <h1>Hello {{ name }}!</h1>
</body>
```

> name값으로 Jason을 설정해주고
>
> 기존에 ng-init로 만들었던 내용은 지우고 컨트롤러를 할당한다.
>
> 컨트롤러의 $scope.name의 값이 출력된다.

---

### # Todolist 

```html
<body>
  <h1>Todo</h1>
  <input type="text" ng-model="todo.title">
  <input type="checkbox" ng-model="todo.completed">
  <date>{{ todo.createdAt }}</date>
</body>
```

```javascript
var app = angular.module('todo', []);

app.controller('TodoCtrl', function($scope){
  $scope.todo = {
    title: '앵귤러 배우기',
    completed: false,
    createdAt: Date.now()
  }
});
```



#### ng-repeat

```html
<!-- index.html -->
<body ng-app="todo" ng-controller="TodoCtrl">
  <ul>
    <li ng-repeat="todo in todos">
      <input type="text" ng-model="todo.title">
      <input type="checkbox" ng-model="todo.completed">
      <date>{{ todo.createdAt }}</date>
    </li>
  </ul>
</body>
```

```javascript
// script.js
var app = angular.module('todo', []);

app.controller('TodoCtrl', function($scope){
  $scope.todos = [
    {
      title: '부트스트랩 학습',
      completed: false,
      createdAt: Date.now()
    },
    {
      title: '앵귤러 학습',
      completed: false,
      createdAt: Date.now()
    },
    {
      title: '잠자기',
      completed: true,
      createdAt: Date.now()
    }
  ];
})
```



#### ngFilter

```html
<date>{{ todo.createdAt | date: 'yyyy-MM-dd' }}</date>
```



#### ng-click

```html
<!-- index.html -->
<li ng-repeat="todo in todos">
  <input type="text" ng-model="todo.title">
  <input type="checkbox" ng-model="todo.completed">
  <button ng-click="remove(todo)">삭제</button>
  <date>{{ todo.createdAt | date: 'yyyy-MM-dd' }}</date>
</li>
```

```javascript
// script.js
var app = angular.module('todo', []);
app.controller('TodoCtrl', function($scope){
  $scope.todos = [
    {
      title: '부트스트랩 학습',
      completed: false,
      createdAt: Date.now()
    },
    {
      title: '앵귤러 학습',
      completed: false,
      createdAt: Date.now()
    },
    {
      title: '잠자기',
      completed: true,
      createdAt: Date.now()
    }
  ];
  
  $scope.remove = function(todo){
    // find todo index in todos
    var idx = $scope.todos.findIndex(function(item){
      return item === todo;
    });
    // remove from todos
    if(idx > -1){
      $scope.todos.splice(idx, 1);
    }
  }
});
```



#### Filter Button

> 완료 항목, 미완료 항목, 모든 항목을 보여주는 기능을 하는 버튼

```html
<!-- index.html -->

<div class="container">
  <h1>해야 할 목록</h1>
  <ul class="list-unstyled">
    <li ng-repeat="todo in todos | filter: statusFilter">
      <div class="input-group">
        <span class="input-group-addon">
          <input type="checkbox" ng-model="todo.completed">
        </span>
        <input type="text" class="form-control" ng-model="todo.title">
        <span class="input-group-btn">
          <button class="btn tbtn-danger" type="button" ng-click="remove(todo)">삭제</button>
        </span>
      </div>
      <date>{{ todo.createdAt | date:'yyyy-MM-dd HH:mm:ss' }}</date>
    </li>
  </ul>
  
  <button class="btn btn-primary" ng-click="statusFilter={completed: true}">Completed</button>
  <button class="btn btn-primary" ng-click="statusFilter={completed: false}">Active</button>
  <button class="btn btn-primary" ng-click="statusFilter={}">All</button>
</div>
```

> ng-repeat에 필터(|)를 사용



#### form만들기

```html
<!-- index.html -->

<div class="container">
  <h1>해야 할 목록</h1>
  
  <form name="TodoForm" ng-submit="add(newTodoTitle)">
    <div class="input-group">
      <input type="text" class="form-control" ng-model="newTodoTitle" placeholder="입력...">
      <span class="input-group-btn">
        <button class="btn btn-success" type="submit">추가</button>
      </span>
    </div>  
  </form>
  
  <ul class="list-unstyled">
    <li ng-repeat="todo in todos | filter: statusFilter">
      <div class="input-group">
        <span class="input-group-addon">
          <input type="checkbox" ng-model="todo.completed">
        </span>
        <input type="text" class="form-control" ng-model="todo.title">
        <span class="input-group-btn">
          <button class="btn tbtn-danger" type="button" ng-click="remove(todo)">삭제</button>
        </span>
      </div>
      <date>{{ todo.createdAt | date:'yyyy-MM-dd HH:mm:ss' }}</date>
    </li>
  </ul>
  
  <button class="btn btn-primary" ng-click="statusFilter={completed: true}">Completed</button>
  <button class="btn btn-primary" ng-click="statusFilter={completed: false}">Active</button>
  <button class="btn btn-primary" ng-click="statusFilter={}">All</button>
</div>
```

> angular에서 form을 만들 때 name을 지정할 수 있다
>
> 추가버튼에 ng-click을 사용할 수 있지만 폼이기 때문에 type을 submit로 하고 form에 ng-submit을 사용하여 add함수를 사용하게 만든다.

```javascript
// script.js

var app = angular.module('todo', []);

app.controller('TodoCtrl', function($scope){
  $scope.todos = [
    {
      title: '요가수행',
      completed: false,
      createdAt: Date.now()
    },
    {
      title: '앵귤러 학습',
      completed: false,
      createdAt: Date.now()
    },
    {
      title: '운동하기',
      completed: true,
      createdAt: Date.now()
    }
  ];
  
  $scope.remove = function(todo){
    var idx = $scope.todos.findIndex(function(item){
      return item === todo;
    })
    if(idx > -1){
      $scope.todos.splice(idx, 1);
    }
  };
  
  $scope.add = function(newTodoTitle){
    var newTodo = {
      title: newTodoTitle,
      completed: false,
      createdAt: Date.now()
    } ;
    
    $scope.todos.push(newTodo);
    
    $scope.newTodoTitle = "";
  }
})
```



