# E-commerce API Testing using Postman

A beginner-level REST API testing project using the [DummyJSON API](https://dummyjson.com). This project demonstrates API authentication, Bearer token handling, environment variables, dynamic data extraction, and response validation using Postman.

## Project Overview

The purpose of this project is to practise testing REST API endpoints and understand how requests, responses, authentication tokens, and Postman test scripts work together.

**API under test:** DummyJSON  
**Tool:** Postman  
**Scripting:** JavaScript (Postman test scripts)  
**Response format:** JSON  
**Version control:** GitHub

## Scope of Testing

The collection contains four requests:

| Request | Method | Endpoint | Purpose |
|---|---|---|---|
| Login API | POST | `/auth/login` | Authenticate with a demo account and receive access and refresh tokens |
| Get User Profile | GET | `/auth/me` | Request the authenticated user's profile using a Bearer access token |
| Get Products | GET | `/products` | Retrieve the product list and save the first product's ID |
| Get Single Product | GET | `/products/{{product_id}}` | Retrieve one product using the ID saved by the previous request |

The base URL is configured through the `base_url` environment variable: `https://dummyjson.com`.

## Authentication and Request Flow

The collection follows this sequence:

1. **Login:** Send a POST request to `/auth/login` with the DummyJSON demo login details in the request body.
2. **Validate the login response:** The test script checks for HTTP 200, verifies that access and refresh tokens are present and non-empty, checks their three-part JWT structure, and checks selected access-token payload fields and expiry.
3. **Save tokens:** The script stores `accessToken` and `refreshToken` in the selected Postman environment.
4. **Send an authenticated request:** The Get User Profile request uses `{{accessToken}}` as its Bearer token.
5. **Fetch products:** The Get Products request saves the first product's ID as `product_id`.
6. **Reuse dynamic data:** Get Single Product uses `{{product_id}}` in its URL and checks that the returned product ID matches the requested ID.

**Note:** The collection stores a refresh token, but it does not currently contain a refresh-token request or an automated token-refresh flow. The JWT checks inspect token structure and selected payload fields; they do not cryptographically verify the token signature.

## Test Scripts and Validations

Postman JavaScript test scripts are used to validate responses and share data between requests.

- **Login API:** Checks status code, access/refresh token presence, JWT structure, selected access-token payload fields (`id`, `username`, `exp`), and that the access token has not expired. Saves both tokens as environment variables.
- **Get User Profile:** Checks that the response status is HTTP 200.
- **Get Products:** Checks HTTP 200 and saves the first product ID to `product_id`.
- **Get Single Product:** Checks HTTP 200 and verifies that the returned product ID matches the saved ID.

## Tools and Concepts Practised

- Postman collections and environment variables
- REST API requests using POST and GET
- JSON request and response bodies
- Authentication using Bearer tokens
- Access-token and refresh-token extraction and storage
- JavaScript test scripts and response assertions
- Dynamic data extraction and reuse across requests
- HTTP status-code validation

## How to Run the Collection

1. Clone or download this repository.
2. Open Postman and import `Ecommerce API Project.postman_collection.json`.
3. Create and select a Postman environment.
4. Add an environment variable named `base_url` with the value `https://dummyjson.com`.
5. Open the Login API request and use valid demo credentials supported by DummyJSON. The collection currently includes sample demo credentials in its request body; these are not personal credentials.
6. Send **Login API** first so the test script can save the tokens.
7. Send **Get User Profile** to use the saved access token.
8. Send **Get Products** to save a product ID, then send **Get Single Product**.
9. Review the response and the **Test Results** tab for each request.

Run the requests in the order shown above so the required environment variables are available.

## Repository File

- [Ecommerce API Project.postman_collection.json](Ecommerce%20API%20Project.postman_collection.json) — importable Postman collection containing the four requests and their test scripts.

## API Reference

- [DummyJSON documentation](https://dummyjson.com/docs)

## Current Project Limitations

- The collection currently focuses on successful request flows; negative scenarios such as invalid credentials, missing/invalid tokens, and invalid product IDs are not included.
- The refresh token is captured and stored, but a refresh-token request is not implemented.
- The Get User Profile request currently validates the HTTP status code only.

These are possible future enhancements, not features claimed as completed.

## Author

**Prashant Kumar**  
[GitHub Profile](https://github.com/prashantkumar1122)
