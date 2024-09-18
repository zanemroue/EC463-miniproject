# 2024 Fall Miniproject

# Reaction Time Game on Raspberry Pi Pico W

## Table of Contents

- [Project Overview](#project-overview)
- [Technologies Used](#technologies-used)
- [Why We Chose These Technologies](#why-we-chose-these-technologies)
- [How the Components Work Together](#how-the-components-work-together)
- [Video Demo](#video-demo)


## Project Overview

- **Device**: Raspberry Pi Pico W with an LED and a button.
- **Game Objective**: Press the button as quickly as possible when the LED flashes.
- **Data Handling**: The device measures reaction times and uploads them to the cloud via an API endpoint.
- **Web Interface**: A React website where users can sign up, log in, and view their scores.

## Technologies Used

- **MicroPython**: Programming language for the Raspberry Pi Pico W.
- **Node.js**:
  - Runtime environment for executing JavaScript code on the server side.
- **Express.js**:
  - Web framework for building the API endpoint.
- **Firebase**:
  - **Authentication**: User sign-up and login functionality.
  - **Firestore Database**: Storing user scores and reaction times.
  - **Cloud Functions**: Hosting the Node.js API endpoint.
- **React.js**: Front-end framework for building the website.
- **HTTPS Communication**: Secure data transmission between the device and the cloud.

## Why We Chose These Technologies

### Node.js and Express.js for the API Endpoint

- **JavaScript Everywhere**: Using Node.js allows for JavaScript to be used both on the frontend and backend, streamlining development.
- **Asynchronous Handling**: Node.js excels at handling asynchronous operations, which is ideal for I/O-bound tasks like network requests.
- **Express.js**:
  - **Middleware Support**: Simplifies request handling, validation, and parsing JSON payloads.
  - **Routing**: Easy to define API endpoints and manage HTTP methods.
- **Integration with Firebase**: Node.js works seamlessly with Firebase Cloud Functions, allowing for easy deployment of serverless functions.

### Firebase

- **Authentication**: Simplifies user management with secure authentication methods.
- **Firestore Database**: Provides a scalable and flexible NoSQL database.
- **Cloud Functions**: Serverless environment to run backend code without managing servers, compatible with Node.js.
- **Integration**: Smooth integration with both the frontend and backend technologies.

### React.js

- **Component-Based Architecture**: Facilitates building reusable UI components.
- **Performance**: Efficient rendering and state management.
- **Developer Tools**: Rich ecosystem and tooling for development and debugging.

### HTTPS Communication

- **Security**: Encrypts data during transmission to protect user information.
- **Compliance**: Meets standard security protocols for web communications.

## How the Components Work Together

### Raspberry Pi Pico W (Device)

- **Game Logic**:
  - Initializes the LED and button.
  - Waits for random intervals before flashing the LED.
  - Measures the time between the LED flash and button press.
  - Repeats this for a set number of times (e.g., 10 flashes).
- **Data Processing**:
  - Calculates statistics like minimum, maximum, and average reaction times.
  - Counts the number of missed attempts.
- **Network Communication**:
  - Connects to Wi-Fi using credentials from a `config.json` file.
  - Prepares data in JSON format for transmission.
  - Sends data to the API endpoint using an HTTPS POST request.

### Node.js API Endpoint (Backend)

- **Hosted on Firebase Cloud Functions**:
  - Utilizes Node.js runtime environment provided by Firebase.
- **API Endpoint (`/upload_data`)**:
  - Uses Express.js to define routes and handle HTTP requests.
  - Validates the device API key from the request headers.
  - Parses the incoming JSON data.
  - Stores the data in the Firestore database under the respective user ID.
- **Security**:
  - Uses HTTPS and API key validation to secure the endpoint.
  - Ensures only authorized devices can upload data.

### Firestore Database

- **Data Storage**:
  - Organizes data in collections and documents.
  - Stores user information and their reaction time records.
- **Data Structure**:
  - Each user has a collection of `response_times`.
  - Each record includes statistics and timestamps.

### React.js Website (Frontend)

- **User Interface**:
  - Provides sign-up and login forms using Firebase Authentication.
  - Displays user-specific data retrieved from Firestore.
- **Authentication**:
  - Manages user sessions and state.
  - Protects routes and components that require authentication.
- **Data Visualization**:
  - Fetches reaction time data from Firestore.
  - Displays statistics and history to the user.
- **Navigation**:
  - Uses React Router (if implemented) for smooth transitions between pages.
  - Includes a navigation bar (`NavBar` component) that changes based on user authentication state.

### Integration Flow

1. **User Interaction**:
   - The user plays the game on the Raspberry Pi Pico W.
   - Reaction times are measured and collected.
2. **Data Transmission**:
   - The device uploads the data to the cloud via the Node.js API endpoint.
3. **Backend Processing**:
   - Firebase Cloud Functions, running Node.js and Express.js, receive the data.
   - Data is validated and stored in Firestore under the user's account.
4. **Frontend Display**:
   - The user logs into the React website.
   - The website fetches the latest data from Firestore.
   - The user views their performance metrics.

---

By choosing Node.js and Express.js for the API endpoint, the project leverages a familiar JavaScript environment that integrates well with Firebase Cloud Functions. This choice simplifies development and deployment, allowing for efficient handling of HTTP requests and easy scaling. Combined with the other technologies, this setup provides a seamless and secure user experience from hardware interaction to cloud data management and user interface.


## Video Demo
  https://youtu.be/j6uMxeUJoNE
