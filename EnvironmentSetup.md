# Environment Setup
Prepare your workstation for the development process.

## Installing Tools
Some key tools will be necessary in order to run the app and contribute to the project.

### Visual Studio Code
VS Code is a lightweight code editor with lots of powerful features. [Click here to download & install it.](https://code.visualstudio.com/Download)

### Node.js
Node.js is a JavaScript runtime that lets developers create web servers. The backend of the project runs on Node.js. [Click here to download the installer.](https://nodejs.org/en/download/prebuilt-installer) Note that **npm** (**n**ode **p**ackage **m**anager) should also be installed as part of the Node.js installation.

### Git
Git is a version control system. The HyTOP codebase is stored in a Git repository on GitHub. [Click here to download & install Git.](https://gitforwindows.org/) Note that **Git BASH**, a command line shell, should also be installed as part of the Git for Windows installation.

>**IMPORTANT NOTE:** You may have to run the installer as an administrator. Right click from the file explorer to see that option.

## Running the App
Once the above tools have been installed, it's time to run the app. The codebase lives in this GitHub repository: [https://github.com/hto-projects/hytop](https://github.com/hto-projects/hytop)

### Getting the Code
Follow these steps to properly grab the code for the project from GitHub:

1. [Go to the repository on the web](https://github.com/hto-projects/hytop)
1. Click the green **<> Code** button in the upper right
1. Copy the **HTTPS** URL
1. Open VS Code
1. Press `Ctrl`+`Shift`+`P` to open the Command Palette
1. Type **Git: Clone** and press `Enter`
1. Paste the HTTPS URL for the repository
1. Select a Repository Destination folder (e.g., the Desktop)
1. Once the repository has been cloned, click "Open" in the pop-up to open it

Now you have the codebase ready for development!

### Setting Up the Environment
Next, get ready to run the project with these steps:

1. Install the [Prettier VS Code extension](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)  
  - It should pop up as recommended
1. Open a terminal with `Ctrl`+`\``

In the terminal, run these commands by typing them and pressing `Enter`:

```bash
npm install
```
>Install the backend dependencies - this may take a while

<br>

```bash
cd frontend
```
>**C**hange to the frontend **D**irectory

<br>

```bash
npm install
```
>Install frontend dependencies - this may take a while

<br>

```bash
cd ..
```
>**C**hange back to the root **D**irectory

<br>

Now, the app should be ready to run!

### Running the App
There are a few ways to run the frontend and the backend, including scripts that run them concurrently:

- In the terminal, from the root directory, run the `npm run dev` command
- In the NPM SCRIPTS pane in VS Code (bottom left), click the **Run** button under **package.json** for the **dev** script

It is also possible to run the backend and frontend separately:

- In the terminal, from the root directory, run the `npm run server` command to run the backend
- Run the `npm run client` command to run the frontend
- These can also be run from the NPM SCRIPTS pane in VS Code

Either way, the application should be running! It will not actually function perfectly just yet, but it will be alive.

## Configuring a Database
When running the application, there should be a message that says:

```
Error: The `uri` parameter to `openUri()` must be a string, got "undefined". Make sure the first parameter to `mongoose.connect()` or `mongoose.createConnection()` is a string.
```

This is because the application expects a database connection string, and there currently is not one.

### Setting Up Your Own Cloud Database
First, you'll want to create a database cluster using MongoDB Atlas online. [Click here for instructions.](MongoAtlasSetup.md) By the end of the setup process, be sure to copy the connection string.

### Connecting to the Database
Once the connection string has been obtained, it will need to live in a **.env** file. This is a secret file, not stored in GitHub, that allows developers to configure the environment an instance of an application.

1. Find the **.env-example** file in the codebase
1. Rename it to **.env**
1. Replace `YOUR_URI_HERE` with the copied connection string
1. Replace `YOUR_DBNAME_HERE` with any name desired (e.g., `hytop-local`)

Once that environment has been setup, run the application again using `npm run dev`. It should actually be connected to your database!

## Connecting the Frontend & Backend
In order to make requests from the frontend to the backend, a frontend **.env** file must be created. Like with the backend, this file allows a developer to configure the environment for the application.

Create a file named **.env** within the **frontend** folder, and add this code:

```
VITE_BACKEND_URL="http://localhost:5000"
```

This will point requests from the frontend to the proper backend. If needed, update the URL so it points to the right place.

## Testing
With all of the setup complete, try registering for an account, and logging into the application. Check the cluster in MongoDB Atlas online, and ensure that the user data is there.

## Conclusion
This should be all that's needed for an up-and-running application. Note that it is not necessary to understand any of the code just yet... the first step is to simply run it and make sure it's working.
