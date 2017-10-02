### $http (get, post, put, delete)

데이터베이스 -> 백엔드 api -> 앵귤러 서비스 -> 앵귤러 컨트롤러 -> 앵귤러 템플릿 

앵귤러 서비스는 api와 http 통신을 통하여 데이터를 주고 받는 역할을 하고 컨트롤러에서는 서비스를 이용해 가져온 데이터를 템플릿에 뿌려주는 역할을 한다.

```javascript
angular
  .module('todo')
  .factory('todoStorage', function($http){
    var storage = {
      todo = [],
      get: function(callback){
        $http.get('경로')
             .then(
               function success(res){
                 console.log(res);
                 callback(null, angular.copy(res.data, storage.todos));
               },
               function error(err){
                 console.log(err);
                 callback(err);
               }
             );
      }
    }
  })
```



```javascript
$http.get('경로')
     .then(
       function success(res){
         var data = res.data;
         var status = res.status;
         var statusText = res.statusText;
         var headers = res.headers;
         var config = res.config;
     },
       function Error(res){
         var data = res.data;
         var status = res.status;
         var statusText = res.statusText;
         var headers = res.headers;
         var config = res.config;
       });
```

