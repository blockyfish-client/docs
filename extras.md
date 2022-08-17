---
icon: gift
title: Extras
order: 996
image: https://raw.githubusercontent.com/blockyfish-client/Assets/main/blockyfishclientbanner.png
---
# Extra stuff
Extra things not related to Blockyfish Client but related to Deeeep.io in general. 

## Mapmaker
Deeeep.io Mapmaker can be found [here](https://mapmaker.deeeep.io)

### Image Tracing
Useful for making Mapmaker Arts based on existing image. 
Change the width, top, and left value according to your needs
```html
<div class="overlay" style="opacity: 0.5;position: absolute;width: 800px;top: 125px;left: 475px;pointer-events: none;">
        <img src="YOUR IMAGE URL">
</div>
```

## API
!!! Note
Not all available API links maybe listed. 
!!!

Terminology:
Required perimeter `<>`
Optional perimeter `[]`

### animals
- `<name_or_id>` — Animal ID or name, value between `0` to `120`. 

Get animal by ID or name
`https://apibeta.deeeep.io/animals/<name_or_id>`

Examples
`https://apibeta.deeeep.io/animals/fish`
`https://apibeta.deeeep.io/animals/0`

### maps
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

Find a map by creator
`https://apibeta.deeeep.io/maps/u/<userid>[page][count][orderBy][period][direction]`

Examples
`https://apibeta.deeeep.io/maps/4643`
`https://apibeta.deeeep.io/maps/s/fishy_ffa`
`https://apibeta.deeeep.io/maps/u/644652?page=1&count=1&orderBy=updated_at&direction=ASC`

### playHistories
- `<userid>` — ID of user. Username doesn't work. 
- `[gmId]` — Gamemode ID, from `1` to `6`. 
- `[animalId]` — Animal ID, `0` to `120`. 
- `[order]` — `score` or `latest`


Get a player's play history
`https://apibeta.deeeep.io/playHistories/u/<userid>[gmId][animalId][order]`

Examples
`https://apibeta.deeeep.io/playHistories/u/5?gmId=1&animalId=1&order=score`
`https://apibeta.deeeep.io/playHistories/u/5?gmId=6&order=latest`

### skins
- `<skinid>` — ID of skin, should be a number. 
- `<creatorid>` — ID of skin creator

Get a skin by ID
`https://apibeta.deeeep.io/skins/<skinid>`

Get skins by creator
`https://apibeta.deeeep.io/skins/creator/<creatorid>`
!!!
Skin must be in the game in order to use `Get skins by creator`. 
!!!

Examples
`https://apibeta.deeeep.io/skins/11829`
`https://apibeta.deeeep.io/skins/creator/546829`

### users
- `<userid>` — ID of user. Username doesn't work. 
- `<userid>` — Username of user. ID doesn't work. 
- `[ref]` — can only be `profile`

Get user by ID
`https://apibeta.deeeep.io/users/<userid>[ref]`

Get user by username
`https://apibeta.deeeep.io/users/u/<username>[ref]`

Examples
`https://apibeta.deeeep.io/users/5`
`https://apibeta.deeeep.io/users/u/ItsGrandPi?ref=profile`

### userStats
- `<userid>` — ID of user. Username doesn't work.

Get userstats by ID
`https://apibeta.deeeep.io/userStats/<userid>`

Examples
`https://apibeta.deeeep.io/userStats/5`