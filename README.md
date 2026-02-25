<h1 align="center">Mineflayer Pathfinding Bot Example</h1>
<br>
<p>Pathfinding Bot</p>

```javascript
const mineflayer = require('mineflayer')
const { pathfinder, Movements, goals} = require('mineflayer-pathfinder')
const GoalFollow = goals.GoalFollow

/* 
How the bot works:
    const bot is the function that creates the bot,
    host is the ip of the server,
    port is the port of the server, (needs to be specific if the server is not using the default port which is 25565)
    username is the username of the bot, (can be anything if the bot is cracked)
*/

// self explanatory
const bot = mineflayer.createBot({
    host: "localhost", // put server ip here
    port: 25565, // put port here ie: 3000
    username: "User_Here",
    // auth: "offline", // auth is the method of logging in, offline means the bot is cracked else its a premium account use if you want to get it on a server
    version: "1.21.11", // only set if you need a specific version or snapshot (ie: "1.8.9" or "1.16.5"), otherwise it's set automatically
    // loginCommand: "/login " + process.argv[2], // Process.argv adds a command line argument so people cant get the password easily Usage: "node Kitbot.js <password>"
    hideErrors: false
});

bot.loadPlugin(pathfinder)

function followPlayer() {
    const player = bot.players["Username"]
 
    if (!player || !player.entity) {
        bot.chat("I cant see User")
        return
    }

    const mcData = require('minecraft-data')(bot.version)
    const movements = new Movements(bot, mcData)
    bot.pathfinder.setMovements(movements)

    const goal = new GoalFollow(playerCE.entity, 1) // 1 is the distance the bot will attempt to get to you b4 stopping
    bot.pathfinder.setGoal(goal, true) // true means the bot will recalculate the path every tick, so it will follow you even if you move

}

bot.once('spawn', followPlayer)
```
