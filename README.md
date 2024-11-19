# Mood for Spotify
PES1UG23AM064, PES1UG23AM075 , PES1UG23AM061

**Mood for Spotify** is a single-page application built using **React** and **Styled-Components**. It allows users to visualize personalized Spotify data and create new playlists based on their mood and genre preferences.

## Setup

1. [Register a Spotify App](https://developer.spotify.com/dashboard/applications) and add `http://localhost:8888/callback` as a Redirect URI in the app settings.
2. Create an `.env` file in the root of the project. (This file is already created, but ensure to add your Spotify `client_id`, `client_secret`, `uri`, and `port` accordingly.)
3. Install dependencies in both `client` and `server` directories using `npm install`.
4. From the `client` directory, run: `npm start`.
5. From the `server` directory, run: `npm run server`.
6. Visit `http://localhost:3000/` to start using the application.

## Dependencies

- **axios**: For making HTTP requests to the Spotify API.
- **cors**: Middleware for handling Cross-Origin Resource Sharing on the server.
- **dotenv**: For managing environment variables.
- **express**: A Node.js framework used to create the backend server and handle API routes.
- **concurrently**: For running the client and server scripts simultaneously during development.
- **nodemon**: To automatically restart the server on changes.
- **styled-components**: For component-level CSS in JavaScript.
- **react-slider**: For implementing sliders to control filters like energy and mood.
- **react-router-dom**: For handling routing between pages in the application.
- **react-bootstrap-icons**: For adding icons from Bootstrap's icon library.
- **react-chartjs-2** and **chart.js**: For creating data visualizations.
- **firebase**: For managing user authentication and data storage.
- **react-dom**: For rendering React components.
- **react-fontawesome**: For adding Font Awesome icons.
- **react-scripts**: For managing scripts and configurations in Create React App.

---

## Overall Workflow of the Project

The project flow consists of both client-side (frontend) and server-side (backend) processes. Below is a step-by-step breakdown of the workflow:

### 1. **User Authentication with Spotify**

   - The user starts by logging into their Spotify account. When they log in, the app requests permissions to access their Spotify data.
   - Spotify redirects the user to the app with an **authorization token** in the callback URL (`http://localhost:8888/callback`).
   - The server uses this token to retrieve an **access token** and **refresh token** for future API calls.

### 2. **Backend - Express Server Setup**

   - The Express server handles routes for Spotify API interactions, including fetching user data, playlists, and track information.
   - The server makes API requests to Spotify on behalf of the user, using the access token provided during authentication.
   - To keep the access token valid, the server periodically refreshes it using the refresh token.

### 3. **Data Retrieval with Axios**

   - Once the user is authenticated, the frontend (client) uses **axios** to make requests to the backend server for Spotify data.
   - The backend server fetches data such as **recently played tracks**, **user’s top tracks**, **audio features** (like danceability, energy, mood), and **playlist information** from Spotify.
   - Axios is also used for sending user-created playlist details back to the server, which then communicates with the Spotify API to create and manage playlists.

### 4. **Data Processing**

   - The backend server processes the data received from Spotify and formats it as needed.
   - For example, the track duration is converted from milliseconds to minutes and seconds using helper functions.
   - Additional data formatting functions are used, like converting pitch classes (musical notes) or extracting the year from a date string.

### 5. **Mood and Genre Selection**

   - The main page features a **mood selector** slider (centered square with moods like Energetic, Sad, Happy, Calm), which allows users to select their current mood.
   - Users can also choose up to 5 music genres using clickable buttons.
   - These selections are used as **filters** when requesting track recommendations or playlist suggestions.

### 6. **Frontend - Data Visualization**

   - The frontend uses **React** components to display personalized Spotify data, including:
     - Charts (created with **react-chartjs-2** and **chart.js**) to show audio features and track attributes.
     - Visual elements styled with **styled-components** for a modern look.
   - Data such as track names, album covers, artists, and playlist details are dynamically displayed.
   - **Mood filtering** and **genre selection** allow users to interact with the data and view tracks that match their preferences.

### 7. **Playlist Creation**

   - Based on the selected mood and genres, users can create custom playlists.
   - The frontend sends the playlist details to the backend server using axios, which then makes a POST request to the Spotify API to create the playlist on the user's account.
   - Once created, the new playlist is displayed in the app, and users can access it directly from their Spotify account.

### 8. **Error Handling and Logging**

   - A higher-order function called `CatchErrors` wraps API calls to handle potential errors gracefully, logging them to the console without disrupting the user experience.

### 9. **Saving User Data with Firebase**

   - **Firebase** is used to manage user authentication data and save user preferences or favorites if implemented.
   - Firebase could also be used to track user activity or save custom playlist details for future sessions.

### 10. **User Interface and Animated Effects**

   - The word "MOOD" has a **glowing, color-changing effect** created with CSS animations.
   - The interactive mood selector and genre buttons offer a responsive and dynamic experience, encouraging users to explore their mood-based playlists.

---
