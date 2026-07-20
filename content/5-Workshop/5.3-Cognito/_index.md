---
title: "Cognito Authentication"
date: 2024-01-01
weight: 3
pre: " <b> 5.3. </b> "
---

## Amazon Cognito Configuration Guide

Amazon Cognito is used in the SyncQuiz project to manage user registration, authentication, and secure access. It allows the system to create User Pools, configure App Clients, perform email-based verification, and issue secure tokens to the frontend upon successful login.

### Step 1: Access Amazon Cognito Service

Description:
Go to the AWS Management Console and search for the Amazon Cognito service. This service manages user identities and controls access to the application.

Image:
![Access Amazon Cognito](/images/5.3-Cognito/cog1.jpg)

### Step 2: Select Add login and signup experiences to your app

Description:
On the Amazon Cognito homepage, select the option Add login and signup experiences to your app. This option is used to set up the authentication flow for web applications.

Image:
![Select Add login and signup experiences](/images/5.3-Cognito/cog2.jpg)

### Step 3: Choose Single-page application type

Description:
Under Define your application, select Single-page application (SPA) because the SyncQuiz frontend is built with React. This application type is suitable for frontend websites running on client browsers.

Image:
![Choose Single-page application](/images/5.3-Cognito/cog3.jpg)

### Step 4: Name your application client

Description:
Enter the name of your application client in the Name your application field. In this example, the app client name is set to webquiz-dev-web-client to serve the development environment of the WebQuiz/SyncQuiz system.

Image:
![Name your Cognito application](/images/5.3-Cognito/cog4.jpg)

### Step 5: Select email-based sign-in

Description:
Under Options for login credentials, select E-mail. With this setting, users can register and log in using their email addresses.

Image:
![Select email sign-in](/images/5.3-Cognito/cog5.jpg)

### Step 6: Enter application Return URL

Description:
Under Add a return URL, enter the callback URL of the frontend. This is the URL that Cognito will redirect users to after successful authentication.

Example for local environment:
http://localhost:3000/callback

For production, replace this with your actual CloudFront domain or deployed website URL.

Image:
![Enter Return URL](/images/5.3-Cognito/cog6.jpg)

### Step 7: Create User Directory

Description:
After completing the necessary details, click Create a user directory to allow Cognito to set up the User Pool and App Client.

Image:
![Create User Directory](/images/5.3-Cognito/cog7.jpg)

### Step 8: Verify the User Pool is created

Description:
Once created, go back to the User groups list to verify your newly created User Pool. This User Pool will manage all user accounts within the system.

Image:
![Verify User Pool](/images/5.3-Cognito/cog8.jpg)

### Step 9: Access Authentication Methods

Description:
Within your User Pool details, navigate to the Authentication tab and select Authentication methods. Here, you can review and configure authentication mechanisms such as email, SMS, and signing policies.

Image:
![Authentication Methods](/images/5.3-Cognito/cog9.jpg)

### Step 10: Configure Password Policy

Description:
Select the password policy to modify settings. In this example, the password requires a minimum length of 8 characters, along with numbers, lowercase letters, uppercase letters, and special characters.

Image:
![Configure Password Policy](/images/5.3-Cognito/cog10.jpg)

### Step 11: Review Registration Settings

Description:
Switch to the Register tab to check the configuration for user account verification. This section defines how Cognito verifies email addresses or phone numbers when users sign up.

Image:
![Review Registration Settings](/images/5.3-Cognito/cog11.jpg)

### Step 12: Modify Account Verification settings

Description:
Click To modify to update the registration verification settings. This step ensures that users must verify their email addresses before they can access their accounts.

Image:
![Modify Registration Settings](/images/5.3-Cognito/cog12.jpg)

### Step 13: Configure verification email sending

Description:
Under Attribute verification and user account confirmation, select the option to allow Cognito to automatically send verification messages. Then select Send an email, verify the email address to trigger a confirmation email to new users.

Image:
![Configure email verification](/images/5.3-Cognito/cog13.jpg)

### Step 14: Save verification changes

Description:
After selecting email verification, click Save changes. From now on, any registering user will be required to confirm their email address.

Image:
![Save email verification settings](/images/5.3-Cognito/cog14.jpg)

### Step 15: Verify Application Client

Description:
Navigate to the Applications tab and select Application clients to check the generated app client. This app client provides the Client ID used by the React frontend to integrate authentication with Cognito.

Image:
![Verify Application Client](/images/5.3-Cognito/cog15.jpg)

### Step 16: Complete Cognito Configuration

Description:
With the User Pool, App Client, email login, return URL, password policy, and email verification successfully configured, Amazon Cognito is now ready for frontend integration.

Image:
![Complete Cognito Configuration](/images/5.3-Cognito/cog16.jpg)

## Expected Outcomes

After completing the steps:
- The User Pool has been successfully created.
- The SPA configuration is set up for the React frontend.
- Users can sign up and sign in using their email.
- The Return URL is configured to handle redirects post-login.
- A strong Password Policy is enforced for enhanced security.
- Email verification is enabled to authenticate user credentials.
- The App Client is ready to be integrated into the SyncQuiz frontend.

## Role of Cognito in the SyncQuiz Project

In the SyncQuiz project, Amazon Cognito serves as the main authentication and identity service. When users sign up or log in, Cognito handles account credentials, verifies email authenticity, and issues JSON Web Tokens (JWT). The React frontend uses these tokens to secure API Gateway endpoints, ensuring only authorized hosts can create quizzes, open game rooms, and manage quiz contents.
