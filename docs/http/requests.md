# The Request Object

The `Request` object plays a crucial role in Floky applications, providing access to information about the incoming HTTP request. You can inject the `Request` object into controller methods to retrieve user input, headers, and other request data.  

## Request Injection

Floky controllers can receive the `Request` object as an argument in their methods. This allows you to access various request details within your controller logic.

Here's an example:

```php
<?php

namespace App\Http\Controllers;

class WelcomeController extends Controller
{

    #[Get(url: '/welcome', name: 'welcome')]
    public function index(Request $request) {

        $name = $request->get('name'); // Accessing a GET parameter
        $message = $request->all();   // Getting all request data

        // ...
    }
}
```

## Request Methods

The `Request` object provides several methods to access different aspects of the HTTP request:

- `input(string $key, $default = null)`: Retrieves a specific value from the request body (either GET or POST data). If the key doesn't exist, it returns the default value.
- `get(string $key = null, $default = null)`: Retrieves a value from the GET request data. If no key is provided, it returns the entire GET data array.
- `post(string $key = null, $default = null)`: Retrieves a value from the POST request data. If no key is provided, it returns the entire POST data array.
- `only(array $keys)`: Returns a subset of the request data containing only the specified keys.
- `all()`: Returns an array containing all request data merged from GET, POST, and other sources.
- `validator(array $rules, array $messages = [])`: Creates a validator instance using the BlakvGhost PHPValidator library to validate request data against defined rules. You can specify custom error messages as well.
- `validate(array $rules, array $messages = [])`: Validates request data against defined rules and throws an exception if validation fails. Alternatively, consider using the `back` method for redirecting with errors.
- `back(mixed $data = [])`: Redirects the user back to the previous page (using the `Referer` header) and stores the provided data in the session for displaying errors or other information.
- `getUri()`: Returns the current request URI.
- `getReferer()`: Returns the URL from which the user originated the request (based on the `Referer` header).
- `getUrl()`: Alias for `getUri()`.
- `getMethod()`: Returns the HTTP method used for the request (GET, POST, PUT, etc.).
- `isMethod(string $method)`: Checks if the current request method matches the provided method.
- `isGet()`, `isPost()`, `isPut()`, etc.: Convenient methods to check if the current request uses the specific HTTP method.
- `header()`: Returns a `Header` object that provides access to request headers.

## Accessing Request Headers in Floky

The `Header` class within Floky's `Request` component provides functionalities to access and manipulate HTTP headers sent by the client in the request : 

* `get(string $headerName)`: Retrieves the value of a specific header by name. The header name is converted to uppercase and underscores are replaced with hyphens for compatibility with the server variable format (e.g., `Content-Type` becomes `HTTP_CONTENT_TYPE`). This method returns the sanitized value of the header or `null` if it doesn't exist.
* `getAll()`: Returns an associative array containing all request headers. The header names are converted to a more readable format (e.g., `Content-Type` becomes `contentType`). The values are also sanitized before being returned.

**Common Header Checks:**

* `acceptJson()`: Checks if the request accepts JSON content type (`application/json`) by examining the `Accept` header.
* `isAjax()`: Determines if the request is an AJAX request by checking the presence and value of the `X-Requested-With` header (`XMLHttpRequest`).

**Setting Headers:**

* `set(string $headerName, string $headerValue)`: Sets a new HTTP header in the response. This method allows you to define custom headers to be sent back to the client.

**Additional Information:**

* `isSecure()`: Checks if the current request is using a secure HTTPS connection.
* `getUserAgent()`: Returns the user agent string sent by the client's browser.
* `getReferer()`: Retrieves the referring URL from the `Referer` header if present.
* `getClientIp()`: Returns the client's IP address based on the `REMOTE_ADDR` server variable.
* `getBearer()`: Extracts the bearer token from the `Authorization` header if the request uses Bearer token authentication. It checks for a prefix of `"Bearer "` and returns the remaining string as the token.

## Additional Features

**File Uploads**

The `Files` trait within Floky's `Request` component provides functionalities to handle file uploads submitted through forms. It's important to note that this trait is used within the `Request` object, not as a standalone class.

**Checking for Uploaded Files:**

* `hasFile(string $inputName)`: This method checks if a specific file input named `$inputName` exists in the uploaded files array (`$_FILES`). It returns `true` if the file was uploaded and `false` otherwise.

**Accessing Uploaded File Details:**

* `getFile(string $inputName)`: If a file with the given `$inputName` was uploaded, this method retrieves the corresponding information from the `$_FILES` array. It returns an associative array containing details about the uploaded file, such as:
    * `name`: The original filename of the uploaded file.
    * `type`: The MIME type of the uploaded file.
    * `tmp_name`: The temporary filename of the uploaded file on the server.
    * `error`: An error code indicating any issues during the upload process (refer to PHP documentation for specific error codes).
    * `size`: The size of the uploaded file in bytes.

**Moving Uploaded Files:**

* `moveUploadedFile(string $inputName, string $destination)`: This method attempts to move the uploaded file identified by `$inputName` to a specified `$destination` path. It performs the following actions:
    * Checks if a file with the provided `$inputName` exists using `hasFile`.
    * Verifies if the upload was successful by checking the `error` code in the file information (should be `UPLOAD_ERR_OK`).
    * Appends the original filename to the provided `$destination` path to avoid naming conflicts.
    * Uses the `move_uploaded_file` PHP function to move the temporary file to the specified destination.
    * If the move operation is successful, it returns the complete destination path where the file is now stored.
    * If any errors occur during the process, it returns `null`.


## Conclusion

The `Request` object is an essential tool for handling user interactions within your Floky applications. By leveraging its methods, you can effectively retrieve request data, validate user input, and implement various request-related functionalities.
