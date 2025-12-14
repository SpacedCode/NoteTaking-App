# Google Classroom Integration

### User's Perspective
1. User clicks on google sign in button
2. Google account selection window appeared in front of the user
3. User choose which google account used for login
4. The screen shows a loading screen instead of login page
5. The screen will goes to the dashboard page (or other?) which shows the login is successful

### What Happened In the Back of the Stage
1. User clicks on google sign in button
      - **[Client]** Redirects user's browser URL to **Google Account Selection Screen**. It also **includes _Client ID_ and scope for Google Classroom consents** as the URL parameters. The Client ID is used by google to know what app this actually is and the scope used to know what user's google data do we want to have

2. Google account selection window appeared
      - **[Google]** Google retrieve accounts that have already logged in to the user device

3. User choose which google account they want to use in order to login to the system
      - **[Google]** When user choose the account, google will creates and sends an **_ID Token_** as the result to the client-side application

4. The screen shows a loading screen instead of login page
      - **[Client]** **The client side will get that _ID Token_** from Google.
      - **[Client]** Client will **sends a login request** to the backend server **including _ID Token_**
      - **[Server]** Server gets the _ID Token_ and **verifies it using _Secret Token_ and the same _Client ID_** to the Google API
      - **[Server]** Server then **gets the _access token_ from Google API**, and save it to the database. That access token is used for getting user data and their classroom data
      - **[Server]** Server then **creates a session token** for the user and store it to the database.

5. The screen will goes to the dashboard page (or other?) which shows the login is successful
      - **[Client]** When the client goes to the dashboard, it will **do verification by sending API request to the server including that session token** that the server gave earlier.
      - **[Server]** Server **verifies the token** and sends OK http status to the user if the token they gave is valid.

### Dictionary
- **ID Token**: A token that created by Google within google authentication process. It includes data that related to the user like username, email, and even their avatar image
- **Secret Token**: A token that created by Google within the first time setting up Google API. It used by the backend server of our application to makes Google believe our server is the legitimate server
- **Client ID**: Used for verifying our application. and used by Google to make sure that our application frontend and backend are the same application.
- **Access Token**: Access token that coming from Google after server verifies the ID Token is used for getting every data that user gives consent for the app to use earlier when choosing Google Account.

### Links
- npm library for connecting to google via ReactJS: https://www.npmjs.com/package/@react-oauth/google
- useful youtube video link for tutorial: https://www.youtube.com/watch?v=GuHN_ZqHExs