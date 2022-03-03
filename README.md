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
- Easy setup & setting for each server ⚙️
- Edit & Get any data with simple function ⛏️
- Returns full data of transfer 📡
- Event & Collection system 🔗

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
/// Important !
client.probot = Probot(client, {
  fetchGuilds: true, // enable event for all bot guilds
  data: [
    // server setting.
    {
      fetchMembers: true, // enable event for all guild member, not only the owner(s)
      guildId: "828240195236266005",
      probotId: "567703512763334685",
      owners: ["496941648576643092"],
    },
  ],
});

client.on("ready", () => console.log("Ready"));

// event.
client.probot.on("transfered", (guild, data, err) => {
  //
  if (err) return console.log(err);
  //
  var { member, price, receiver, owner, fullPrice } = data;
  //
  /* What you can do? let's see. */

   member.send(`> Thanks for your donate, \`${price}\`.`); // send message to member
  //
  guild.channel.send(`> ${member.user}, Thanks for your donate \`${price}\``); // send message in same channel
  //

  guild.channels.cache
    .get("id")
    .send(
      `> ${member.user} transfer \`${price}\` to ${receiver.user} in channel ${guild.channel}`
    ); // send message to specific channel
  //
  member.roles.add("id"); // add role(s) to member
  //
  member.roles.remove("id"); // remove role(s) from member
  //
  // add role(s) for member when price is 40000 **
  if (price == "40000") {
    member.roles.add("id");
  }
  // add role(s) for member when the receiption is owner
  if (owner) {
    member.roles.add("id");
  }
  // send file when transfer in specific channel
  if (guild.channel.id == "id") {
    guild.channel.send({ files: ["<Buffer | Link>"] });
  }
  //
});

client.on("message", async (message) => {
  var args = message.content.split(/ +/);
  if (message.content == "buy") {
    if (client.probot.check(message))
      return message.channel.send(` you already have an order !`);
    message.channel.send(
      "> Hello, \nyou have 5 minute for transfer `$5264` to owners."
    );

    var check = await client.probot.collect(message, {
      probotId: `567703512763334685`,
      owners: ["496941648576643092"],
      time: 1000 * 60 * 5, // 5 min
      userId: message.author.id, // when you not specify the user, return full collection for first transfer in main channel.
      price: 5000, 
    });
    if (check.status) {
      return message.channel.send(
        `> Thanks for your donate ${check.member},  ${check.priceTransfered}.`
      );
    } else if (check.error) {
      return message.channel.send(`> ${check.error.message} 😢`);
    } else {
      return message.channel.send(`> Required credit: ${check.priceRequired},
      you transfered: ${check.fullPrice}, 
      i got: ${check.priceTransfered},
      retry and transfer ${check.priceTotal}`);
    }
  } else if (args[0] == "tax") {
    if (!args[1]) return;
    var price = client.probot.tax(args[1]);
    message.channel.send(`${price.amount} => ${price.withTax}`);
  }
});

// More functions.
client.probot.getData(); // to get all data setup
client.probot.create({ guildId, probotId, owners, fetchMembers }); // create new data for server
client.probot.edit("guildId", { probotId, owners, fetchMembers }); // edit data for specific server
client.probot.delete("guildId"); // delele server data

// for use only tax 
const { tax } = require("discord-probot-transfer");
console.log(tax("5000")) // Object.
```

## Thanks.
