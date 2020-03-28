# Everybody Edits Universe Messages Protocol
This repository contains documentation on the EEUniverse protocol (By Jesse) based on the [Everybody Edits Universe](http://ee-universe.com) API.  
Protocol Update: 2020-03-19 
Use [EEUProtocolTool](https://github.com/capasha/EEUProtocolTool) to check the protocol.  

## Table of contents
- [Game Information](#game-information)
- [Room Types](#room-types)
- [Receive Messages from Client](#receive-messages-client)
  - [SelfInfo](#rm-selfinfo)
- [Receive Messages from Connection](#receive-messages-conn)
  - [CanEdit](#rm-canedit)
  - [CanGod](#rm-cangod)
  - [Chat](#rm-chat)
  - [ChatInfo](#rm-chatinfo)
  - [ChatOld](#rm-chatold)
  - [Clear](#rm-clear)
  - [RoomConnect](#rm-roomconnect)
  - [PlaceBlock](#rm-placeblock)
    - [Sign](#rm-placesign)
  - [PlayerAdd](#rm-playeradd)
  - [PlayerExit](#rm-playerexit)
  - [PlayerGod](#rm-playergod)
  - [PlayerJoin](#rm-playerjoin)
  - [PlayerMove](#rm-playermove)
  - [PlayerSmiley](#rm-playersmiley)
  - [Won](#rm-won)
  - [ZoneCreate](#rm-zonecreate)
  - [ZoneEdit](#rm-zoneedit)
  - [ZoneDelete](#rm-zonedelete)
- [Send Messages Connection](#send-messages)
  - [test](#sm-test)

## <a id="receive-messages-client">Receive Messages from Client</a>    

### <a id="rm-selfinfo">"SelfInfo"</a>
Occurs when you read SelfInfo

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `String`    | Nickname      	    | Your nickname
| `1`  | `Integer`   | MaxEnergy          | Your max energy
| `2`  | `Integer`   | Stardust		        | Your stardust
| `3`  | `Integer`   | Jewels             | Your jewels
| `4`  | `Integer`   | Worlds             | How many worlds you have
| `...`  | `Object`  | World Info         | Read world information

Example: loop through Worlds, then read through each object.  
This will return: WorldID, WorldTitle, WorldPlays, Hidden or not.

## <a id="receive-messages-conn">Receive Messages from Connection</a>    

### <a id="rm-canedit">"CanEdit"</a>
Occurs when a player's edit is modified

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `Integer`   | ID                 | The player's ID
| `1`  | `Boolean`   | Can Edit           | Whether the player can edit or not

### <a id="rm-cangod">"CanGod"</a>
Occurs when a player's god mode is modified

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `Integer`   | ID                 | The player's ID
| `1`  | `Boolean`   | Can God            | Whether the player can toggle god mode or not

### <a id="rm-chat">"Chat"</a>
Occurs when a chat message is sent

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `Integer`   | ID                 | The player's ID
| `1`  | `String`    | Text               | The chat message

### <a id="rm-chatinfo">"ChatInfo"</a>
Occurs when a chat response is received from using a command.

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `String`    | Text               | The chat message

### <a id="rm-chatold">"ChatOld"</a>
Occurs during RoomConnect. The five most recent messages prior to connecting are received.

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `String`    | Username           | The player's username
| `1`  | `String`    | Text               | The chat message

### <a id="rm-chatpmfrom">"ChatPMFrom"</a>
Occurs when you receive a private message.

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `Integer`   | ID                 | The sender's ID
| `1`  | `String`    | Text               | The chat message

### <a id="rm-chatpmto">"ChatPMTo"</a>
Occurs when you send a private message.

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `Integer`   | ID                 | The receiver's ID
| `1`  | `String`    | Text               | The chat message

### <a id="rm-clear">"Clear"</a>
Occurs when `/clear` is used

### <a id="rm-bgcolor">"BgColor"</a>
Occurs when `/bgcolor hexcolor` is used.

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `Integer`   | UintColor          | The Color is sent as uint color.

### <a id="rm-roomconnect">"RoomConnect"</a>
Occurs when you connect to a world

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `Integer`   | ID                 | Your ID
| `1`  | `String`    | Owner Username     | The world owner's username
| `2`  | `???`       | ???                | ???
| `3`  | `???`       | ???                | ???
| `4`  | `Integer`   | X                  | Your X coordinate
| `5`  | `Integer`   | Y                  | Your Y coordinate
| `6`  | `String`    | Title              | The world's title
| `7`  | `String`    | Username           | Your username
| `8`  | `Integer`   | Background Color   | The world's background color
| `9`  | `Integer`   | World Width        | The world's width
| `10` | `Integer`   | World Height       | The world's height
| `11 : MessageCount - 5` | `Object[]` | World Data      | The world data
| `MessageCount - 4` | `Integer` | Time Offset  | ???
| `MessageCount - 3` | `Boolean` | Can Edit     | Whether you can edit or not
| `MessageCount - 2` | `Boolean` | Is Mod       | Whether you are a mod or not
| `MessageCount - 1` | `Integer` | Zone Count   | Number of zones

You can parse the world data from index `11` to `MessageCount - 5`.

### <a id="rm-placeblock">"PlaceBlock"</a>
Occurs when a block is placed

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `Integer`   | Layer              | 0 For background and 1 foreground.
| `1`  | `Integer`   | X                  | The X coordinate
| `2`  | `Integer`   | Y                  | The Y coordinate
| `3`  | `Integer`   | ID                 | The block ID

* Portal  
Additional values for placed portals  

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `4`  | `Integer`   | Rotation           | The rotation
| `5`  | `Integer`   | Id                 | The id
| `6`  | `Integer`   | Target             | The target
| `7`  | `Boolean`   | Flipped            | Flipped or not

* Sign  
Additional values for placed signs  

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `4`  | `String`    | Text               | The sign's text
| `5`  | `Integer`   | Form               | The sign's orientation

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
| `31` | `Double`    | Space Timestamp    | When the player pressed space
| `32` | `Boolean`   | Can God            | Whether the player can toggle god mode or not
| `33` | `Boolean`   | Can Edit           | Whether the player can edit or not
| `34` | `Boolean`   | Is Mod             | Whether the player is a mod or not

`Space Timestamp` will have a value of `∞` if `Pressed Space` is `false`.

### <a id="rm-playerexit">"PlayerExit"</a>
Occurs when a player leaves the world

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `Integer`   | ID                 | The player's ID

### <a id="rm-playergod">"PlayerGod"</a>
Occurs when a player toggles god mode

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `Integer`   | ID                 | The player's ID
| `1`  | `Boolean`   | God Mode           | Whether the player is in god mode or not

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
| `6`  | `Boolean`   | Can God            | Whether the player can toggle god mode or not
| `7`  | `Boolean`   | Can Edit           | Whether the player can edit or not
| `8`  | `Boolean`   | Is Mod             | Whether the player is a mod or not

### <a id="rm-playermove">"PlayerMove"</a>
Occurs when a player moves

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `Integer`   | ID                 | The player's ID
| `1`  | `Double`    | Time               | ???
| `2`  | `Double`    | ???                | ???
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
| `28` | `Integer`   | Unknown             | Unknown
| `29` | `Boolean`   | Pressed Space      | Whether the player pressed space or not
| `30` | `Double`    | Space Timestamp    | When the player pressed space
| `31` | `Boolean`   | God Mode           | Whether the player is in god mode or not

Indexes `12` to `17` contain the `X` and `Y` coordinates (in order) of the blocks the player touch during movement.

### <a id="rm-playersmiley">"PlayerSmiley"</a>
Occurs when a player changes their smiley

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `Integer`   | ID                 | The player's ID
| `1`  | `Integer`   | Smiley ID          | The smiley's ID

### <a id="rm-won">"Won"</a>
Occurs when a player touch the crown

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `Integer`   | ID                 | The player's ID

### <a id="rm-zonecreate">"ZoneCreate"</a>
Occurs when a zone is created

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `Integer`   | ID                 | The zone's ID

### <a id="rm-zoneedit">"ZoneEdit"</a>
Occurs when a zone is edited

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `Integer`   | ID                 | The zone's ID
| `1`  | `Boolean`   | Edit Type          | Whether you are adding or removing zone area
| `2`  | `Integer`   | X                  | The top left X coordinate of the edit
| `3`  | `Integer`   | Y                  | The top left Y coordinate of the edit
| `4`  | `Integer`   | Width              | The width of the edit
| `5`  | `Integer`   | Height             | The height of the edit

Note that the `X` and `Y` values are not the top left coordinates of the entire zone, but only the edit. Same goes for the width and length.

### <a id="rm-zonedelete">"ZoneDelete"</a>
Occurs when a zone is deleted

| ID   | Type        | Name               | Description
| ---  | ---         | ----               | -----------
| `0`  | `Integer`   | ID                 | The zone's ID


## <a id="send-messages">Send Messages Connection</a>  


