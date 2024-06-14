# Architecture
Information coming soon!

## Actual Hacking
Some intrepid young game players may want to _actually_ hack the game instead of the pseudo-hacking built into the game. Ideally, there would be layers of security in place to prevent them from doing so. However, if the game is to be accessible offline (e.g., without a server or database), verifying their actual progress could be incredibly difficult. Most of the gameplay almost inherently _has_ to be hackable. However, the players should also have their own accounts and be able to represent themselves and their progress _without_ fear of being hacked by other players. Thus, the overall philosophy regarding hacking is this:

**There will be no protections against hacking the basic gameplay of the application, but user information and "Collectibles" will be secure in the backend.**

The basic gameplay includes things like the number of bits, currency amount, upgrades, achievements, and more. It may be very easy for players to open up `localStorage` in their web browser and change the numbers around - but really, it's all for fun anyway, so that's fine.

The user information, like username, password, profile, and collected items, can remain behind the security of authentication. This will hopefully create a community economy in which unhackable user data holds much more weight than amount of in-game data or in-game currency.

Essentially, a user can "hack" whatever garbage they want into their saved game data - it is not worth preventing this from happening. However, they will **not** be able to "hack" a new collectible item into their showcase, or "hack" another player's user information.

Overall, this should make it much easier to work with game data offline, while still encouraging players to create accounts, collect collectibles, and connect with other players.
