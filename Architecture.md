# Architecture
This guide contains an overview of the architecture for the application.

## Shared
Some pieces of the application are shared by both the frontend and the backend. This is especially important when the frontend and backend need to use the same types variables and objects.

### Types
The **shared/types.ts** file contains the types for the data within the application. Actually, it only has [`enum`](https://www.typescriptlang.org/docs/handbook/enums.html) and [`interface`](https://www.typescriptlang.org/docs/handbook/2/objects.html) declarations, but these are used to ensure the data is in the proper form everywhere.

As an example, the game data stores the number of bits collected, the amount of currency earned, the user's email, and a list of owned upgrades. This is done with the `IGameData` interface.

### Utility Functions
The **shared/util.ts** file contains some helper functions that can be utilized throughout the application:

- The `pluck` function takes an array and a predicate function, and removes one value from the array that satisfies the predicate
- The `runMod` function takes a variable value and modifies it based on the value and mod function
- The `calculateVariableValue` function calculates the value of a game variable (like the likelihood of a bit appearing)

### Upgrades
The `IUpgrade` interface represents objects that are upgrades in the game (like the one that doubles the amount of bits that appear). Each upgrade has a name, description, cost, picture, and list of effects.

Each effect is an `IUpgradeEffect`. These effects define a modification to one of the `GameVariable` values. They point to one of those variables, have a `VariableModFunction` to determine how the variable will be updated, and have a `modValue` to represent the amount of change. Here's an example of an upgrade from the **shared/upgrades.ts** file:

```ts
{
  name: "Double Checks",
  description: "Check for bits twice as often",
  picture: "🔍🔍",
  cost: 10,
  effects: [
    {
      variableAffected: GameVariable.BitCheckInterval,
      variableMod: VariableModFunction.Multiply,
      modValue: 0.5
    }
  ]
}
```

It is named "Double Checks" and it costs 10 currency. When owned, it modifies the `BitCheckInterval` game variable - basically, how often the game should check for bits to appear. It uses the `Multiply` mod, and `0.5` as the `modValue` to split the amount in half. Effectively, this takes the normal "once per second" check and makes it "once per half second" instead.

## Frontend
The frontend of the application is built using [React](https://react.dev/), [React Redux](https://react-redux.js.org/), and [Phaser](https://phaser.io/).

### Starting Point
The actual starting point is the **frontend/index.html** file - however, that file does not do much beyond including the **frontend/src/main.tsx** file:

```html
<script type="module" src="/src/main.tsx"></script>
```

The **main.tsx** file is the main entry point into the actual React application. This file does not do anything too interesting - it does have a little router that is not currently used very much. The main thing it does is point the root (`"/"`) to the **App.tsx** file. The  important thing is the `ReactDOM.createRoot` - that renders the React application into the HTML. The interesting thing there is the `Provider` element:

```tsx
<Provider store={store}>
```

That `store` is the React Redux store - basically, the thing that holds all of the data for the frontend.

So, from there, there are two big things: the `<App>` component (from the **App.tsx** file), and the Redux `store` (from the **store.ts** file).

### App
In the **App.tsx** file lives the `<App>` component. This is really the main HTML container for everything else in the game. It contains the actual `<PhaserGame>` component (the part that uses the Phaser library and has the bits appearing), as well as a `<BoxContainer>` that includes the left `<Box>` for auth and the right `<Box>` for game data.

### Store
The game data is kind of magically distributed throughout the app using [Redux](https://redux.js.org/). There is quite a bit that goes into writing Redux code - it is recommended to read through some of the [essential concepts](https://redux.js.org/tutorials/essentials/part-1-overview-concepts) and [structure](https://redux.js.org/tutorials/essentials/part-2-app-structure).

The **store.ts** file stores the game data. It is in the form of the `IGameState` interface. This state is both loaded from and saved to [`localStorage`](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage) using the `loadState` and `saveState` functions. That is what allows the application to persist data over time. The store sets up a subscription - basically, every time the state is updated, it's saved to `localStorage` using `saveState`. This happens at most once per second because of the `throttle`.

The `configureStore` function sets up the store with the state (loaded from `localStorage`) and all the reducers from the slices (more on that next). 

### Slices
In Redux, a [slice](https://redux.js.org/tutorials/essentials/part-2-app-structure#redux-slices) is a collection of Redux reducer logic and actions for a single feature in the application. A reducer is basically a function that takes the current state and updates it based on an action that is occurring. There's quite a bit of slices that are doing things that are complex, but the important ones for basic gameplay are in the **gameDataSlice.ts** file and **upgradesSlice.ts** file within the **slices/** folder.

These slices tell the game how to respond to certain actions. For example, the `addBits` reducer in the `gameDataSlice` takes the current state, and updates the number of bits in the game data based on the action payload. The `addBits` reducer is dispatched by the application at various points - these all come back to the store through the reducer, and the state is updated there.

The `upgradesSlice` contains the available upgrades for purchase. Currently, it simply holds the basic starter upgrades - but as the game progresses, there may be upgrades that are revealed later.

Ultimately, slices are the tools that allow the application to update the state of the application in a "global" way using Redux.

### Components
In React, a [component](https://react.dev/learn/describing-the-ui#your-first-component) is an isolated piece of UI. Components are a lot like HTML Elements - in fact, they are represented in the same manner, using angle brackets like `<ThisComponent></ThisComponent>`. There are some components in the **frontend/src/components/** folder - all of which are meant to represent one small part of the larger game. The `<App>` component pulls in several of these components to make them work together.

For example, the `<AutoCollector>` component is a little piece of UI to represent Al the Auto-Collector. It dispatches the `addBits` reducer to add bits based on the current interval, and it also displays the current rate of bit collection. A component is just a function that returns some JSX (basically HTML with JS or TS inside).

Several components use the [`useEffect` hook](https://react.dev/reference/react/useEffect) - this allows the application to sync a component with an external system.

### Game
The actual game, with the Phaser code, is connected from the `<PhaserGame>` component. The connection between React and Phaser is based on [this template](https://phaser.io/news/2024/03/phaser-3-and-react-typescript-template). Using both allows for much more powerful interactions - the gameplay can be fun and interactive, but React can keep track of the state and interact with the backend if needed. The biggest thing with the game is the `EventBus` - this tool allows the Phaser code to interact with the rest of the application.

The actual Phaser stuff is configured in the **frontend/src/game/main.ts** file - that sets up the basic game, pointing to the scenes within the **scenes/** folder.

Each scene in Phaser inherits from the `Scene` class. Within those classes (e.g., `Collect`), game components and interactions can be added. This is the main place to control the actual physical gameplay - Phaser can be used for graphical and physical gameplay, whereas React is more for state control and communication.

## Backend
For now, don't worry too much about the backend. Ultimately, the backend will allow players to save their game data in the cloud, as well as present collectibles.

## Actual Hacking
Some intrepid young game players may want to _actually_ hack the game instead of the pseudo-hacking built into the game. Ideally, there would be layers of security in place to prevent them from doing so. However, if the game is to be accessible offline (e.g., without a server or database), verifying their actual progress could be incredibly difficult. Most of the gameplay almost inherently _has_ to be hackable. However, the players should also have their own accounts and be able to represent themselves and their progress _without_ fear of being hacked by other players. Thus, the overall philosophy regarding hacking is this:

**There will be no protections against hacking the basic gameplay of the application, but user information and "Collectibles" will be secure in the backend.**

The basic gameplay includes things like the number of bits, currency amount, upgrades, achievements, and more. It may be very easy for players to open up `localStorage` in their web browser and change the numbers around - but really, it's all for fun anyway, so that's fine.

The user information, like username, password, profile, and collected items, can remain behind the security of authentication. This will hopefully create a community economy in which unhackable user data holds much more weight than amount of in-game data or in-game currency.

Essentially, a user can "hack" whatever garbage they want into their saved game data - it is not worth preventing this from happening. However, they will **not** be able to "hack" a new collectible item into their showcase, or "hack" another player's user information.

Overall, this should make it much easier to work with game data offline, while still encouraging players to create accounts, collect collectibles, and connect with other players.
