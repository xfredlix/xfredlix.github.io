# Angular 1
- Extends HTML attributes with directives, which have an ng prefix
- The ng-app directive defines an AngularJS application
- The ng-model directive binds the value of HTML controls (input, select, button, textarea) to application data, data goes both ways
- Binds data to HTML view from model with expressions, {{ expression }} or ng-bind="expression"
- When data in the model changes, the view reflects the change, and when data in the view changes, the model is updated as well. This happens immediately and automatically, which makes sure that the model and the view is updated at all times

### Modules
- A container for the different parts of an application
- Created by using the AngularJS function angular.module: var app = angular.module("myApp", []);
- The "myApp" parameter refers to an HTML element in which the application will run
- The [] parameter in the module definition can be used to define dependent modules
- Without the [] parameter, you are not creating a new module, but retrieving an existing one

### Directives
- JavaScript functions that manipulate and add behaviors to HTML DOM elements
- Has a set of built-in directives which offers functionality to your applications, and also lets you create your own directives
- The ng-repeat directive actually clones HTML elements once for each item in a collection
- New directives are created by using the .directive function
- When naming a directive, you must use a camel case name: testOne, but when invoking it, you must use - separated name: test-one
- To invoke the new directive, make an HTML element with the same tag name as the new directive. Can invoke a directive by using Element name: <test-one></test-one>, Attribute: <div test-one></div>, Class: <div class="test-one"></div>, Comment <!-- directive: test-one -->
- Restrict your directives to only be invoked by some of the methods: E for Element name, A for Attribute, C for Class, M for Comment
- Default value is EA, meaning that both element names and attribute names can invoke the directive

### Directive lifecycle
- The compile function allows the directive to manipulate the DOM before it is compiled and linked thereby allowing it to add/remove/change directives, as well as, add/remove/change other DOM elements
- The controller function facilitates directive communication. Sibling and child directives can request the controller of their siblings and parents to communicate information
- The pre-link function allows for private $scope manipulation before the post-link process begins
- The post-link method is the primary workhorse method of the directive
- Compile Phase: Compile Function: parentDir, Compile Function: childDir, Compile Function: grandChildDir
- Controller & Pre-Link Phase: Controller Function: parentDir, Pre-Link Function: parentDir, Controller Function: childDir, Pre-Link Function: childDir, Controller Function: grandChildDir, Pre-Link Function: grandChildDir
- Post-Link Phase: Post-Link Function: grandChildDir, Post-Link Function: childDir, Post-Link Function: parentDir

### Controllers
- Control the data of AngularJS applications, are regular JavaScript Objects
- When you make a controller, you pass the $scope object as an argument
- angular.module('myApp', []).controller('namesCtrl', function($scope) {
  // code
});

### Scope
- The binding part between the HTML (view) and the JavaScript (controller), considered as the model
- An object with the available properties and methods, associated with an element and all of its child elements
- Elements are assigned a scope in 3 ways: a scope is created on an element by a controller or a directive (directives don’t always introduce new scopes), a scope isn’t present on the element, then it’s inherited from its parent, the element isn’t part of an ng-app, then it doesn’t belong to a scope at all
- In the view, you do not use the prefix $scope, you just refer to a property name, like {{carname}}
- All applications have a $rootScope which is the scope created on the HTML element that contains the ng-app directive
- The rootScope is available in the entire application
- If a variable has the same name in both the current scope and in the rootScope, the application uses the one in the current scope

### $digest cycle
- When you write an expression {{aModel}}, behind the scenes Angular sets up a watcher on the scope model, Angular’s built-in directives also do this
- $scope.$watch('aModel', function(newValue, oldValue) {
  //update the DOM with newValue
});
- When the $digest cycle starts, it fires each of the watchers. These watchers check if the current value of the scope model is different from the last calculated value. If yes, then the corresponding listener function executes
- Angular doesn’t directly call $digest(), it calls $scope.$apply(), which in turn calls $rootScope.$digest().
- A digest cycle starts at the $rootScope, and subsequently visits all the child scopes calling the watchers along the way
- Aassume you attach an ng-click directive to a button and pass a function name to it. When the button is clicked, AngularJS wraps the function call within $scope.$apply()
- If Angular cannot detect your changes, then you must call $apply() manually
- The $digest cycle keeps looping until there are no more model changes, or it hits the max loop count of 10. Try to stay idempotent and minimize model changes inside the listener functions
- At a minimum, $digest will run twice even if your listener functions don’t change any models

### Filters
- Formats the value of an expression for display to the user. They can be used in view templates, controllers or services
- Can be added to expressions by using the pipe character | followed by a filter
  <li ng-repeat="x in names | orderBy:'country'">
    {{ x.name + ', ' + x.country }}
  </li>
- Can make your own filters by registering a new filter factory function with your module: .filter
- currency Format a number to a currency format
- date Format a date to a specified format
- filter Select a subset of items from an array, can only be used on arrays, and it returns an array containing only the matching items
- json Format an object to a JSON string
- limitTo Limits an array/string, into a specified number of elements/characters
- lowercase Format a string to lower case
- number Format a number to a string
- orderBy Orders an array by an expression
- uppercase Format a string to upper case

### Services
- A function, or object, that is available for, and limited to, your AngularJS application
- Can make your own service, or use one of the many built-in services
- Once you have created a service, and connected it to your application, can use the service in any controller, directive, filter, and other services
- In order to use the service in the controller, it must be defined as a dependency
- $location service has methods which return information about the location of the current web page
- $http service makes a request to the server, and lets your application handle the response
- $timeout service is AngularJS' version of the window.setTimeout function

### Form Validation
- Client-side form validation for input data
- Use the HTML5 attribute required to specify that the input field must be filled out
- http://www.w3schools.com/angular/angular_validation.asp

### Routing
- ngRoute module helps your application to become a Single Page Application
- Must include the AngularJS Route module: <script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.4.8/angular-route.js"></script>
- Must add the ngRoute as a dependency in the application module: var app = angular.module("myApp", ["ngRoute"]);
- Now your application has access to the route module, which provides the $routeProvider
- app.config(function($routeProvider) {
    $routeProvider
    .when("/", {
        templateUrl : "main.html"
    })
    .when("/london", {
        templateUrl : "london.html",
        controller : "londonCtrl"
    })
    .otherwise({
        templateUrl: "paris.html"
    });
- Your application needs a container to put the content provided by the routing, which is the ng-view directive
- Can only have one ng-view directive
- 3 different ways to include the ng-view directive in your application: <div ng-view></div>, <ng-view></ng-view>, <div class="ng-view"></div>
- Use the otherwise method, which is the default route when none of the others get a match

# Lifecycle
- 3 phases: bootstrap, compilation, and runtime
- The three phases of the life cycle of an AngularJS application happen each time a web page is loaded in the browser

### The Bootstrap Phase
- First phase, occurs when the AngularJS JavaScript library is downloaded to the browser
- AngularJS initializes its own necessary components and then initializes your module, which the ng-app directive points to. The module is loaded, and any dependencies are injected into your module and made available to code within the module

### The Compilation Phase
- Initially when a web page is loaded, a static form of the DOM is loaded in the browser. During the compilation phase, the static DOM is replaced with a dynamic DOM that represents the AngularJS view
- Second phase, traverses the static DOM and collecting all the directives and then linking the directives to the appropriate JavaScript functionality in the AngularJS built-in library or custom directive code. The directives are combined with a scope to produce the dynamic or live view

### The Runtime Data Binding Phase
- Final phase, which exists until the user reloads or navigates away from a web page. At that point, any changes in the scope are reflected in the view, and any changes in the view are directly updated in the scope, making the scope the single source of data for the view
- AngularJS behaves differently from traditional methods of binding data. Traditional methods combine a template with data received from the engine and then manipulate the DOM each time the data changes. AngularJS compiles the DOM only once and then links the compiled template as necessary, making it much more efficient than traditional methods