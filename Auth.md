# Authentication API Documentation

## Base URL
`/api/auth`

## Endpoints

### 1. Register
- **URL:** `/register`
- **Method:** POST
- **Description:** Register a new user
- **Request Body:**
  - `name`: string (required)
  - `email`: string (required)
  - `password`: string (required)
- **Response:**
  - Success (201): User registered successfully
  - Error (400): User already exists
  - Error (500): Internal server error

### 2. Verify Email
- **URL:** `/verify-email/:token`
- **Method:** GET
- **Description:** Verify user's email address
- **URL Parameters:**
  - `token`: string (required) - Verification token sent to user's email
- **Response:**
  - Success (200): Email verified successfully
  - Error (400): Invalid verification token
  - Error (500): Internal server error

### 3. Login
- **URL:** `/login`
- **Method:** POST
- **Description:** Authenticate user and receive a JWT token
- **Request Body:**
  - `email`: string (required)
  - `password`: string (required)
- **Response:**
  - Success (200): Login successful, returns JWT token
  - Error (400): Invalid credentials
  - Error (401): Email not verified
  - Error (500): Internal server error

### 4. Validate Token
- **URL:** `/validate`
- **Method:** GET
- **Description:** Validate JWT token and get user information
- **Headers:**
  - `Authorization`: Bearer {token}
- **Response:**
  - Success (200): Token is valid, returns user information
  - Error (401): Invalid or no token provided
  - Error (500): Internal server error

### 5. Change Password
- **URL:** `/change-password`
- **Method:** POST
- **Description:** Change user's password (requires authentication)
- **Headers:**
  - `Authorization`: Bearer {token}
- **Request Body:**
  - `currentPassword`: string (required)
  - `newPassword`: string (required)
- **Response:**
  - Success (200): Password changed successfully
  - Error (400): Current password is incorrect
  - Error (404): User not found
  - Error (500): Internal server error

### 6. Forgot Password
- **URL:** `/forgot-password`
- **Method:** POST
- **Description:** Request a password reset email
- **Request Body:**
  - `email`: string (required)
- **Response:**
  - Success (200): Password reset email sent
  - Error (400): User not found
  - Error (500): Internal server error

### 7. Reset Password
- **URL:** `/reset-password`
- **Method:** POST
- **Description:** Reset user's password using the token received in email
- **Request Body:**
  - `token`: string (required) - Reset token received in email
  - `newPassword`: string (required)
- **Response:**
  - Success (200): Password has been reset successfully
  - Error (400): Invalid or expired password reset token
  - Error (500): Internal server error

## Notes
- All successful responses include a message and relevant data.
- Error responses include an error message and appropriate HTTP status code.
- The `/change-password` endpoint requires authentication using a valid JWT token.
- Email verification is required before a user can log in.
- Password reset tokens expire after 1 hour.
