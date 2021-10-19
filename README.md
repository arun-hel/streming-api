## Obtain JWT 

`POST /auth/login`

### Data required:

```json
    {
        "username": "username@example.com",
        "password": "password"
    }
```

### Sample code
```javascript
const axios = require("axios")
let jwtToken = "" 

async function getToken(){
    const data = {
        "username": "username@example.com",
        "password": "password"
    }

    const response = await axios.post("https://stream.classplusplus.com/auth/login", data)

    //we need to include this token  as Bearer token for all the other calls
    jwtToken = response.data.access_token
}
getToken()

// set Authorization to all api calls
axios.defaults.headers.common = {'Authorization': `Bearer ${jwtToken}`}

```

## Start Streaming 
Start Streaming Instance

`POST /instances`

Start Streaming

`PATCH /instances/start/:name`
### Data required: 
Note: JWT Token needs to be included as Bearer Token.
```json
{
    "name": "uniqueName",
    "bbbUrl":"https://your.bbburl.com/bigbluebutton/",
    "bbbSecret":"bbbSecret",
    "meetingId":"mettingId",
    "meetingPassword":"meetingPassword", 
    "rtmpUrl":"rtmp://a.rtmp.youtube.com/live2/yourStreamingKey",
    "isThirdParty": true
}
```
### Sample code
```javascript

const data = {
    "name": "uniqueName",
    "bbbUrl":"https://your.bbburl.com/bigbluebutton/",
    "bbbSecret":"bbbSecret",
    "meetingId":"mettingId",
    "meetingPassword":"meetingPassword", 
    "rtmpUrl":"rtmp://a.rtmp.youtube.com/live2/yourStreamingKey",
    "isThirdParty": true
}
async function startStreaming(){

    // start Streaming Instance.
    await axios.post("https://stream.classplusplus.com/instances", data)

    // once Streaming Instance is started then Start Streaming.
    await axios.patch(`https://stream.classplusplus.com/instances/start/${data.name}`)

}
startStreaming()

```

### Stop Streaming

`PATCH /instances/:name`

### Data required: `name`

Note: JWT Token needs to be included as Bearer Token.

### Sample code
```javascript
async function stopStreaming(){
    // stop Streaming.
    await axios.patch(`https://stream.classplusplus.com/instances/stop/${name}`)
}
stopStreaming()

```









