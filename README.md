# Discord-probot-transfer

[![downloadsBadge](https://img.shields.io/npm/dt/discord-probot-transfer)](https://npmjs.com/discord-probot-transfer)
[![versionBadge](https://img.shields.io/npm/v/discord-probot-transfer)](https://npmjs.com/discord-probot-transfer)
[![discordBadge](https://img.shields.io/discord/828240195236266005?color=7289da)](https://discord.gg/VwTxJaqjsJ)

## Installation

### Install **[discord-probot-transfer](https://npmjs.com/package/discord-probot-transfer)**

```sh
$ npm install discord-probot-transfer
```

### Install **[discord.js](https://npmjs.com/package/discord.js)**

```sh
$ npm install discord.js
```

# Features

- Simple & easy to use 🎗️
- Support All probot language 🔗
- Returns full data of transfer 📡

## Getting Started

At first install the [discord-probot-transfer](https://npmjs.com/discord-probot-transfer) package

```js
const { Client, Intents } = require("discord.js"); // npm i discord.js
const client = new Client({
  intents: [
    Intents.FLAGS.GUILDS,
    Intents.FLAGS.GUILD_MESSAGES,
    Intents.FLAGS.GUILD_MEMBERS,
  ],
});



const { Probot } = require("discord-probot-transfer"); // npm i discord-probot-transfer
Probot(client, {
  probot: "567703512763334685", // your probot id
  owners: ["496941648576643092"], // member(s) who must transfer credit to them
});



client.on("transfered", (guild, data, err) => {
  //
  if (err) return console.log(err.message);
  //
  var { member, price, owner, fullPrice } = data;
  //

  /* What you can do? let's see. */

  member.send(`> Thanks for your donate, \`${price}\`.`); // send message to member
  //
  guild.channel.send(`> ${member.user}, Thanks for your donate \`${price}\``); // send message in same channel
  //
  guild.channels.cache
    .get("id")
    .send(
      `> ${member.user} transfer \`${price}\` to ${owner.user} in channel ${guild.channel}`
    ); // send message to specific channel
  //
  member.roles.add("id"); // add role(s) to member
  //
  member.roles.remove("id"); // remove role(s) from member
  //
  /* add role(s) for member when price is 40000 */
  if (price == "40000") {
    member.roles.add("id");
  }
  //
});


client.login("BOT TOKEN")

```
## Thanks.

