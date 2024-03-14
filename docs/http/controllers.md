# Controller

Controllers are a fundamental part of the Floky MVC architecture. They handle incoming HTTP requests, interact with models to retrieve or manipulate data, and prepare the data for presentation in views. Controllers provide a layer of abstraction between the routes and the underlying application logic.

## Creating Controllers

Floky provides a convenient command for quickly creating controllers. This command generates a PHP controller file within the `app/Http/Controllers` directory.

Example:

```bash title="Create a new controller"
php floky make:controller WelcomeController
```

This command will create a WelcomeController.php file inside the `app/Http/Controllers` directory. The generated file will contain the following boilerplate code:

```php

<?php

namespace App\Http\Controllers;


class WelcomeController extends Controller
{
    // ...
}
```
## Anatomy of a Controller

A typical Floky controller consists of the following elements:

- **Namespace:** Controllers are typically placed within a namespace that reflects their location within the application. In the example provided, the controller resides in the `App\Http\Controllers` namespace.
- **Inheritance:** Floky controllers inherit from the `Floky\Http\Controllers\Controller` class. This base class provides essential functionalities common to all controllers in your application.
- **Request Handling Methods:** Controllers define methods to handle different HTTP request types (GET, POST, PUT, etc.). These methods are decorated with the `#[Get]`, `#[Post]`, `#[Put]`, or `#[Delete]` attributes from the `Floky\Routing\Attributes` namespace. These attributes specify the HTTP method the method handles and allow you to define the route URL and any middleware to be applied before the method execution.
- **Dependency Injection:** Controller methods can accept arguments through constructor injection or method injection. A common approach is to inject the `Floky\Http\Requests\Request` object to access request data.
- **Model Interaction:** Controllers often interact with models to retrieve or manipulate data. Models represent the data layer of your application and encapsulate the business logic.
- **View Rendering:** Once the controller has processed the request and prepared the data, it returns a view. The view typically represents the user interface (UI) component responsible for presenting the data to the user. The controller uses the `view` function provided by Floky to render the desired view and pass any necessary data to it.

## Example Controller

```php

<?php

namespace App\Http\Controllers;

use Floky\Http\Requests\Request;
use Floky\Routing\Attributes\Get;

class WelcomeController extends Controller
{

    #[Get(url: '/welcome', name: 'welcome')]
    public function index(Request $request) {

        // Simulate some data fetching
        $data = ['message' => 'Welcome to Floky!'];

        return view('welcome', $data);
    }
}
```

In this example, the `WelcomeController` has an `index` method decorated with the `#[Get]` attribute. This method handles GET requests to the `/welcome` route. The `middlewares` option specifies that the `first` middleware should be executed before the controller method. The `index` method receives a `Request` object as an argument, allowing it to access request data. Here, the controller simulates fetching some data and then returns the `welcome` view, passing the `$data` array containing the welcome message.

## Key Points

* Controllers are responsible for handling HTTP requests, interacting with models, and preparing data for views.
* Floky controllers inherit from the `Floky\Http\Controllers\Controller` class.
* Request handling methods are decorated with routing attributes to define the HTTP method and route URL.
* Controllers can leverage dependency injection to access request data and other dependencies.
* Controllers interact with models to manage application data.
* Controllers return views to render the UI based on processed data.
