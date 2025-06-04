# Technologies
This project combines a number of technologies that work together to create the game experience and functionality.

## Shared Language
Both the frontend and the backend of the application use [TypeScript](https://www.typescriptlang.org/).

## Backend
The backend is built with [Node.js](https://nodejs.org/en) and [Express](https://expressjs.com/).

The server connects to the frontend through HTTP - this serves as an API for the frontend.

The server interfaces with the [MongoDB](https://www.mongodb.com/) database using [mongoose](https://mongoosejs.com/).

For authentication, the server uses [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken).

## Frontend
The frontend is built with [React](https://react.dev/).

It uses [React Redux](https://react-redux.js.org/) to store state.

The project uses [Vite](https://vitejs.dev/) as a build tool.
