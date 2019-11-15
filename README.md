# Everybody Edits Universe Messages Protocol
This repository contains documentation on the EEUniverse protocol(By Jesse) based [Everybody Edits Universe](http://ee-universe.com) API.  
Protocol Update: 2019-10-17

## Table of contents
- [Game Information](#game-information)
- [Room Types](#room-types)
- [Receive Messages from Client](#receive-messages-client)
  - [SelfInfo](#rm-selfinfo)
- [Receive Messages from Connection](#receive-messages-conn)
- [Send Messages Connection](#send-messages)
  - [test](#sm-test)


### <a id="rm-selfinfo">"SelfInfo"</a>
Occurs when you read SelfInfo

| Id   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `String`    | Nickname      	  | You're Nickname.
| `1`  | `Integer`   | MaxEnergy          | You're Max Energy.
| `2`  | `Integer`   | Stardust		      | You're Stardust.
| `3`  | `Integer`   | Jewels             | You're Jewels.
| `4`  | `Integer`   | Worlds             | How many worlds you have.
| `...`  | `Object`  | World Info         | Read world information.

Example: loop through Worlds, then read through each object.  
This will return: WorldID, WorldTitle, WorldPlays.

