# Response

The `Response` class empowers you to construct varied responses to deliver to the user's browser in your Floky applications. It offers convenient methods to handle various response types effectively.

## Key Methods

- **`json(array $data = [])`:**
    - Sets the response content type to `application/json`.
    - Encodes the provided data as a JSON string.
    - Sends the JSON response to the browser.
    - Frequently employed for API endpoints.

- **`html(string $content, int $statusCode = 200)`:**
    - Sets the HTTP status code (defaulting to 200).
    - Outputs the specified HTML content directly to the browser.
    - Ideal for rendering views and static HTML responses.

- **`redirect(string $url, int $statusCode = 302)`:**
    - Sets a redirect header with the given URL.
    - Uses a default status code of 302 (temporary redirect).
    - Redirects the user's browser to the specified URL.

- **`text(string $text, int $statusCode = 200)`:**
    - Sets the content type to `text/plain`.
    - Sets a custom HTTP status code (defaulting to 200).
    - Outputs plain text content to the browser.

**Example Usage:**

```php
<?php

// Returning a JSON response with user data
return Response::json(['name' => 'John Doe', 'email' => 'johndoe@example.com']);

// Rendering a view and sending an HTML response
$content = view('welcome', ['name' => $user->name]);
return Response::html($content);

// Redirecting to the home page
return Response::redirect('/');
```

## Using `response()` Helper

This helper function provides an instance of the currently used `Response` object. This allows you to chain method calls on the response object, leading to more concise and readable code.

**Example Usage:**

```php
<?php

// Returning a JSON response with user data (equivalent to Response::json($data))
return response()->json($data);

// Chaining methods for a more complex response
return response()->json($data)->setStatusCode(401); // Set JSON data and status code
```

## Benefits of the Helper

- **Improved Code Readability:** Chaining methods makes the code flow clearer and easier to understand.
- **Reduced Repetition:** Eliminates the need to repeatedly call `response()` before each method.
- **Simplified Complex Responses:** Facilitates building more intricate responses by chaining multiple methods.


## In Conclusion

The `Response` class simplifies response handling in Floky, enabling you to generate diverse response types with ease. It proves instrumental in crafting informative and engaging user experiences within your web applications.
The `response()` helper adds another layer of convenience to response creation in Floky. By leveraging this helper, you can streamline your code, enhance readability, and craft effective user interactions within your applications.
