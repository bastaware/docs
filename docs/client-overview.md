# Overview

Colyseus currently have clients for the platforms:

- [HTML5](https://github.com/gamestdio/colyseus.js/)
- [Unity3D](https://github.com/gamestdio/colyseus-unity3d)
- [Defold](https://github.com/gamestdio/colyseus-defold)

Need a client for another platform? Share your interest on the [discussion board](https://discuss.colyseus.io/)!

## Connecting to the Server

```typescript fct_label="TypeScript"
import * as Colyseus from "colyseus.js";
// ...

let client = new Colyseus.Client("ws://localhost:2657");
```

```csharp fct_label="C#"
using Colyseus;
// ...

Client client = new Client("ws://localhost:2657");
```

```lua fct_label="lua"
local ColyseusClient = require("colyseus.client")
// ...

local client = ColyseusClient.new("ws://localhost:2657");
```

## Methods

### `join (roomName: string, options: any)`

```typescript fct_label="TypeScript"
let room = client.join("battle");
```

```csharp fct_label="C#"
Room room = client.Join("battle");
```

```lua fct_label="lua"
local room = client:join("battle")
```

### `rejoin (roomName: string, sessionId: string)`

Reconnects the client into a room he was previously connected with.

Must be used along with [`allowReconnection()`](api-room#allowreconnection-client-seconds) in the server-side.

```typescript fct_label="TypeScript"
let room = client.rejoin("battle", "SkNaHTazQ");
```

```csharp fct_label="C#"
Room room = client.ReJoin("battle", "SkNaHTazQ");
```

```lua fct_label="lua"
local room = client:rejoin("battle", "SkNaHTazQ")
```

### `getAvailableRooms (roomName: string)`

List all available rooms to connect with the provided `roomName`. Locked rooms
won't be listed.

```typescript fct_label="TypeScript"
client.getAvailableRooms("battle", function(rooms, err) {
  if (err) console.error(err);
  rooms.forEach(function(room) {
    console.log(room.roomId);
    console.log(room.clients);
    console.log(room.maxClients);
    console.log(room.metadata);
  });
});
```

```csharp fct_label="C#"
client.GetAvailableRooms("battle", (rooms: RoomsAvailable, err: ErrorEventArgs) => {
  rooms.
});
```

```lua fct_label="lua"
client:getAvailableRooms("battle", function(rooms, err)
  if (err) console.error(err);
  for i, rooms in pairs(rooms) do
    print(rooms[i].roomId)
    print(rooms[i].clients)
    print(rooms[i].maxClients)
    print(rooms[i].metadata)
  end
end);
```

### `close ()`

Close connection with the server.

```typescript fct_label="TypeScript"
client.close();
```

```csharp fct_label="C#"
client.Close();
```

```lua fct_label="lua"
client:close()
```

## Events

### `onOpen`

This event is triggered when the connection is accepted by the server.

```typescript fct_label="TypeScript"
client.onOpen.add(function() {
  console.log("connection is now open");
});
```

```csharp fct_label="C#"
client.OnOpen += (object sender, EventArgs e) => {
  Debug.Log ("connection is now open");
}
```

```lua fct_label="lua"
client:on('open', function()
  print("connection is now open")
end)
```

### `onClose`

This event is triggered when the connection is closed.

```typescript fct_label="TypeScript"
client.onClose.add(function() {
  console.log("connection has been closed");
});
```

```csharp fct_label="C#"
client.OnClose += (object sender, EventArgs e) => {
  Debug.Log ("connection has been closed");
}
```

```lua fct_label="lua"
client:on('close', function()
  print("connection has been closed")
end)
```

### `onError`

This event is triggered when some error occurs in the server.

```typescript fct_label="TypeScript"
client.onError.add(function(err) {
  console.log("something wrong happened", err);
});
```

```csharp fct_label="C#"
client.OnError += (object sender, EventArgs e) => {
  Debug.Log ("something wrong happened");
}
```

```lua fct_label="lua"
client:on("error", function()
  print("something wrong happened")
end)
```

<!-- TODO: document raw `onMessage` -->
<!-- ### `onMessage` -->

## Properties

### `id: string`

Unique identifier for the client.

!!! Note
    The same client id can connect into the same room handler when joining from multiple browser tabs.
