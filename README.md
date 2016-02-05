Frontend test v2
===========
You should create simple web chat application. All data needed to complete this goal is presented in the current repository.

Task description
-------------------
This task is all about creating a simple web chat application, which is supports creating
rooms and exchanging messages.

## Task

- User should be able to pick up his username when he is connecting to the chat
- Username should be unique
- User should see available rooms, can switch them, can create and delete own rooms
- User should see other users in room
- If user deleted own room, other users which were in this room should be redirected to default room
- When user is connected in some room, last few messages from room should be showed
- User can write and edit/delete own messages
- If app lose connection, it should try to reconnect. After reconnecting it should automatically switch to room
user was connected


## Frontend

- Highlight current user name in chat on new message (@username)
- Application should be responsible
- SCSS/SASS should be used
- HTML5 doctype should be used

## Other
- All sources should be committed to public source repository, such as: http://github.com, http://bitbucket.org, etc
- Feel free to use 3rd party libraries and frameworks (like jQuery, backbone, sass etc...)

Additional plus
-----------------
- Using any of module loader (e.g. require.js)
- Using Task Runner (e.g. Gulp) for concatenation, minifying etc
- **Using your own backend**. If you dare, the requirements for it should be just the same as for the task.

API
-----------------
Address: http://

## Data Types
* **User**
    * **name**: String
    * **created**: Date
* **Room**
    * **name**: String
    * **created**: Date
    * **user**: User
    * **default**: Boolean
* **Message**
    * **content**: String
    * **created**: Date
    * **user**: User
    * **room**: Room

## Socket queries:
* **login** ( { username: String } )
    * Sends **user joined** to already logged in users
    * Sends **setup** to you
    * *Throws **appError** - wrong username, username already logged in*
* **new room** ( { name: String } )
    * Sends **room created** to users
    * *Throws **appError** - wrong room name or already exists*
* **edit room** ( { room: Room, remove: Boolean } )
    * Sends **room updated** or **room removed**
    * *Throws **appError** - wrong room names, room not found or room isn't yours*
* **switch room** ( { room: Room } )
* **new message** ( { message: String } )
    * *Throws **appError** - no message*
* **edit message** ( { id: String, message: String, remove: Boolean } )
    * Sends **message updated** or **message removed**
    * *Throws **appError** - no message*

## Socket events:
* **appError** *[@you]* ( { message: String } )
* **setup** *[@you]* ( { rooms: [Room], users: [User], messages: [Message] } )
* **room created** *[@wide]* ( Room )
* **room updated** *[@wide]* ( Room )
* **room removed** *[@wide]* ( Room )
* **user joined** *[@room]* ( [User] )
* **user left** *[@room]* ( [User] )
* **room switched** *[@you]* ( { messages: [Message], users: [User] } )
* **message created** *[@room]* ( Message )
* **message updated** *[@room]* ( Message )
* **message removed** *[@room]* ( Message )