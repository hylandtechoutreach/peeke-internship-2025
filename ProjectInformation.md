# HYLAND TECH OUTREACH PORTAL (HyTOP)
_an online IDE for Hyland Tech Outreach programs_

## Description
This application will help students learn to code while providing a fun and engaging game experience. Taking inspiration from incremental games like [Cookie Clicker](https://en.wikipedia.org/wiki/Cookie_Clicker), [AdVenture Capitalist](https://en.wikipedia.org/wiki/AdVenture_Capitalist), [Idle Slayer](https://idleslayer.com/), and [Candy Box](https://candybox2.github.io/candybox/), the game will encourage players to return on a regular basis to build up their hoard of data AND their programming acumen.

### Player Learning
The game will be designed in such a way that players will learn about computer science without even realizing it - through puzzles, mini-games, achievements, and challenges. Learning should in no way be the main focus of the game - it will simply be a byproduct of the playing experience. The hope is that by prioritizing the actual gameplay, students will be more compelled to return and keep learning in order to keep playing the game.

Because the game itself is written in TypeScript/JavaScript, the code presented to the player should all be actual JavaScript code. That said, the language specifics are not the important thing to teach - it is much more important to teach the _concepts_ behind the code. For example, players should have the opportunity to learn about things like:

- Loops
- Arrays
- Variables
- Functions
- Conditional Statements
- Data Structures

Since the codebase itself uses all of these concepts, the idea is to bring some of that to light in a simplified, welcoming, playground environment. This peek behind the curtain should hopefully help the players realize that they too could build a game like this if they wanted to build it!

### Why an Idle Game?
Essentially, [people like when number go bigger](https://fictiontalk.com/2021/08/25/the-psychology-of-idle-games-why-humans-like-big-numbers/). This will hopefully keep players invested, and make them want to level up their coding skills.

## Gameplay
The goal of the game is to collect as much _data_ as possible. Initially, this will happen by tapping `1`s and `0`s as they randomly appear on a screen - kind of like [Whac-A-Mole](https://en.wikipedia.org/wiki/Whac-A-Mole). As the game progresses, players will be able to "hack" the data collection process to automatically collect data, enhance their data storage, and more - all through coding. Players will also be able to _sell_ their data to receive currency. This currency can be used to purchase upgrades: making bits appear more frequently, checking for bits more frequently, superpowers like data magnets, increasing the value of each collected chunk, or AI.

All of the basic gameplay will be possible without signing in or storing data in a database. This will allow anyone to start playing very quickly, and even play offline - their game data will be stored in the browser local storage.

### Accounts: Collectible Items
There will also be an option to create an account. This will allow for cloud saves, and, most importantly, the appearance of collectible items. These items (like [Blooks](https://blooket.fandom.com/wiki/Blooks)) will have a cool name. They will:

- Appear randomly
- Appear only when connected to the server with an account  
    - Except for the first one, which is only collectible with an account
- Be showcased and traded
- Have different levels of rarity
- Be awarded for some achievements
- Sometimes join together to unlock the final form (like [Exodia from Yu-Gi-Oh!](https://yugioh.fandom.com/wiki/Forbidden_One))
- Be available from purchaseable random boxes (using in-game currency)
- Regularly provide new releases to promote sustainability/long-term play

This will provide an opportunity for players to connect and interact.

### Learning Journeys
There will be various ways to learn and practice computer science skills within the game.

- There may be instructional lesson videos (edutainment)
- There may be puzzles (drag code to the right place)
- All of the learning will be available offline
- There will be some collectibles only available through the learning (must be registered)

The learning is the primary purpose of the application; however, it should never take away from the players' enjoyment of the game.

### Creativity
There will be several opportunities for creativity during this project. Many aspects exist beyond the actual coding:

- Art
- Music
- Game Design
- User Experience
- Marketing

Ultimately, the vision for the game will be determined by the intern team.

## GitHub
The codebase is stored in this GitHub Repository:  
[https://github.com/hto-projects/hytop](https://github.com/hto-projects/hytop)

Issues will be tracked in this GitHub Project:  
[https://github.com/orgs/hto-projects/projects/8](https://github.com/orgs/hto-projects/projects/8)

## Current State
Currently, the game does not do much. There is a lot of work to be done.

The deployed application is hosted [on render](https://autohack-idle.onrender.com/).

## Copyright
All team members will be listed as copyright holders for the application codebase.

## Additional Information
Check out these pages for more information:

- [Technologies (MERN Stack + Phaser)](Technologies.md)
- [Architecture](Architecture.md)
- [Team Workflow (Trunk-based Development)](TeamWorkflow.md)
