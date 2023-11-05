# Immutable Passport Integration Guide

<h2>Introduction</h2>
<p>In this guide, we'll walk you through the process of integrating Immutable Passport into your application for authentication and transaction initiation. Immutable Passport is designed for gaming purposes and offers a secure way to authenticate users and initiate blockchain transactions.</p>

<h2>Prerequisites</h2>
<p>Before getting started, ensure you have the following:</p>

<ul>
  <li>Node.js and npm installed on your machine.</li>
  <li>A code editor of your choice.</li>
  <li>A GitHub account for hosting your sample application and guide.</li>
  <li>A Passport account.</li>
</ul>

<h2>Step 1: Set Up Your Application</h2>
<h4>Create a new directory for your project or git clone a repository of a simple application that you'd like to use for showcasing Immutable Passport integration.</h4>
<p>Navigate to a directory where you want to create your application and create a new directory called passport-app.</p>

```shell
cd ~
mkdir passport-app
```

<p>Navigate to the passport-app directory and initialize a new Node.js project.</p>

```shell
cd passport-app
npm init -y
```

<p>Install the Immutable Passport SDK.</p>

```shell
npm install @immutablex/passport
```

<h2>Step 2: Register Your Application</h2>
<h4>Register the application on Immutable Developer Hub</h4>
<ol>
  <li>Go to the <a href="https://hub.immutable.com/">Immutable Developer Hub</a> and log in with your Passport account.</li>
  <li>Click the Create New Application button.</li>
  <li>Enter a name for your application and select the Passport authentication type.</li>
  <li>Click the Create Application button.</li>
  <li>Copy the Client ID and Client Secret for your application.</li>
</ol>

<h2>Step 3: Install and Initialize the Passport Client</h2>
<p>Create a new file called index.js in the passport-app directory and add the following code:</p>

```js
const passport = require('@immutablex/passport');

const app = passport({
  clientId: 'YOUR_CLIENT_ID',
  clientSecret: 'YOUR_CLIENT_SECRET',
});

// Export the app for use in other files
module.exports = app;
```

<h2>Step 4: Logging in a User with Passport</h2>
<p>To log in a user with Passport, you can use the following code:</p>

```js
const passport = require('./index');

const login = async () => {
  // Get the login URL from Passport
  const loginUrl = await passport.getLoginUrl();

  // Open the login URL in a browser
  window.open(loginUrl);
};

// Handle the login callback
const handleLoginCallback = async (code) => {
  // Exchange the code for an access token
  const accessToken = await passport.getAccessToken(code);

  // Use the access token to get the user's profile
  const profile = await passport.getProfile();

  // Display the user's profile on the page
  document.querySelector('#user-profile').innerHTML = `
    <h1>${profile.nickname}</h1>
  `;
};
```

<h3>Displaying on the app the id token, access token obtained from authenticating with Passport after login, and the user's nickname.</h3>
<p>To display the ID token, access token, and user's nickname on the app, you can use the following code:</p>

```js
const passport = require('./index');

const displayLoginInfo = () => {
  // Get the ID token and access token
  const idToken = passport.getIdToken();
  const accessToken = passport.getAccessToken();

  // Get the user's profile
  const profile = passport.getProfile();

  // Display the ID token, access token, and user's nickname on the page
  document.querySelector('#id-token').innerHTML = `
    <p>ID Token: ${idToken}</p>
  `;
  document.querySelector('#access-token').innerHTML = `
    <p>Access Token: ${accessToken}</p>
  `;
  document.querySelector('#nickname').innerHTML = `
    <p>Nickname: ${profile.nickname}</p>
  `;
};
```

<h2>Step 5: Logging Out a User</h2>
<p>To log out a user, you can use the following code:</p>

```js
const passport = require('./index');

const logout = async () => {
  // Log out the user
  await passport.logout();

  // Redirect the user to the login page
  window.location.href = '/login';
};
```

<h2>Step 6: Initiate a Transaction from Passport</h2>
<h4>Implement a feature in your application that initiates a transaction using Immutable Passport. For example, sending a placeholder string and obtaining the transaction hash.</h4>
<p>To initiate a transaction from Passport, you can use the following code:</p>

```js
const passport = require('./index');

const sendTransaction = async () => {
  // Create a new transaction object
  const transaction = {
    to: 'YOUR_RECIPIENT_ADDRESS',
    value: '1000000000000000000',
    data: 'Hello, world!',
  };

  // Send the transaction using Passport
  const transactionHash = await passport.sendTransaction(transaction);

  // Display the transaction hash on the page
  document.querySelector('#transaction-hash').innerHTML = `
    <p>Transaction Hash: ${transactionHash}</p>
  `;
```

<h2>Conclusion</h2>
<p>You have successfully integrated Immutable Passport into your application, allowing users to authenticate, initiate transactions, and securely interact with the Immutable blockchain designed for gaming. For more information and detailed options, refer to the <a href= "https://docs.immutable.com/docs/zkevm/products/passport/">Immutable Passport documentation</a>.</p>

<h2>Sample Application</h2>
<p>For a working sample application demonstrating Immutable Passport integration, please refer to the <a href="https://github.com/AgosVenezia/StackUp/tree/main/zkevm_nft">GitHub repository</a> containing the guide and relevant source files.</p>
