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
    * [MySQL Database and Sequelize](#MySQL-Database-and-Sequelize)
    * [Path NPM](#Path-NPM)
    * [Passport Authentication](#Passport-Authentication)
    * [Password Hashing](#Password-Hashing)
    * [Public Interaction](#Public-Interation)
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

# Explanation of Code


## MySQL Database and Sequelize

Our code is making use of the MySQL Database Service in order to maintain our database on the server side and interact with the database on the client side using requests and responses. We have implimented this interaction using the Sequelize ORM (Object-relational Mapping). Sequelize is a promise based ORM meaning that is makes use of the NodeJS promise library.

Using Sequelize we are able to connect to the database stored on the server and allow the client side application to interact with that database. We can pull data from the server side database to be used client side as well as send and post data from the client to the server and allow this data to be stored and used later. 

For our purposes in this application we are implimenting Sequelize in the server.js file as well as the index.js and user.js files within the "models" folder. Server.js is requiring in the index.js and user.js files making use of these two models but keeping the server.js file clean and readable. These two models are saved to the "db" variable and then used by Sequelize to sync the database to the client side application using the app.listen() method and taking in the PORT parameter then using a function to return a message to the user that the server is listening for requests on the port. The port we are listening on here is 8080 and process.env is a global variable injected by Node which allows these two environments to talk to eachother. 

The database is also being utilized through the api-routes.js and the html-routes.js within the "routes" folder. 

## Path NPM

The code makes use of the Path NPM. Path is a node package manager that allows us to use relative paths to associated files rather than using absolute paths. This simply allows us to reference files relative to the file they are being used in rather than needing to state the path to the file as it relates to the root of the file path. Path has been required into the html-routes.js file in the "routes" folder as well as the index.js file in the "models" folder. 

## Passport Authentication

The provided code uses an npm package called "Passport" which handles all the verification requests. Passport is an API middleware developed for use with Node.js and is Express-compatible which is also being used with our code. Using the Passport API lets us take the very complicated process of user authentication and easily integrate it into the final application. For our purposes here Passport has been set up as a "Local Strategy" which simply handles username and password credentials. Passport offers additional authentication methods with their other strategies however the local strategy is sufficient for our purposes. 

Passport is being utilized in the passport.js file. Upon sending a login request to the passport modules checks two conditons sequentially in an if/else if statement. First it checks to see if there is a matching username stored in the database. If it does not find a matching username a message will cue an "Incorrect email" message. If the user is found the else if statement condition will be checked to make sure the user entered password matches the password stored in the database. Passport does this by using the .validPassword method defined by Passport. If the password does not match the password stored in the database the .validPassword method will return the value "false" and cue an "Incorrect Password" message. If neither of these two conditions are met the username matches a user in the database and the password given is associated with that username so the code is allowed to proceded to the next step. In this implimentation of code Passport is checking for falsiness in the username and password provided. Passport uses the .serializeUser and .deserializeUser methods in order to send data back and forth over HTTP connections. These two methods convert the objects being sent to a stream of bytes and then converts it back to something readable by the application once it is received.

## Password Hashing

With every passing year, cyber criminals are looking for new ways to infiltrate application code in order to source the data being sent back and forth over the numerous calls and responses being utelized by online application. The security of these applications is extremely important and help solidify the trust that users have in these applicaitons while using them. Because of this it is important to use a data encryption method on any sensative information that may be being sent over the internet. For our code that has been provided the application is using the "bcrypt.js" npm to handle the hashing of the passwords being sent to and from the user and the server holding the database of information. 

Bcrypt is being implimented in the user.js file. Bcrypt is doing most of this behind the scenes to keep the methods secure which further enhances the security of the application. What we can see from its use in this application is that bcrypt is taking the user provided password, making sure the provided password can be hashed and compared to the hashed password stored on the database, and then hashing the incoming user provided password BEFORE it is sent to the database. Because of the way bcrypt impliments its hashing method, the password is only hashed and unhashed on the client side. This ensures that only properly hashed (secure) password data is being sent over the web.

## Public Interation

In order for the public to interact with this code, they are first taken to the Sign Up Page. Here the user can enter in an email address as well as a password. Upon clicking the "SIGN UP" button the user has now created an account with the application. If the user has already created an account with the application, there is a button at the bottom of the Sign Up page which will take them to a Login Page instead. The Login Page opperates almost identically to the Sign Up with the only difference being that the user must have already signed up for an account with the application. Upon completing either the Sign Up form or the Login Form, the user is taken to the members page. This page welcomes the user by name and will become the home page for the user while implemented by the application.


## Usage 

This starter code can be implemented by a number of other applications or websites. Users can access these pages to sign up for and login to a webpage or application. The code provides a great way to authenticate the user using a password saved to a server associated with the given user.

## Credits

This assignment was done under Trilogy Education Services through the Northwestern University Coding Bootcamp. The starter code for this assignment was provided by Trilogy Education Services. 

---