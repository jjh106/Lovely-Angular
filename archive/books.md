```html
<!doctype html>
<html>
  <head>
      <link href="https://s3.amazonaws.com/codecademy-content/projects/bootstrap.min.css" rel="stylesheet" />
    <link href='https://fonts.googleapis.com/css?family=Roboto:500,300,700,400' rel='stylesheet' type='text/css'>
    <link href="css/main.css" rel="stylesheet" />

    <script src="//ajax.googleapis.com/ajax/libs/angularjs/1.3.5/angular.min.js"></script>
  </head>
  <body ng-app="myApp">
    <div class="header">
      <div class="container">
        <h1>Book End</h1>
      </div>
    </div>

    <div class="main" ng-controller="MainController">
      <div class="container">

        <h1>{{ title }}</h1>
        <h2>{{ promo }}</h2>

        <div ng-repeat="product in products" class="col-md-6">
          <div class="thumbnail">
            <img ng-src="{{ product.cover }}">
            <p class="title">{{ product.name }}</p>
            <p class="price">{{ product.price | currency }}</p>
            <p class="date">{{ product.pubdate | date }}</p>
            <div class="rating">
              <p class="likes" ng-click="plusOne($index)">{{ product.likes }}</p>
              <p class="dislikes" ng-click="minusOne($index)">{{ product.dislikes }}</p>
            </div>
          </div>
        </div>

      </div>
    </div>

    <div class="footer">
      <div class="container">
        <h2>Available for iPhone and Android.</h2>
        <img src="https://s3.amazonaws.com/codecademy-content/projects/shutterbugg/app-store.png" width="120px" />
        <img src="https://s3.amazonaws.com/codecademy-content/projects/shutterbugg/google-play.png" width="110px" />
      </div>
    </div>


    <!-- Modules -->
    <script src="js/app.js"></script>

    <!-- Controllers -->
    <script src="js/controllers/MainController.js"></script>
  </body>
</html>

```

```javascript
app.controller('MainController', function($scope){
  $scope.title = 'hello angular';
  
  $scope.promo = 'my book';
  
  $scope.products = [
    {
      name: 'The Book of Trees',
      price: 19,
      pubdate: new Date('2014', '03', '08'),
      cover: 'img/the-book-of-trees.jpg',
      likes: 0,
      dislikes: 0
    },
    {
      name: 'Program or be Programmed',
      price: 8,
      pubdate: new Date('2013', '08', '01'),
      cover: 'img/program-or-be-programmed.jpg',
      likes: 0,
      dislikes: 0
    },
    {
      name: 'AngularJS in action',
      price: 10,
      pubdate: new Date('2017', '10', '20'),
      cover: 'img/the-book-of-trees.jpg',
      likes: 0,
      dislikes: 0
    },
    {
      name: 'Javascript30',
      price: 50,
      pubdate: new Date('2018', '05', '15'),
      cover: 'img/program-or-be-programmed.jpg',
      likes: 0,
      dislikes: 0
    }
  ];
  
  $scope.plusOne = function(index){
    $scope.products[index].likes += 1;
  };
  
  $scope.minusOne = function(index){
    $scope.products[index].dislikes += 1;
  }
});
```

