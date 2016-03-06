Musiqpad Client API Functions
=======

To Do :- Add Description

*Current version: 0.5 Beta*

## Table Of Contents

### Musiqpad Client API Functions
- [API.room](#apiroom)
- [API.queue](#apiqueue)
- [API.chat](#apichat)
- [API.playlist](#apiplaylist)
- [API.player](#apiplayer)
- [Other Functions & Events](#other-api-functions)

### Musiqpad Client API Objects
- [Media](#media)
- [User](#user)
- [Role](#role)

### Musiqpad Client Data Api
- [PLAYER](#player)
- [USER](#user-1)
- [CHAT](#chat)
- [EVENTS](#events)


This is a list of all the public functions available in the API.

## API.room

### getInfo

Retrieve general information about the pad.

Parameters:

  * callback | optional
    * If provided will return the data from a new socket request.
	* Otherwise will return the data that the client currently has.

``` javascript
API.room.getInfo(function (data) {
  // doSomething();
});
```

### getUser

Retrieve a user in the pad.

Returns a [user] object.

Parameters:

  * user_id | integer | optional
    * Will pass back the current logged in users information if this parameter is not provided.
  * callback | function | optional
    * If provided will return the data from a new socket request.
	* Otherwise will return the data that the client currently has.

``` javascript
API.room.getUser(123, function (data) {
  // doSomething();
});
```

### getUsers

Retrieve the current users in the pad.

Returns array of [user] objects.

Parameters:

  * is_array | boolean | optional
    * Defaults to false if not provided.
	* If is_array is set to true then the users will be returned in the format `[{user_object}]`
	* If is_array is set to false then the users will be returned in the format `{user_id:{user_object}}`

``` javascript
API.room.getUsers(true);
```

### getStaff

Retrieve a list of the pad staff.

Returns an array of staff [user] object.

Parameters:

  * callback | function | optional
    * If provided will return the data from a new socket request.
	* Otherwise will return the data that the client currently has.

``` javascript
API.room.getStaff(function (data) {
  // doSomething();
});
```

### getBannedUsers

Retrieve a list of banned users.

Returns an array of banned [user] object.

Parameters:

  * callback | function | optional
    * If provided will return the data from a new socket request.
	* Otherwise will return the data that the client currently has.

``` javascript
API.room.getBannedUsers(function (data) {
  // doSomething();
});
```

### getRoles

Retrieve the pads available roles.

Returns array of [role] objects.

Parameters:

  * is_array | boolean | optional
    * Defaults to false if not provided.
	* If is_array is set to true then the roles will be returned in the format `[{role_object}]`
	* If is_array is set to false then the roles will be returned in the format `{role_name:{role_object}}`

``` javascript
API.room.getRoles(true);
```

### getHistory

Retrieve the queue history.

Returns sorted array of [media] objects.

Parameters:

  * callback | function | optional
    * If provided will return the data from a new socket request.
	* Otherwise will return the data that the client currently has.

``` javascript
API.room.getHistory(function (data) {
  // doSomething();
});
```

### getMedia

Retrieve information about the current video.

Returns [media] object.

``` javascript
API.room.getMedia();
```

### getTimeElapsed

Retrieve the time elapsed of the current video.

Returns the time elapsed of the current song in seconds.

``` javascript
API.room.getTimeElapsed();
```

### getTimeRemaining

Retrieve the time remaining of the current video.

Returns the time remaining of the current song in seconds.

``` javascript
API.room.getTimeRemaining();
```

### banUser

Ban a user.

Parameters:

  * user_id | integer | mandatory
    * The id of the user whom you wish to ban.
  * duration | string | mandatory
    * The duration which you would like to ban for. Pre-defined durations are available in the [Data API].
  * reason | string | optional
    * The reason for the ban. This will be shown to the user who gets banned.
  * callback | function | optional
    * Returns once the action has been completed on the server.

``` javascript
API.room.banUser(123, API.DATA.USER.BAN.DAY.duration, 'Ban Reason', function (data) {
  // doSomething();
});
```

### unbanUser

Unban a user.

Parameters:

  * user_id | integer | mandatory
    * The id of the user whom you wish to unban.
  * callback | function | optional
    * Returns once the action has been completed on the server.

``` javascript
API.room.unbanUser(123, function (data) {
  // doSomething();
});
```

### setRole

Set a user's role.

Parameters:

  * user_id | integer | mandatory
    * The id of the user whom you wish to ban.
  * role | string | mandatory
    * The role to set the user to. Must match the role name from [API.room.getRoles].
  * callback | function | optional
    * Returns once the action has been completed on the server.

``` javascript
API.room.setRole(123, 'role name', function (data) {
  // doSomething();
});
```

## API.queue

### join

Join the queue.

Parameters:

  * callback | function | optional
    * Returns once the action has been completed on the server.

``` javascript
API.queue.join(function (data) {
  // doSomething();
});
```

### leave

Leave the queue.

Parameters:

  * callback | function | optional
    * Returns once the action has been completed on the server.

``` javascript
API.queue.leave(function (data) {
  // doSomething();
});
```

### modAddDJ

Add a user to the queue.

Parameters:

  * user_id | integer | mandatory
    * The id of the user whom you wish to add to the queue.
  * callback | function | optional
    * Returns once the action has been completed on the server.

``` javascript
API.queue.modAddDJ(123, function (data) {
  // doSomething();
});
```

### modRemoveDJ

Remove a user from the queue.

Parameters:

  * user_id | integer | mandatory
    * The id of the user whom you wish to remove from the queue.
  * callback | function | optional
    * Returns once the action has been completed on the server.

``` javascript
API.queue.modRemoveDJ(123, function (data) {
  // doSomething();
});
```

### modSwapDJ

Swap 2 users positions in the queue.

Parameters:

  * user_id_1 | integer | mandatory
    * The id of the user whom you wish to swap with user_id_2.
  * user_id_2 | integer | mandatory
    * The id of the user whom you wish to swap with user_id_1.
  * callback | function | optional
    * Returns once the action has been completed on the server.

``` javascript
API.queue.modSwapDJ(123, 321, function (data) {
  // doSomething();
});
```

### modMoveDJ

Move a user to a specified position in the queue.

Parameters:

  * user_id | integer | mandatory
    * The id of the user whom you wish to move.
  * position | integer | mandatory
    * The position you would like to move the user to.
  * callback | function | optional
    * Returns once the action has been completed on the server.

``` javascript
API.queue.modSwapDJ(123, 5, function (data) {
  // doSomething();
});
```

### skipDJ

Skip the current DJ. This may be used by a mod to skip the current song or by the user playing the song.

Parameters:

  * position | integer | optional
    * The position you would like to move the user to after being skipped.
    * Will 'Lock Skip' the user to the position specified.
  * callback | function | optional
    * Returns once the action has been completed on the server.

``` javascript
API.queue.skipDJ(5, function (data) {
  // doSomething();
});
```

### setLock

Set whether the queue is locked.

Parameters:

  * lock_status | boolean | optional
    * If specified will attempt to set the lock status.
    * If not specified will toggle the lock.
  * callback | function | optional
    * Returns once the action has been completed on the server.

``` javascript
API.queue.setLock(true, function (data) {
  // doSomething();
});
```

### setCycle

Set whether DJ's should be added back into the queue after they DJ.

Parameters:

  * cycle_status | boolean | optional
    * If specified will attempt to set the cycle.
    * If not specified will toggle the cycle.
  * callback | function | optional
    * Returns once the action has been completed on the server.

``` javascript
API.queue.setCycle(true, function (data) {
  // doSomething();
});
```

### getDJ

Retrieve the current dj's [user] object.

Returns the [user] object of the current DJ.

``` javascript
API.queue.getDJ();
```

### getDJs

Returns an array containing [user] objects of the queue.

``` javascript
API.queue.getDJs();
```

### getPosition

Retrieve the position of a user in the queue.

Returns an integer for the users position in the queue.

Parameters:

  * user_id | integer | optional
    * If specified will get the position of the provided user in the queue.
    * If not specified will get the position of the current user in the queue.

``` javascript
API.queue.getPosition(123);
```

## API.chat

### send

Send a chat message to everyone in the pad.

Parameters:

  * message | string | mandatory
    * The message to send.

``` javascript
API.chat.send('Message');
```

### log

Add a log message to the local chat window.

Parameters:

  * message | string | mandatory
    * Adds the message to the chat in the format of a log message.
  * message_title | string | optional
    * A title for the log message

``` javascript
API.chat.log('Message', 'Message Title');
```

### system

Add a system message to the local chat window.

Parameters:

  * message | string | mandatory
    * Adds the message to the chat in the format of a system message.

``` javascript
API.chat.system('Message');
```

### broadcast

Send a broadcast message to everyone in the pad.

Parameters:

  * message | string | mandatory
    * Sends a broadcast message to everyone in the pad.

``` javascript
API.chat.broadcast('Message');
```

### delete

Delete a chat message.

Parameters:

  * chat_id | integer | mandatory
    * Deletes the message with the provided chat id.

``` javascript
API.chat.delete(123);
```

## API.playlist

### get

Retrieve an existing playlist.

Parameters:

  * playlist_id | integer | optional
    * If provided returns the playlist associated with the id.
	* If not provided will return an array of all playlists for the current user.

``` javascript
API.playlist.get(1);
```

### create

Create a new playlist.

Parameters:

  * name | string | mandatory
    * The name for the playlist.
  * callback | function | optional
    * Returns once the action has been completed on the server.

``` javascript
API.playlist.create('Playlist Name', function(data) {
	// doSomething();
});
```

### delete

Delete a playlist.

Parameters:

  * playlist_id | integer | mandatory
    * The id of the playlist to delete.
  * callback | function | optional
    * Returns once the action has been completed on the server.

``` javascript
API.playlist.delete(1, function(data) {
	// doSomething();
});
```

### addSong

Add a song to a playlist.

Parameters:

  * playlist_id | integer | mandatory
    * The id of the playlist to add the song to.
  * youtube_id | string | mandatory
    * The id of the youtube video to add to the playlist.
  * position | integer | optional
    * The position in the playlist to add the song at.
  * callback | function | optional
    * Returns once the action has been completed on the server.

``` javascript
API.playlist.addSong(1, 'youtube_id', 1, function(data) {
	// doSomething();
});
```

### removeSong

Remove a song from a playlist.

Parameters:

  * playlist_id | integer | mandatory
    * The id of the playlist to remove the song from.
  * youtube_id | string | mandatory
    * The id of the youtube video to remove from the playlist.
  * callback | function | optional
    * Returns once the action has been completed on the server.

``` javascript
API.playlist.removeSong(1, 'youtube_id', function(data) {
	// doSomething();
});
```

### moveSong

Move a song to a specified position in a playlist.

Parameters:

  * playlist_id | integer | mandatory
    * The id of the playlist to move the song in.
  * youtube_id | string | mandatory
    * The id of the youtube video to move.
  * position | integer | optional
    * The position in the playlist to move the song to.
  * callback | function | optional
    * Returns once the action has been completed on the server.

``` javascript
API.playlist.moveSong(1, 'youtube_id', 1, function(data) {
	// doSomething();
});
```

### import

Import a YouTube playlist.

Parameters:

  * youtube_playlist_id | string | mandatory
    * The id of the YouTube playlist to import.
  * callback | function | optional
    * Returns once the action has been completed on the server.

``` javascript
API.playlist.moveSong('youtube_playlist_id', 'youtube_id', 1, function(data) {
	// doSomething();
});
```

### shuffle

Shuffle a playlist into a random order.

Parameters:

  * playlist_id | integer | optional
    * The id of the playlist to shuffle.
	* If no playlist_id is provided will shuffle the current active playlist.
  * callback | function | optional
    * Returns once the action has been completed on the server.

``` javascript
API.playlist.shuffle(1, function(data) {
	// doSomething();
});
```

## API.player

### setVolume

Set the volume to the specified value.

Parameters:

  * volume | int | mandatory
    * The volume to set. Must be between 0 and 100.

``` javascript
API.player.setVolume(50);
```

### setMute

Set whether the volume is muted or unmuted.

Parameters:

  * mute | boolean | mandatory
    * Sets whether the volume is muted.

``` javascript
API.player.setMute(true);
```

### refresh

Refresh the player.

``` javascript
API.player.refresh();
```

### snooze

Snooze the current song.

``` javascript
API.player.snooze();
```

## Other API Functions

### on

Subscribe to a socket event.

Returns integer (callback_id) which is unique per event.

Parameters:

  * event | string | mandatory
    * The event to subscribe to. Available events are located in the [Data API -> EVENTS]
  * callback | function | mandatory
	* The function to call when the event is fired.

``` javascript
API.player.on(API.DATA.EVENTS.EVENT, function(data) {
	// doSomething();
});
```

### off

Unsubscribe from a socket event.

Parameters:

  * event | string | mandatory
    * The event to unsubscribe from. Available events are located in the [Data API -> EVENTS]
  * callback_id | integer | mandatory
    * The unique id for the callback in the event that you want to unsubscribe from. This is the id returned from the `API.on` function.

``` javascript
API.player.off(API.DATA.EVENTS.EVENT, 1);
```

### fullscreen

Toggles Fullscreen

``` javascript
API.player.fullscreen();
```

Musiqpad Client API Objects
=======

## Media

``` javascript
{
	cid: 'The YouTube Video ID',
	title: 'The title of the Video',
	duration: 0
}
```

## User

``` javascript
{
	banned: false,
	role: 'default',
	uid: 123,
	un: 'Username'
}
```

## Role

``` javascript
{
	canGrantRoles: [], // The roles this user can grant
	permissions: [], // Permissions granted by having this user role.
	showtitle: true, // If true the title will be shown on the userlist.
	style: {
		color: '#c4a8d6' // Any styles that are applied to a user with this role.
	}, 
	title: 'Artist/DJ' // The title of the role.
}
```

Musiqpad Client Data API
=======

The Data API is available at API.DATA and contains the following objects:

## PLAYER
### QUALITY
  * HD2160
  * HD1440
  * HD1080
  * HD720
  * LQ480
  * MQ360
  * SQ240
  * TQ144
  * AUTO

## USER

### BAN

  * MIN5:
    * text: '5 minutes'
	* duration: 'PT5M'
  * MIN30:
    * text: '30 minutes'
	* duration: 'PT30M'
  * HOUR:
    * text: '1 hour'
	* duration: 'PT1H'
  * HOUR12:
    * text: '12 hours'
	* duration: 'PT12H'
  * DAY:
    * text: '1 day'
	* duration: 'P1DT'
  * DAY10:
    * text: '10 days'
	* duration: 'P10DT'
  * DAY30:
    * text: '30 days'
	* duration: 'P30DT'
  * PERMA:
    * text: 'Permanent'
	* duration: 'P100YT'
	
## CHAT

### TSFORMAT

  * HR12
  * HR24
  
## EVENTS

### ADVANCE

``` javascript
{
  type: 'advance',
  data: {
    last: {
      song: {
        cid: '',
        title: '',
        duration: 0
      },
      uid: 123,
      start: 1456909101882
    },
    next: {
      song: {
        cid: '',
        title: '',
        duration: 0
      },
      uid: 123,
      start: 1456909347005
    }
  }
}
```

### CHAT

``` javascript
{
  type: 'chat',
  data: {
    uid: 123,
    message: '',
    time: 1456936308972,
    cid: 420
  }
}
```

### DELETE_CHAT

``` javascript
{
  type: 'deleteChat',
  data: {
    cid: 420,
    mid: 123
  }
}
```

### DJ_QUEUE_CYCLE

``` javascript
{
  type: 'djQueueCycle',
  data: {
    mid: 123,
    state: true
  }
}
```

### DJ_QUEUE_LOCK

``` javascript
{
  type: 'djQueueLock',
  data: {
    mid: 123,
    state: true
  }
}
```

### DJ_QUEUE_SKIP

``` javascript
{
  type: 'djQueueSkip',
  data: {
    uid: 123
  }
}
```

### DJ_QUEUE_MOD_SKIP

``` javascript
{
  type: 'djQueueModSkip',
  data: {
    mid: 123
  }
}
```

### DJ_QUEUE_MOVE

``` javascript
{
  type: 'djQueueModMove',
  data: {
    queueList: [123,321],
    uid: 123,
    from: 1,
    to: 0,
    mid: 123
  }
}
```

### DJ_QUEUE_SWAP

``` javascript
{
  type: 'djQueueModSwap',
  data: {
    queueList: [321,123],
    uid1: 123,
    uid2: 321,
    pos1: 0,
    pos2: 1,
    mid: 123
  }
}
```

### DJ_QUEUE_ADD

``` javascript
{
  type: 'djQueueModAdd',
  data: {
    mid: 123,
    uid: 123
  }
}
```

### DJ_QUEUE_REMOVE

``` javascript
{
  type: 'djQueueModRemove',
  data: {
    mid: 123,
    uid: 123
  }
}
```

### DJ_QUEUE_LIMIT

``` javascript

```

### USER_JOINED

``` javascript
{
  type: 'userJoined',
  data: {
    user: {
      badge: {
        top: '#003cff',
        bottom: '#ffffff'
      },
      banned: false,
      role: 'default',
      un: 'Username',
      uid: 1
    },
    guests: 5
  }
}
```

### USER_JOINED_QUEUE

``` javascript
{
  type: 'userJoinedQueue',
  data: {
  	queueList: [123,321,456,654]
  }
}
```

### USER_LEFT

``` javascript
{
  type: 'userLeft',
  data: {
    user: {
      badge: {
        top: '#003cff',
        bottom: '#ffffff'
      },
      banned: false,
      role: 'default',
      un: 'Username',
      uid: 1
    },
    guests: 5
  }
}
```

### USER_LEFT_QUEUE

``` javascript
{
  type: 'userLeftQueue',
  data: {
  	queueList: [123,321,456,654]
  }
}
```

### USER_UPDATE

``` javascript
{
  type: 'userUpdate',
  data: {
    user: {
      badge: {
        top: '#003cff',
        bottom: '#ffffff'
      },
      banned: false,
      role: 'default',
      un: 'Username',
      uid: 1
    }
  }
}
```

### USER_BANNED

``` javascript
{
  type: 'userBanned',
  data: {
    uid: 321,
    bannedBy: 123
  }
}
```

### USER_UNBANNED

``` javascript
{
  type: 'userUnbanned',
  data: {
    uid: 321,
    unbannedBy: 123
  }
}
```

### USER_ROLE_CHANGE

``` javascript
{
  type: 'moderateSetRole',
  data: {
    mid: 123,
    uid: 321,
    role: 'supervisor'
  }
}
```

### VOTE_UPDATE

``` javascript
{
  type: 'voteUpdate',
  data: {
    votes: {
      like: 5,
      dislike: 0,
      grab: 0
    },
    action: 'like',
    voted: 1
  }
}
```

### SYSTEM_MESSAGE

``` javascript

```

### BROADCAST_MESSAGE

``` javascript
{
  type: 'broadcastMessage',
  data: 'Test Message'
}
```

### PRIVATE_MESSAGE

``` javascript
{
  type: 'privateMessage',
  data: {
    uid: 123,
    message: 'Test Message'
  }
}
```

### SERVER_RESPONSE

[API.room.getRoles]: #musiqpad-client-api-functions-apiroom-getroles
[media]: #musiqpad-client-api-objects-media
[user]: #musiqpad-client-api-objects-user
[role]: #musiqpad-client-api-objects-role
[Data API]: #musiqpad-client-data-api
[Data API -> EVENTS]: #musiqpad-client-data-api-events
