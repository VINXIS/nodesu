nodesu!
======

An API wrapper for the [osu! api](https://github.com/ppy/osu-api/wiki), written for and in [node.js](https://nodejs.org/).
(node + osu = nodesu!)

## Setup for your project
```
# In your project directory
$ npm install --save nicholastay/nodesu
```

## Documentation / Usage
More information on API returns and how some parameters work can be found at the [official osu! API GitHub wiki page](https://github.com/ppy/osu-api/wiki). 
### Main functions
(Any function not stated as optional should be required)
#### new OsuApi()
```javascript
var OsuApi = require('nodesu');

var osu = new OsuApi({
  apiKey: 'your_key_here'
});
```
Get started by requiring the module and defining your API key.

#### raw
```javascript
osu.raw(endpoint, params, callback);
```
Sends a request to the osu! API with your parameters
* `endpoint`: A string containing the endpoint, e.g. `'/get_user'`
* `params`: An object containing the parameters to be passed, e.g. `{u: 'Nexerq', m: '0'} // which turns into ?u=Nexerq&m=0`
* `callback`: A function to be used as a callback.

A further example can be found in `examples/raw_request.js`.

#### getBeatmaps
```javascript
osu.getBeatmaps(object, mode, callback);
```
The callback returns with a error parameter and a response parameter. Upon a successful response, it should return with an array of beatmaps.
* `object`: An object, that can be easily constructed with the `beatmap` helper function (discussed below).
* `mode`: (optional, if so use `osu.mode.all`) A string, that can be easily constructed with thhe `mode` helper function.
* `callback`: A function to be used as a callback.

A further example can be found in `examples/beatmap_request.js`.

#### getScores
```javascript
osu.getScores(beatmap_object, user_object, mode, callback);
```
The callback returns with a error parameter and a response parameter. Upon a successful response, it should return with an array of scores for the chosen beatmap.
* `beatmap_object`: A object, that can be easily constructed with the `beatmap` helper function. Only `.byMapID` can be used as this API call can only take beatmap IDs.
* `user_object`: (optional, if so use `osu.user.all`) A object, that can be easily constructed with the `user` helper function.
* `mode`: (optional, if so use `osu.mode.all`) A string, that can be again easily constructed with a helper function.
* `callback`: A function to be used as a callback.

A further example can be found in `examples/beatmap_request.js`.

#### getUser
```javascript
osu.getUser(object, callback);
```
The callback returns with a error parameter and a response parameter. Upon a successful response, it should return with an object of the user.
* `object`: An object, that can be easily constructed with the `user` convenience function (discussed below).
* `callback`: A function to be used as a callback.

A further example can be found in `examples/user_request.js`.

#### getUserBest
```javascript
osu.getUserBest(object, mode, callback);
```
The callback returns with a error parameter and a response parameter. Upon a successful response, it should return with an array of beatmaps containing the user's best scores.
* `object`: An object, that can be easily constructed with the `user` helper function (discussed below).
* `mode`: (optional, if so use `osu.mode.all`) A string, that can be easily constructed with thhe `mode` helper function.
* `callback`: A function to be used as a callback.

A further example can be found in `examples/user_request.js`.

#### getUserRecent
```javascript
osu.getUserBest(object, mode, callback);
```
The callback returns with a error parameter and a response parameter. Upon a successful response, it should return with an array of beatmaps containing the user's most recent scores. It may throw an error if there are no scores in there, as they may not have played recently.
* `object`: An object, that can be easily constructed with the `user` helper function (discussed below).
* `mode`: (optional, if so use `osu.mode.all`) A string, that can be easily constructed with thhe `mode` helper function.
* `callback`: A function to be used as a callback.

A further example can be found in `examples/user_request.js`.

#### getMatch
```javascript
osu.getUserBest(id, callback);
```
The callback returns with a error parameter and a response parameter. Upon a successful response, it should return with an array with a multiplayer match's data.
* `id`: The multiplayer match ID (can be expressed in integer or string)
* `callback`: A function to be used as a callback.

#### getReplay
```javascript
osu.getScores(beatmap_object, user_object, mode, callback);
```
The callback returns with a error parameter and a response parameter. Upon a successful response, it should return with the replay data encoded in base64 by the server.
* `beatmap_object`: A object, that can be easily constructed with the `beatmap` helper function. Only a beatmap ID can be used.
* `user_object`: A object, that can be easily constructed with the `user` helper function.
* `mode`: A string, that can be again easily constructed with the `mode` helper function.
* `callback`: A function to be used as a callback.


### Some helper convenience/readability functions/variables
#### beatmap
```javascript
osu.beatmap.*(id, limit)
```
The * can be replaced with:
* `byMapset`: lookup beatmap by mapset
* `byMapID`: lookup beatmap by beatmap ID
* `byUserID`: lookup beatmap by user ID
* `byUsername`: lookup beatmap by username
* `byHash`: lookup beatmap by hash (refer to the API wiki for details)
* `byLetter`: lookup beatmap by letter (s, b) (any letter the API can take for a beatmap)

The other variables:
* `id`: An integer or string, that corresponds to the ID of the map/mapset or it can be a username/userid/hash
* `limit`: (optional) Limit the beatmaps that are returned


#### score
```javascript
osu.score.all
```
This just returns `null`, which can be used to return all scores when using `getScores`. It is just a convenience and ease of reading function. Refer to `examples/scores_request.js` for a better indication.


### user
```javascript
osu.user.*(id, data)
```
The `*` can be replaced with:
* `byUserID`: lookup user by user ID
* `byUsername`: lookup user by username
* `all`: returns `null` for `getScores` convenience

The other variables
* `id`: An integer or string that is the user ID/username
* `data`: For `getUser` this is the `event_days` parameter, and this limits the number of days events are grabbed. For any other function this is the `limit` parameter, and this basically limits how many results are returned. (more info on the official wiki)


### mode
```javascript
osu.mode.*
```
The `*` can be replaced with (most are self-explanatory):
* `standard`
* `taiko`
* `ctb`
* `mania`
* `all`
* `default`
This is just for convenience instead of knowing the numbers, as well as for readability. `all` and `default` both return `null`, refer to examples or the module itself to understand usage better.



## Contributing / Setup for development
To contribute, you should fork this project then I will review and accept as required pull requests.
```
# Fork the project first
$ git clone https://github.com/_name_/nodesu.git && cd nodesu
$ npm install
# Then shoot the PR through if you work on it and do something cool!
```
