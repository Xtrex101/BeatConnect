# BeatConnect - Online Music Application


A full-stack online music app, developed using MERN stack (React, Express.js, MongoDB) and Electron. Libraries including Tailwind CSS, Redux, Socket.IO are adopted.

<p align="center">
    <img src="https://github.com/Xtrex101/BeatConnect/blob/main/github-assets/explore_page.png?raw=true" width="60%">
</p>

## Features

- :star: Favoriting music & Adding music to playlists (from context menu)

<p align="center">
    <img src="https://github.com/Xtrex101/BeatConnect/blob/main/github-assets/favorites.png?raw=true" width="60%">
</p>

- :speech_balloon: Sharing comments & Viewing others' comments of a track

<p align="center">
    <img src="https://github.com/Xtrex101/BeatConnect/blob/main/github-assets/music_comments.png?raw=true" height="auto" width="60%">
</p>

- :clipboard: Creating and managing playlists & Favoriting others' playlists

- :cloud: Personal music cloud drive

- :speaker: Posting thoughts with music & Viewing friends' posts

<p align="center">
    <img src="https://github.com/Xtrex101/BeatConnect/blob/main/github-assets/upload_posts.png" width="45%">
    <img src="https://github.com/Xtrex101/BeatConnect/blob/main/github-assets/friends_posts.png?raw=true" width="45%">
</p>

- :blush: Personal profile page, showing one's favorites, playlists and posts

<p align="center">
    <img src="https://github.com/Xtrex101/BeatConnect/blob/main/github-assets/personal_profile.png" height="auto" width="60%">
</p>

- :envelope: Personal messaging (Socket.IO)

<p align="center">
    <img src="https://github.com/Xtrex101/BeatConnect/blob/main/github-assets/personal_messaging.png?raw=true" height="auto" width="60%">
</p>

- :lock: User authentication with JWT

## How to Run

**Tools needed:** Node v20.13.1, npm 10.5.2, MongoDB (local or cloud like Atlas)

**Dependency Installation:** `npm install` for both the frontend and backend.

**Backend:**

Inside the backend directory, create a `.env` file specifying environment variables as below:

```env
PORT=""            # The port for backend
MONGO_URI=""       # MongoDB URI, local or cloud. E.g., "mongodb://localhost:27017/BeatConnect"
JWT_SECRET_KEY=""  # Secret key for JWT, which can be generated using `openssl rand -base64 64`
```

Run: `node app.js`

**Frontend:**

Inside the `.env.local` file, specify `VITE_SERVER_URL=` as the backend URL, *without a slash at the end*.
E.g., `"http://localhost:3000"`

Start React frontend: `npm run dev`

Start Electron client: `npm run electron:start`

## Miscellaneous

- Note that only admin can manage tracks. A user can be set as admin using mongosh:

    ```shell
    db.users.findOneAndUpdate({_id: ObjectId('xxx')}, {$set: {role: "admin"}})
    ```


- All the files are stored on the local file system, Cloud integration in remaning.

<details>

<summary><b>RESTful API Design</b></summary>

### Users

**GET /api/users/userId [?populate=]** - Get user info. `userId` can be `current`

**POST /api/users** - Register a new user

**PUT /api/users** - Update user info

**GET /api/users/:userId/following** - Get the user's following list. `userId` can be `current`

**POST/DELETE /api/users/:userId/follow** - Follow/Unfollow

### Playlists

**GET /api/playlists/:playlistId** - Get playlist info

**POST /api/playlists** - Create a new playlist

**PUT /api/playlists/:playlistId** - Update a playlist

**DELETE /api/playlists/:playlistId** - Remove a playlist

**POST /api/playlists/:playlistId/tracks body: trackId** - Add a track to a playlist

**DELETE /api/playlists/:playlistId/tracks/:trackId** - Remove a track from the playlist

**GET /api/users/:userId/playlists** - Get playlists created by the user. `userId` can be `current`

### Favorite playlists

**GET /api/users/:userId/favoritePlaylists** - Get a user’s favorite playlists

**POST/DELETE /api/playlists/:playlistId/favorite** - Favorite/Unfavorite a playlist

### Favorite tracks

**GET /api/users/:userId/favorites** - Get user’s favorite list. `userId` can be `current`

**POST/api/favorites body: trackId** - Favorite a track

**DELETE /api/favorites/:trackId** - Unfavorite a track

### Tracks

**GET /api/tracks/:trackId?** - Get info of a track

**POST /api/tracks body: trackId** - Upload a track. Requires admin privilege

**PUT /api/tracks/:trackId body: trackId** - Update a track. Requires admin privilege

**DELETE /api/tracks/:trackId** - Remove a track. Requires admin privilege

### Comments

**GET /api/tracks/:trackId/comments** - Get comments of a track

**POST /api/tracks/:trackId/comments** - Post a comment to a track

### Drive

**GET /api/drive** - Get tracks in the user's drive

**POST /api/drive** - Upload a track to the user's drive

**DELETE /api/drive/:trackId** - Remove a track from the user's drive

### Search

**GET /api/search ?q=** - Search for tracks and users

### Posts

**GET /api/posts** - Retrieve posts from followed users

**GET /api/users/:userId/posts** - Retrieve a user’s posts

**POST /api/posts body: postId** - Send a post

**DELETE /api/posts/:postId** - Remove a post

### Chat

**GET /api/messages** - Retrieve users that have had messages with current user (name, avatar)

**GET /api/messages/:partnerUserId** - Retrieve messages between the user and a partner

</details>
