# Sequelize - Reverse Engineering Code

## Description 

The purpose of this assignment is to reverse engineer the starter code provided and provide a tutorial


The webpage is hosted on [GitHub](https://rconat.github.io/ReverseEngineeringSequelizeCode/).

You can find the repo on [GitHub](https://github.com/Rconat/ReverseEngineeringSequelizeCode).

![Sign Up Layout](assets/SignUpPage.png)
![Login Layout](assets/LoginPage.png)
![Members Layout](assets/MembersPage.png)

---

## Table of Contents

* [List of Files](#List-of-Files)
* [Explanation of Code](#Explanation-of-Code)
* [Usage](#usage)
* [Credits](#credits)

## List of Files

<ul>
    <li>server.js</li>
    <li>package.json</li>
    <li>package-lock.json</li>
    <li>.gitignore</li>
    <li>README.md</li>
    <li>api-routes.js</li>
    <li>html-routes.js</li>
    <li>login.html</li>
    <li>members.html</li>
    <li>signup.html</li>
    <li>style.css</li>
    <li>login.js</li>
    <li>members.js</li>
    <li>signup.js</li>
    <li>index.js</li>
    <li>user.js</li>
    <li>passport.js</li>
    <li>config.json</li>
    <li>isAuthenticated.js</li>

</ul>

---

## Explanation of Code

Client Side Code



Passport Authentication

The provided code uses an npm package called "Passport" which handles all the verification requests. Passport is an API middleware developed for use with Node.js and is Express-compatible which is also being used with our code. Using the Passport API lets us take the very complicated process of user authentication and easily integrate it into the final application. For our purposes here Passport has been set up as a "Local Strategy" which simply handles username and password credentials. Passport offers additional authentication methods with their other strategies however the local strategy is sufficient for our purposes. Passport is utilized in the passport.js file. Upon sending a login request to the passport modules checks two conditons sequentially in an if/else if statement. First it checks to see if there is a matching username stored in the database. If it does not find a matching username a message will cue an "Incorrect email" message. If the user is found the else if statement condition will be checked to make sure the user entered password matches the password stored in the database. Passport does this by using the .validPassword method defined by Passport. If the password does not match the password stored in the database the .validPassword method will return the value "false" and cue an "Incorrect Password" message. If neither of these two conditions are met the username matches a user in the database and the password given is associated with that username so the code is allowed to proceded to the next step. In this implimentation of code Passport is checking for falsiness in the username and password provided. Passport uses the .serializeUser and .deserializeUser methods in order to send data back and forth over HTTP connections. These two methods convert the objects being sent to a stream of bytes and then converts it back to something readable by the application once it is received.

Public Interation

In order for the public to interact with this code, they are first taken to the Sign Up Page. Here the user can enter in an email address as well as a password. Upon clicking the "SIGN UP" button the user has now created an account with the application. If the user has already created an account with the application, there is a button at the bottom of the Sign Up page which will take them to a Login Page instead. The Login Page opperates almost identically to the Sign Up with the only difference being that the user must have already signed up for an account with the application. Upon completing either the Sign Up form or the Login Form, the user is taken to the members page. This page welcomes the user by name and will become the home page for the user while implemented by the application.


## Usage 

This starter code can be implemented by a number of other applications or websites. Users can access these pages to sign up for and login to a webpage or application. The code provides a great way to authenticate the user using a password saved to a server associated with the given user.

## Credits

This assignment was done under Trilogy Education Services through the Northwestern University Coding Bootcamp. The starter code for this assignment was provided by Trilogy Education Services. 

---