# Routing

## Routing in Floky

Routing plays a crucial role in any web application, defining how URLs map to specific controller actions. Floky offers a flexible and intuitive routing system that allows you to define routes in two ways.

## Using Routing Attributes

You can decorate controller methods with routing attributes to define routes and their corresponding HTTP methods. Floky provides the following routing attributes:

- `#[Get(url: '/path', name: 'routeName', middlewares: [])]`
- `#[Post(url: '/path', name: 'routeName', middlewares: [])]`
- `#[Put(url: '/path', name: 'routeName', middlewares: [])]`
- `#[Patch(url: '/path', name: 'routeName', middlewares: [])]`
- `#[Delete(url: '/path', name: 'routeName', middlewares: [])]`
- `#[MatchWith(['GET', 'POST'], url: '/path', name: 'routeName', middlewares: [])]`

**Example :**

```php
<?php

namespace App\Http\Controllers;

use Floky\Http\Requests\Request;
use Floky\Routing\Attributes\Get;

class WelcomeController extends Controller
{

    #[Get(url: '/welcome', name: 'welcome')]
    public function index(Request $request) {

        return view('welcome');
    }
}
```

In this example, the `WelcomeController` has an `index` method decorated with the `#[Get]` attribute. This method handles GET requests to the `/welcome` URL. The `middlewares` option specifies that the `first` middleware should be executed before the controller method.

## Declaring Routes in Route Files

You can also define routes in the `web.php` and `api.php` files located in the `routes` directory. These files use the Laravel Route facade to define routes.

**Example:**

```php
<?php

Route::get('/', function (Request $request) {

    return view('welcome');

});
```

This route defines a GET route to the `/` URL that renders the `welcome` view. The `middleware` method is used to assign the `first` middleware to this route.

## Benefits of Routing Attributes

- **Improved readability:** Decorating controller methods with attributes makes your code more readable and easier to understand.
- **Reduced boilerplate:** You can avoid defining routes in separate files, reducing boilerplate code.
- **Closer association:** Routing logic is closely associated with the controller methods it handles.

## Using Route Files

While routing attributes offer a concise and modern approach, defining routes in separate files can be beneficial in certain situations:

- **Large applications:** For large applications with many routes, organizing routes in separate files can improve readability and maintainability.
- **Separation of concerns:** It allows you to separate routing logic from controller logic, promoting cleaner code organization.

## Conclusion

Floky's routing system provides flexibility and convenience. You can choose the approach that best suits your application's needs and preferences. Consider using routing attributes for smaller applications and simpler routing logic, while larger applications may benefit from defining routes in separate files.