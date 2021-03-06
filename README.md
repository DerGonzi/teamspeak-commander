TeamSpeak Command Interface for TS3-NodeJS-Library
===

[![Build Status](https://github.com/multivit4min/teamspeak-commander/workflows/Node%20CI/badge.svg)](https://travis-ci.com/Multivit4min/teamspeak-commander)
[![Coverage Status](https://coveralls.io/repos/github/Multivit4min/teamspeak-commander/badge.svg?branch=master)](https://coveralls.io/github/Multivit4min/teamspeak-commander?branch=master)
[![npm](https://img.shields.io/npm/v/teamspeak-commander.svg)](https://www.npmjs.com/package/teamspeak-commander)
[![Discord](https://img.shields.io/discord/653273459840778270)](https://discord.gg/Z5rdcGu)

## **This is still work in progress API may change without notice**

# Introduction

This library allows you to easily create commands for your teamspeak server using `ts3-nodejs-library`

## Install

`npm install --save teamspeak-commander`


# Documentation

You can find all necessary documentation [here](https://multivit4min.github.io/teamspeak-commander) or a lot of examples in the **docs** folder of this project!


Usage:

```javascript
const { TeamSpeak } = require("ts3-nodejs-library")
const { Commander } = require("teamspeak-commander")

const commander = new Commander({ prefix: "!" })

//command !ping
commander.createCommand("ping")
  .setHelp("sends pong as response")
  .run(event => {
    event.reply("Pong!")
  })

//command !roll 10 -> rolls a number between 1 and 10
//command !roll -> rolls a number between 1 and 6
commander.createCommand("roll")
  .help("rolls a number")
  .addArgument(arg => arg.number.name("max").optional(6))
  .run(event => {
    const random = Math.floor(Math.random() * event.arguments.max) + 1
    event.reply(`Rolled a ${random} (from 1-${event.arguments.max})`)
  })

TeamSpeak.connect({
  host: "....",
}).then(teamspeak => {
  commander.addInstance(teamspeak)
})
```