# Sequelize - Reverse Engineering Code

## Description 

The purpose of this assignment is to reverse engineer the starter code provided and provide a tutorial

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
    * [Express NPM](#Express-NPM)
    * [Passport Authentication](#Passport-Authentication)
    * [Password Hashing](#Password-Hashing)
    * [JavaScript Libraries](#JavaScript-Libraries)
    * [Public Files](#Public-Files)
    * [Public Interaction](#Public-Interation)
    * [Usage](#usage)
* [Credits](#credits)

<br>

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

<br>

# Explanation of Code

## MySQL Database and Sequelize

The code provided code is making use of the MySQL Database Service in order to maintain our database on the server side and interact with the database on the client side using requests and responses. We have implemented this interaction using the Sequelize ORM (Object-relational Mapping). Sequelize is a promise based ORM meaning that it makes use of the NodeJS promise library.

Using Sequelize we are able to connect to the database stored on the server and allow the client side application to interact with that database. We can pull data from the server side database to be used client side as well as send and post data from the client to the server and allow this data to be stored and used later. 

For our purposes in this application we are implementing Sequelize in the server.js file as well as the index.js and user.js files within the "models" folder. Server.js is requiring in the index.js and user.js files making use of these two models but keeping the server.js file clean and readable. These two models are saved to the "db" variable and then used by Sequelize to sync the database to the client side application using the app.listen() method and taking in the PORT parameter then using a function to return a message to the user that the server is listening for requests on the port. The port we are listening on here is 8080 and process.env is a global variable injected by Node which allows these two environments to talk to each other. The database is also being utilized through the api-routes.js and the html-routes.js within the "routes" folder. The api-routes.js and html-routes.js closely send data back and forth with each other. These two files are the main communication methods between the client and the server holding our database. 

Api-routes.js file holds the module that handles all the requests coming from client side and responds from the server. Api-routes.js is using passport authentication (see [Passport Authentication](#Passport-Authentication) section below for details) to handle authorization requests. Api-routes.js also holds our application methods that interact with the database on the server side. The code uses both POST route methods as well as GET route methods in order to interact with the database. Api-routes.js is simply storing these route methods into a module which is being exported to be called using "app.use()" with given parameters through the Express NPM framework (see [Express NPM](#Express-NPM) section below for details) in the server.js file. The main methods of the api-routes module include verifying authentication of users via passport middleware as well as handling the requests from the user and appropriately sending the appropriate data back fropm the server to the client which will allow the user to navigate through the website using html-routes.js. The first POST route validates the login credentials and returns the stored username. The second POST route is used through the "signup" page. It takes in the user entered username (email) and password and creates a database entry for the new user. Upon completing the database entry, if successful it sends information back to the client redirecting them to the login page with the .then() method on line 21. If there is an error with the creating the database entry it will be caught with the .catch() method on line 24. The first GET route simply handles the request from the client upon clicking the "logout" button. This will take that request and use the logout() method clearing out current user information from the database and responding with the redirect("/") method to be used by the html-routes.js file. The second GET route is used to get the user data stored in the server and send it to the client to be used. Within this route there is an if/else statement that first checks to make sure the user is "logged in" and if they are not, it will return an empty object. If the user is logged it, the server will respond with a JSON object containing the username (email) and the user id number which is automatically generated by the MySQL database. 

The html-routes.js file holds the module containing the methods to handle requests being sent by the client and responses being sent from the server. Similarly to the api-routes.js file, html-routes.js is simply storing these route methods into a module which is being exported to be called using "app.use()" with given parameters through the Express NPM framework (see [Express NPM](#Express-NPM) section below for details) in the server.js file.Html-routes.js starts by checking if the user is logged in. The code has implemented a custom middleware for authentication. This middleware is being required on line 5. The module holds three GET requests which interact with the server through the api-routes.js file. The first GET route method (line 9) will be called upon the client visiting the "/" path. This route method uses an if statment to check whether the user has an account stored in the server database and will then redirect the user using the "/members" request otherwise it will send back the data to display the "signup.html" page stored in the "public" folder. The second GET route method (line 17) handles requests being sent by the client when visiting the "/login" path. Just like the first route method, this route method uses an if statment to check whether the user has an account stored in the server database and will then redirect the user using the "/members" request otherwise it will send back the data to display the "login.html" page stored in the "public" folder. The final GET route method (line 27) will be called upon the client visiting the "/members" path. As stated above this route will initiate as long as the user already has an account saved in the database server side. This route also takes in "isAuthenticated" as a parameter (see [Passport Authentication](#Passport-Authentication) section below for details) to authenticate the user. The route will then pull the data from the response and display the "members.html" page stored in the "public" folder.

## Path NPM

The code makes use of the Path NPM. Path is a node package manager that allows us to use relative paths to associated files rather than using absolute paths. This simply allows us to reference files relative to the file they are being used in rather than needing to state the path to the file as it relates to the root of the file path. Path has been required into the html-routes.js file in the "routes" folder as well as the index.js file in the "models" folder. 

## Express NPM

Express NPM is a Node.js web application framework. This framework is used to help develop Node based web applications. The Express framework allows us to set up middlewares that will respond to HTTP requests. Express also allows us to define our routing modules in both the api-routes.js file as well as the html-routes.js file and then using those requests we can dynamically render HTML pages client side to be used in the application. Express is mainly implemented in the server.js file however it references all of the route modules. Express is the framework that allows are client side to communicate with the server side database.

## Passport Authentication

The provided code uses an npm package called "Passport" which handles the verification requests. Passport is an API middleware developed for use with Node.js and is Express-compatible which is also being used with our code. Using the Passport API lets us take the very complicated process of user authentication and easily integrate it into the final application. For our purposes here Passport has been set up as a "Local Strategy" which simply handles username and password credentials. Passport offers additional authentication methods with their other strategies however the local strategy is sufficient for our purposes. 

Passport is being utilized in the passport.js file. Upon sending a login request to the passport modules checks two conditons sequentially in an if/else if statement. First it checks to see if there is a matching username stored in the database. If it does not find a matching username a message will cue an "Incorrect email" message. If the user is found the else if statement condition will be checked to make sure the user entered password matches the password stored in the database. Passport does this by using the .validPassword method defined by Passport. If the password does not match the password stored in the database the .validPassword method will return the value "false" and cue an "Incorrect Password" message. If neither of these two conditions are met the username matches a user in the database and the password given is associated with that username so the code is allowed to proceded to the next step. In this implementation of code Passport is checking for falsiness in the username and password provided. Passport uses the .serializeUser and .deserializeUser methods in order to send data back and forth over HTTP connections. These two methods convert the objects being sent to a stream of bytes and then converts it back to something readable by the application once it is received.

## Password Hashing

With every passing year, cyber criminals are looking for new ways to infiltrate application code in order to source the data being sent back and forth over the numerous calls and responses being utelized by online application. The security of these applications is extremely important and help solidify the trust that users have in these applicaitons while using them. Because of this it is important to use a data encryption method on any sensative information that may be being sent over the internet. For our code that has been provided the application is using the "bcrypt.js" npm to handle the hashing of the passwords being sent to and from the user and the server holding the database of information. 

Bcrypt is being implemented in the user.js file. Bcrypt is doing most of this behind the scenes to keep the methods secure which further enhances the security of the application. What we can see from its use in this application is that bcrypt is taking the user provided password, making sure the provided password can be hashed and compared to the hashed password stored on the database, and then hashing the incoming user provided password BEFORE it is sent to the database. Because of the way bcrypt implements its hashing method, the password is only hashed and unhashed on the client side. This ensures that only properly hashed (secure) password data is being sent over the web.

## JavaScript Libraries

For this application we have made use of both the Bootstrap and jQuery JavaScript Libraries. These libraries help simplify front end code and can streamline the functionality of the application.

jQuery is a JavaScript library that helps greatly in the functionality of the JavaScript code. Using jQuery we can more easily manipulate DOM element, handle events, and send Ajax calls to our server for use on client side pages. JQuery is being implemented in the application in all three of our JavaScript files discussed below (see [Public Files](#Public-Files) for reference). 

Bootstrap is a JavaScript Library and front-end framework that helps create effective layouts to be used in client side HTML files. Bootstrap helps streamline the process of creating and developing HTML that will enhance functionality and provide an easy framework for a successful UI/UX (User Interface/User eXperience). Bootstrap is utilized through predefined classes which are given to HTML elements. These classes modify these HTML elements in order to change the functionality of those elements. Much of Bootstrap also requires cooresponding JavaScript to be properly utilized.

## Public Files

In the code provided they have included a "public" folder which contains all the JavaScript files, HTML files, and stylesheet files which will be used client side by the application. The HTML files have been discussed earlier within the MySQL Database and Sequelize section [here](#MySQL-Database-and-Sequelize) and the Express NPM section [here](#Express-NPM). To reiterate on these HTML files our application is using Express to dynically render the HTML files for client side viewing based on the requests and responses made by our route modules within the api-routes.js and html-routes.js files. 

The public JavaScript files contain the JavaScript code which runs on the rendered HTML pages. These files make use of our JavasScript Libraries which were described about (see [JavaScript Libraries](#JavaScript-Libraries) for reference). The JavaScript files in the "public" folder also contain all of the Ajax calls being made to the server which can then be used by our front end code. 

The login.js file using jQuery to manipulate the DOM elements is taking in the user inputed data and running the loginUser() function using the email and password provided by the user as parameters. The loginUser() function runs an Ajax POST request call to the server to find the associated user data in the server. This POST call runs through the api-routes.js for authenticaion.

The members.js file is doing an Ajax GET request call to the server through the api-routes.js module and returning the data containing the username(email). This data is then simply displayed at the top of the page with some welcome text.

The signup.js file uses jQuery to manipulate the DOM input provided by the user in the same was that the login.js script but instead of running the loginUser() function, it invokes the signUpUser() function taking in the username(email) and password as parameters. The function does an Ajax call to the server through the api-routes.js module and if successful will navigate the user to the /members page. If the function is not successful the .catch() method will invoke the handleLoginErr() function and return an alert message with the "err.responseJSON" data as well as a "500" error message.

## Public Interaction

In order for the public to interact with this code, they are first taken to the Sign Up Page. Here the user can enter in an email address as well as a password. Upon clicking the "SIGN UP" button the user has now created an account with the application. If the user has already created an account with the application, there is a button at the bottom of the Sign Up page which will take them to a Login Page instead. The Login Page operates almost identically to the Sign Up with the only difference being that the user must have already signed up for an account with the application. Upon completing either the Sign Up form or the Login Form, the user is taken to the members page. This page welcomes the user by name and will become the home page for the user while implemented by the application.


## Usage 

This starter code can be implemented by a number of other applications or websites. Users can access these pages to sign up for and login to a webpage or application. The code provides a great way to authenticate the user using a password saved to a server associated with the given user.

## Credits

This assignment was done under Trilogy Education Services through the Northwestern University Coding Bootcamp. The starter code for this assignment was provided by Trilogy Education Services. 

---