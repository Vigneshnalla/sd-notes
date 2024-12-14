
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

- **GET**: Used to request information from a resource. Since it only reads the data, it is considered a safe method. [200]
  
- **POST**: Used to create a new resource on the backend server. Data is sent to the server in the request body. Two identical `POST` requests will create two new equivalent resources with different resource IDs. It is neither safe nor idempotent.[201]

- **PUT**: Used to update a resource that exists on the server by sending the updated data as content of the request body. It is idempotent but not safe.[200,204]

- **PATCH**: Used to partially update a resource. Unlike `PUT`, which typically replaces the entire resource, `PATCH` allows sending only the fields to be updated. It is neither safe nor idempotent.[200 or 204]

- **DELETE**: Used to delete a resource on the server. It is idempotent but not safe. Returns 200 or 404 status codes.[200 204]

- **HEAD**: Retrieves metadata about a resource (e.g., content type, content length, last modified date) without downloading the resource itself. It is lightweight and faster than `GET`. Used for validation and caching mechanisms. Safe and idempotent.[200]

- **OPTIONS**: Describes the communication options available for a specific resource or the server as a whole. It provides information about supported HTTP methods and other capabilities of the API. It is used in Cross-Origin Resource Sharing (CORS) to determine if the actual request is allowed by the server. Safe and idempotent.[200]

- **TRACE**: Used to debug issues with how HTTP requests are being transmitted through the network. It shows how a request is processed and whether any transformations have been made by proxies or other intermediaries.



### What is a Proxy?
A proxy is an intermediary server that sits between a client (such as a web browser) and the destination server (like a website). When a client makes a request, it goes through the proxy, which then forwards the request to the destination server. Once the server responds, the proxy sends the response back to the client.

#### Types of Proxies:
1. **Forward Proxy**:  
   - Forwards requests from the client to the destination server.  
   - Common use cases: Anonymous browsing, accessing blocked content, caching to improve performance.

2. **Reverse Proxy**:  
   - Sits in front of one or more backend servers and handles requests from clients.  
   - Common use cases: Load balancing, caching, security (to hide backend servers).

3. **Transparent Proxy**:  
   - Does not modify the request or response.  
   - The client is unaware of the proxy being used.

4. **Anonymous Proxy**:  
   - Hides the client's identity by masking its IP address.

#### Benefits of Proxies:
- **Security**: Proxies can filter content and block malicious sites.
- **Privacy**: They help protect the client's identity by masking its IP address.
- **Access Control**: Proxies can restrict access to certain websites or services.
- **Caching**: Improves response time and reduces bandwidth usage.
- **Load Balancing**: Distributes requests across multiple servers to improve performance.

---

### What is TLS (Transport Layer Security)?
TLS is a cryptographic protocol designed to secure communication over a network. It ensures that the data exchanged between a client and a server remains confidential, integral, and authentic.

#### How TLS Works:
- **Encryption**: TLS encrypts the data sent between the client and the server. Even if someone intercepts the data, they cannot read it without the proper decryption keys.
- **Integrity**: TLS ensures that the data cannot be tampered with during transmission. Any changes to the data will be detected by comparing checksums (hash values).
- **Authentication**: TLS allows the client to verify the identity of the server through digital certificates issued by a trusted certificate authority (CA).

#### Key Steps in a TLS Handshake:
1. **Client Hello**: The client sends a message to the server with the encryption algorithms it supports.
2. **Server Hello**: The server responds with its chosen encryption algorithms and its digital certificate containing its public key.
3. **Key Exchange**: The client and server exchange keys to establish a secure communication channel.
4. **Session Established**: After the handshake, the data is securely transmitted.

#### Benefits of TLS:
- **Confidentiality**: Data is encrypted and cannot be read by unauthorized parties.
- **Data Integrity**: The data cannot be altered during transmission.
- **Authentication**: The client can verify the legitimacy of the server.

---

### What is the CONNECT Method?
The CONNECT method is used by a web client when it needs to talk to a proxy server and the final URI (Uniform Resource Identifier) starts with https://. This method tells the proxy to open a raw TCP connection to the destination server (e.g., www.google.com:443), and all data sent after that is simply forwarded through that connection without interpretation. This method is commonly used for HTTPS communication.

#### How CONNECT Works:
1. **Proxy Communication**: The client sends the CONNECT method to the proxy server, requesting it to establish a connection to the destination server (e.g., www.google.com:443).
2. **Forwarding Data**: The proxy forwards all data between the client and the destination server without inspecting or altering it. The data is often encrypted using TLS (HTTPS), ensuring the content is secure.

#### Why Use CONNECT?
- **Encrypted Communication**: CONNECT allows encrypted communication (e.g., HTTPS) even through proxies. The proxy forwards the encrypted data but cannot read it.
- **Not Dependent on TLS**: Although CONNECT is often used with TLS, it does not inherently rely on it. It’s primarily about forwarding raw data between the client and the server.
- **Proxy Security Risks**: Proxies using CONNECT need to be careful, as any data (including harmful requests like an SSH attack or spam) can pass through without inspection. It's up to proxies to manage security risks.

---

### The Role of TLS in Data Integrity:
When TLS is used, data integrity ensures that the data cannot be tampered with while it’s in transit. Any alteration (e.g., modification, addition, or deletion of data) will be detected.

#### How Data Integrity Works in TLS:
- **Checksums (Hashes)**: Both the client and server compute a checksum (also called a hash or message digest) for the transmitted data. The checksum is unique to the content of the data.
- **Tampering Detection**: If a hacker intercepts and changes the data, the checksum will no longer match. This mismatch indicates that the data has been tampered with.
- **Rejection of Tampered Data**: If the integrity check fails (i.e., the checksum does not match), the data is rejected, and the transmission is considered compromised.


# Authentication Methods

### Types of Authentication:
- **Basic and Bearer**
- **API Keys**
- **OAuth (2.0)**
- **OpenID Connect**

---

## Basic Authentication
- Rarely recommended due to inherent security vulnerabilities.
- Simple and straightforward method.
- The sender includes a username and password in the request headers.

### Example:
In headers:
```http
Authorization: Basic bdkadfjuiujkdsaZq=
```
(Encoded with Base64)

### Key Features:
- Does not require cookies, session IDs, login pages, or other specialized solutions.
- Uses the HTTP header directly, eliminating the need for handshakes or complex response systems.

---

## Bearer Authentication
- Also known as **Token Authentication**.
- HTTP authentication scheme involving security tokens ("bearer tokens").
- Grants access to specific resources or URLs via a bearer token.

### How It Works:
- A bearer token, a complex string generated by the server upon login, is used as authorization to access protected resources.
- First introduced in OAuth 2.0 (RFC-6750), but can also be used independently of OAuth.

### Key Features:
1. **Secure Communication**:
   - Should only be utilized with HTTPS to ensure secure communication.
2. **No Identity Verification**:
   - Since bearer tokens do not require a signature, anyone with access to the token can use it. Hence, keeping tokens secure is crucial.
3. **Short-Lived Tokens**:
   - Typically expire after a short period, requiring a new token via refresh tokens or re-authentication.

### Transmission:
- Always use HTTPS to prevent token interception during transmission.

---

## OAuth (2.0)
- Allows clients to access protected resources by obtaining an **access token**.
- Access tokens represent access authorization issued to the client.

### Key Features:
- Tokens are issued by an **Authorization Server** with the approval of the resource owner.
- Clients use the token to access protected resources hosted by the resource server.
- OAuth 2.0 simplifies the process compared to OAuth 1.0 and 1.0a by removing the need to sign every call with a keyed hash.

### Components:
1. **Access Token**:
   - A string that represents access authorization.
2. **Refresh Token**:
   - If an access token expires, a refresh token can be used to retrieve a new one.

### Advantages:
- Combines **Authentication** and **Authorization**.
- Allows precise control over token scope and validity.
- Facilitates sophisticated security measures in the authorization process.

---

### Summary:
- Basic Authentication is simple but insecure.
- Bearer Authentication relies on tokens but requires HTTPS for secure communication.
- OAuth 2.0 introduces a more advanced framework, combining authentication and authorization for improved security and flexibility.
