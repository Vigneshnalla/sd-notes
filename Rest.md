
# API, REST API, and HTTP Methods

## API
An API (Application Programming Interface) allows interaction between systems by following a set of standards and protocols to share features, information, and data. It acts as an interface between different applications.

## REST API
A REST API is an architectural style used to develop web applications, using HTTP protocols as a communication interface. Data is transferred through HTTP methods.

REST is a way for different systems to communicate with each other and exchange information securely. The five main methods used in a REST API are:

- **GET**: Retrieves a specific resource or collection of resources.
- **POST**: Creates a new resource.
- **PUT**: Updates an existing resource.
- **DELETE**: Removes a specific resource.
- **PATCH**: Partially updates an existing resource.

REST primarily uses **JSON** or **plain text** for data exchange, which is lightweight and easy to parse. SOAP, on the other hand, relies on **XML**, which is verbose and requires more bandwidth to transmit.

## URL and URI

- **URL (Uniform Resource Locator)**: A URL is the address of a resource. It identifies the resource and specifies how to access it. In an API, the URL is often called the base URL, which serves as the starting address used for every request to the API.
  
- **URI (Uniform Resource Identifier)**: A URI is used in the URL to specify which resource the client would like to access in a request. It uniquely identifies a resource on the internet or within a system.

## Parameters

- **Body Parameters**: The body of the request contains all the data that the server needs to successfully process the request. Body parameters are only used in requests such as `create` or `update`.
  
- **Path Parameter**: Example: `/restaurant/1/`. It is used to identify a specific resource.
  
- **Query Parameter**: Example: `/products?id=1`. It is used for filtering, searching, pagination, or sorting results. Multiple parameters can be used simultaneously.

| Feature            | Path Parameter          | Query Parameter             |
|--------------------|-------------------------|-----------------------------|
| **Purpose**        | Identify a specific resource | Modify or filter the response |
| **Location**       | Part of the URL path    | After `?` in the URL         |
| **Mandatory**      | Yes                     | No                          |
| **Format**         | `/users/{id}`           | `/users?id=123&status=active`|
| **Example Use**    | `/users/123` (User ID = 123) | `/users?status=active` (Filter users) |

## Headers
Headers allow sending extra information in a request, such as authentication tokens and content types.

## Status Codes

- **2XX**: Success
- **3XX**: Redirection
- **4XX**: Problem with client
- **5XX**: Problem with server

## HTTP Methods

Every HTTP request should have a URL or URI address and a method.

### Categories of HTTP Methods
1. **Safe HTTP Methods**: These do not change data on the server and always return the same response, no matter how many times they are called. Example: `GET`, `HEAD`.
2. **Idempotent Methods**: These may change data on the server but always return the same response, no matter how many times they are called. Example: `GET`, `HEAD`, `PUT`, `DELETE`, `TRACE`.

> **Note**: All safe operations are idempotent, but not all idempotent methods are safe.

### HTTP Methods Explained:

- **GET**: Used to request information from a resource. Since it only reads the data, it is considered a safe method.
  
- **POST**: Used to create a new resource on the backend server. Data is sent to the server in the request body. Two identical `POST` requests will create two new equivalent resources with different resource IDs. It is neither safe nor idempotent.

- **PUT**: Used to update a resource that exists on the server by sending the updated data as content of the request body. It is idempotent but not safe.

- **PATCH**: Used to partially update a resource. Unlike `PUT`, which typically replaces the entire resource, `PATCH` allows sending only the fields to be updated. It is neither safe nor idempotent.

- **DELETE**: Used to delete a resource on the server. It is idempotent but not safe. Returns 200 or 404 status codes.

- **HEAD**: Retrieves metadata about a resource (e.g., content type, content length, last modified date) without downloading the resource itself. It is lightweight and faster than `GET`. Used for validation and caching mechanisms. Safe and idempotent.

- **OPTIONS**: Describes the communication options available for a specific resource or the server as a whole. It provides information about supported HTTP methods and other capabilities of the API. It is used in Cross-Origin Resource Sharing (CORS) to determine if the actual request is allowed by the server. Safe and idempotent.

- **TRACE**: Used to debug issues with how HTTP requests are being transmitted through the network. It shows how a request is processed and whether any transformations have been made by proxies or other intermediaries.

