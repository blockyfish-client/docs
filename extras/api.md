---
icon: chevron-right
order: 1000
title: Deeeep.io API
image: https://raw.githubusercontent.com/blockyfish-client/Assets/main/blockyfishclientbanner.png
---
# API
!!!warning
Still incomplete
!!!
!!!
Not all available API links maybe listed. 
!!!

Terminology:
Required perimeter `<>`
Optional perimeter `[]`

## animals
- `<name_or_id>` — Animal ID or name, value between `0` to `120`. 

Get animal by ID or name
`https://apibeta.deeeep.io/animals/<name_or_id>`

Examples
`https://apibeta.deeeep.io/animals/fish`
`https://apibeta.deeeep.io/animals/0`

## auth
### logout
Log out of account. 

Examples
`https://apibeta.deeeep.io/auth/logout`

### me
Get info of currently logged in user.

Examples
`https://apibeta.deeeep.io/auth/me`

## emotes
- `<id>` — Number ID of an emote. 
- `<userid>` — ID of user. Username doesn't work. 

Find an emote by ID
`https://apibeta.deeeep.io/emotes/<id>`

Find emotes by creator
^Currently does not work^
`https://apibeta.deeeep.io/emotes/creator/<userid>`

Examples
`https://apibeta.deeeep.io/emotes/36`

## host
- `[servers]` — Can only be `1`, shows extra info about the servers
- `[beta]` — Can only be `1`, does nothing
- `[version]` — Integer, leave blank unless you know what you're doing

Get a list of available servers
`https://apibeta.deeeep.io/hosts[servers][beta][version]`

Examples
`https://apibeta.deeeep.io/hosts`
`https://apibeta.deeeep.io/hosts?servers=1`
`https://apibeta.deeeep.io/hosts?servers=1&beta=1&version=51`

## leaderboard
- `<gameMode>` — Can be the following:
  - `1` — FFA
  - `2` — PD
  - `5` — 1v1
  - `6` — TFFA
- `<period>` — Can be the following:
  - `today`
  - `week`
  - `month`
  - `always`
- `<type>` — Can be the following:
  - `highscore`
  - `longest`
  - `mostKills`

Get leaderboard
`https://apibeta.deeeep.io/leaderboard<gameMode><period><type>`

Examples
`https://apibeta.deeeep.io/leaderboard?gameMode=1&period=always&type=longest`
`https://apibeta.deeeep.io/leaderboard?gameMode=6&period=week&type=mostkills`

## maps
- `<id>` — Number ID of a map. 
- `<string_id>` — String ID of a map. 
- `<userid>` — ID of user. Username doesn't work. 
- `[page]` — Page number of the output. 
- `[count]` — How many maps to show per page. 
- `[orderBy]` — `updated_at`, `likes`, or `created_at`
- `[period]` — How many days to look back for maps. E.g. `1`, `30`, and `0` (all time)
- `[direction]` — `ASC` or `DESC`

Find a map by ID
`https://apibeta.deeeep.io/maps/<id>`

Find a map by string ID
`https://apibeta.deeeep.io/maps/s/<string_id>`

Find maps by creator
`https://apibeta.deeeep.io/maps/u/<userid>[page][count][orderBy][period][direction]`

Examples
`https://apibeta.deeeep.io/maps/4643`
`https://apibeta.deeeep.io/maps/s/fishy_ffa`
`https://apibeta.deeeep.io/maps/u/644652?page=1&count=1&orderBy=updated_at&direction=ASC`

### packs
- `<id>` — Number ID of a map. 

Get all sprites used in a map
`https://apibeta.deeeep.io/maps/<id>/packs`

Examples
`https://apibeta.deeeep.io/maps/4643/packs`

## pets
- `<id>` — Number ID of a pet. 
- `<userid>` — ID of user. Username doesn't work. 

Find a pet by ID
`https://apibeta.deeeep.io/pets/<id>`

Find pets by creator
^Currently does not work^
`https://apibeta.deeeep.io/pets/creator/<userid>`

Examples
`https://apibeta.deeeep.io/emotes/18`

## playHistories
- `<userid>` — ID of user. Username doesn't work. 
- `[gmId]` — Gamemode ID, from `1` to `6`. 
- `[animalId]` — Animal ID, `0` to `120`. 
- `[order]` — `score` or `latest`


Get a player's play history
`https://apibeta.deeeep.io/playHistories/u/<userid>[gmId][animalId][order]`

Examples
`https://apibeta.deeeep.io/playHistories/u/5?gmId=1&animalId=1&order=score`
`https://apibeta.deeeep.io/playHistories/u/5?gmId=6&order=latest`

## regions
Get all available Deeeep.io servers
`https://apibeta.deeeep.io/regions`

## servers/l
Get your location as a latitude and longitude
`https://apibeta.deeeep.io/servers/l`

## skins
- `<skinid>` — ID of skin, should be a number. 
- `<animalid>` — ID of animal, should be a number. 
- `<creatorid>` — ID of skin creator. 

Get a skin by ID
`https://apibeta.deeeep.io/skins/<skinid>`

Get skins by animal
`https://apibeta.deeeep.io/skins?<animalid>`

Get skins by creator
`https://apibeta.deeeep.io/skins/creator/<creatorid>`
!!!
Skin must be in the game in order to use `Get skins by creator`. 
!!!

Examples
`https://apibeta.deeeep.io/skins/11829`
`https://apibeta.deeeep.io/skins?animalId=7`
`https://apibeta.deeeep.io/skins/creator/546829`

## socialNetworks
- `<userid>` — ID of user. Username doesn't work.

Get socialNetworks by ID
`https://apibeta.deeeep.io/socialNetworks/<userid>`

Examples
`https://apibeta.deeeep.io/socialNetworks/5`

## twitch
Get current Deeeep.io Twitch streams
`https://apibeta.deeeep.io/twitch?new`

## users
- `<userid>` — ID of user. Username doesn't work. 
- `<userid>` — Username of user. ID doesn't work. 
- `[ref]` — Can only be `profile`. Will show profile view counts.

Get user by ID
`https://apibeta.deeeep.io/users/<userid>[ref]`

Get user by username
`https://apibeta.deeeep.io/users/u/<username>[ref]`

Examples
`https://apibeta.deeeep.io/users/5`
`https://apibeta.deeeep.io/users/u/ItsGrandPi?ref=profile`

## userStats
- `<userid>` — ID of user. Username doesn't work.

Get userStats by ID
`https://apibeta.deeeep.io/userStats/<userid>`

Examples
`https://apibeta.deeeep.io/userStats/5`

## videos
Get the most recent Deeeep.io YouTube videos
`https://apibeta.deeeep.io/videos`