# Everybody Edits Universe Messages Protocol
This repository contains documentation on the EEUniverse protocol(By Jesse) based [Everybody Edits Universe](http://ee-universe.com) API.  
Protocol Update: 2019-11-22

## Table of contents
- [Game Information](#game-information)
- [Room Types](#room-types)
- [Receive Messages from Client](#receive-messages-client)
  - [SelfInfo](#rm-selfinfo)
- [Receive Messages from Connection](#receive-messages-conn)
  - [RoomConnect](#rm-roomconnect)
  - [PlaceBlock](#rm-placeblock)
    - [Sign](#rm-placesign)
  - [PlayerAdd](#rm-playeradd)
  - [PlayerExit](#rm-playerexit)
  - [PlayerJoin](#rm-playerjoin)
  - [PlayerMove](#rm-playermove)
- [Send Messages Connection](#send-messages)
  - [test](#sm-test)


### <a id="rm-selfinfo">"SelfInfo"</a>
Occurs when you read SelfInfo

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `String`    | Nickname      	    | Your nickname.
| `1`  | `Integer`   | MaxEnergy          | Your max energy.
| `2`  | `Integer`   | Stardust		        | Your stardust.
| `3`  | `Integer`   | Jewels             | Your jewels.
| `4`  | `Integer`   | Worlds             | How many worlds you have.
| `...`  | `Object`  | World Info         | Read world information.

Example: loop through Worlds, then read through each object.  
This will return: WorldID, WorldTitle, WorldPlays.

### <a id="rm-roomconnect">"RoomConnect"</a>
Occurs when you connect to a world

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `Integer`   | ID                 | Your ID.
| `1`  | `String`    | Owner Username     | The world owner's username.
| `2`  | `???`       | ???                | ???
| `3`  | `???`       | ???                | ???
| `4`  | `Integer`   | X                  | Your X coordinate.
| `5`  | `Integer`   | Y                  | Your Y coordinate.
| `6`  | `String`    | Title              | The world's title.
| `7`  | `String`    | Username           | Your username.
| `8`  | `???`       | ???                | ???
| `9`  | `Integer`   | World Width        | The world's width.
| `10` | `Integer`   | World Height       | The world's height.
| `11 : MessageCount - 5` | `Object[]` | World Data      | The world data.
| `MessageCount - 4` | `Integer` | Time Offset  | ???
| `MessageCount - 3` | `Boolean` | Can Edit     | Whether you can edit or not
| `MessageCount - 2` | `Boolean` | Is Mod       | Whether you are a mod or not
| `MessageCount - 1` | `Integer` | Zone Count   | Number of zones

You can parse the world data from index `11` to `MessageCount - 5`.

### <a id="rm-placeblock">"PlaceBlock"</a>
Occurs when a block is placed

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `Integer`   | X                  | The X coordinate
| `1`  | `Integer`   | Y                  | The Y coordinate
| `2`  | `Integer`   | ID                 | The block ID
| `3 : MessageCount - 1`  | `Object[]` | Parameters        | Any additional block parameters

### <a id="rm-placesign">"Sign"</a>
Additional values for placed signs

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `3`  | `String`    | Text               | The sign's text
| `4`  | `Integer`   | Form               | The sign's orientation

### <a id="rm-playeradd">"PlayerAdd"</a>
Occurs when initializing current players in the world

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `Integer`   | ID                 | The player's ID
| `1`  | `String`    | Username           | The player's username
| `2`  | `Integer`   | ???                | ???
| `3`  | `Integer`   | ???                | ???
| `4`  | `Integer`   | ???                | ???
| `5`  | `Integer`   | ???                | ???
| `6`  | `Integer`   | ???                | ???
| `7`  | `Double`    | X                  | The player's X coordinate
| `8`  | `Double`    | Y                  | The player's Y coordinate
| `9`  | `Double`    | ???                | ???
| `10` | `Double`    | ???                | ???
| `11` | `Integer`   | ???                | ???
| `12` | `Integer`   | ???                | ???
| `13` | `Double`    | ???                | ???
| `14` | `Integer`   | ???                | ???
| `15` | `Integer`   | ???                | ???
| `16` | `Integer`   | ???                | ???
| `17` | `Integer`   | ???                | ???
| `18` | `Integer`   | ???                | ???
| `19` | `Integer`   | ???                | ???
| `20` | `Integer`   | ???                | ???
| `21` | `Integer`   | ???                | ???
| `22` | `Integer`   | ???                | ???
| `23` | `Integer`   | ???                | ???
| `24` | `Integer`   | ???                | ???
| `25` | `Integer`   | ???                | ???
| `26` | `Integer`   | ???                | ???
| `27` | `Integer`   | ???                | ???
| `28` | `Integer`   | X                  | The player's X coordinate
| `29` | `Integer`   | Y                  | The player's Y coordinate
| `30` | `Boolean`   | Pressed Space      | Whether the player pressed space
| `31` | `Double`    | Space Timestamp          | When the player pressed space
| `32` | `Boolean`   | God Mode           | Whether the player is in god mode or not
| `33` | `Boolean`   | Can Edit           | Whether the player can edit or not
| `34` | `Boolean`   | Is Mod             | Whether the player is a mod or not

`Space Timestamp` will have a value of `∞` if `Pressed Space` is `false`.

### <a id="rm-playerexit">"PlayerExit"</a>
Occurs when a player leaves the world

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `Integer`   | ID                 | The player's ID

### <a id="rm-playerjoin">"PlayerJoin"</a>
Occurs when a player joins the world

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `Integer`   | ID                 | The player's ID
| `1`  | `String`    | Username           | The player's username
| `2`  | `Integer`   | ???                | ???
| `3`  | `Double`    | ???                | ???
| `4`  | `Integer`   | X                  | The player's X coordinate
| `5`  | `Integer`   | Y                  | The player's Y coordinate
| `6`  | `Boolean`   | ???                | ???
| `7`  | `Boolean`   | Can Edit           | Whether the player can edit or not
| `8`  | `Boolean`   | Is Mod             | Whether the player is a mod or not

### <a id="rm-playermove">"PlayerMove"</a>
Occurs when a player moves

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `Integer`   | ID                 | The player's ID
| `1`  | `Integer`   | Time               | ???
| `2`  | `Integer`   | ???                | ???
| `3`  | `Integer`   | Horizontal Direction   | The player's horizontal direction
| `4`  | `Integer`   | Vertical Direction     | The player's vertical direction
| `5`  | `Double`    | X                  | The player's X coordinate
| `6`  | `Double`    | Y                  | The player's Y coordinate
| `7`  | `Double`    | ???                | ???
| `8`  | `Double`    | ???                | ???
| `9`  | `Double`    | ???                | ???
| `10` | `Double`    | ???                | ???
| `11` | `Double`    | Drag               | The player's drag value
| `12 : 17` | `Integer`   | Edges         | The coordinates of the edges the player touch
| `18 : 23` | `Integer`   | Sliding Parameters   | Values used for calculating sliding
| `24` | `Double`    | Horizontal Force   | The horizontal reaction force
| `25` | `Double`    | Vertical Force     | The vertical reaction force
| `26` | `Integer`   | Grid X             | The X coordinate of the block the player is in
| `27` | `Integer`   | Grid Y             | The Y coordinate of the block the player is in
| `28` | `Boolean`   | Pressed Space      | Whether the player pressed space or not
| `29` | `Double`    | Space Timestamp    | When the player pressed space
| `30` | `Boolean`   | God Mode           | Whether the player is in god mode or not

Indexes `12` to `17` contain the `X` and `Y` coordinates (in order) of the blocks the player touch during movement.




























