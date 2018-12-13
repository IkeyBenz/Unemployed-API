# Unemployed API

> This API allows the front end of [Unemployed](https://unemployed.herokuapp.com) to create and authenticate users, and CRUD posts and comments.

----

Because the api and front end are hosted on the same server, all api endpoints need to be accessed from the /api/ route.

## Authentication

All requests that deal with authenticating and creating users can be accessed from the /api/auth/ route.

---
> POST: `/api/auth/signup/`

Requires:
```javascript
{ name: String, email: String,  password: String }
```

Modifies: Creates a new user with given credentials

Returns: A cookie containing a JWT token signed for the newly made user

>POST: `/api/auth/signin/`

Requires: 
```javascript
{ email: String, password: String }
```

Modifies: Nothing

Returns: A cookie containing a JWT token signed for the found user, or an error because the user couldn't be found.

>GET: `/api/auth/authenticatedUser/`

Requires: A cookie named UnToken containing a JWT token for a user

Modifies: Nothing

Returns: The user credentials found from decoding the recieved JWT token

>GET: `/api/auth/signout/`

Requires: Nothing

Modifies: Removes the UnToken Cookie from the requester

Returns: Nothing

## Posts
All requests dealing with the post resource can be accessed from /api/posts/.
The POST, PATCH, and DELETE requests require a cookie name UnToken that contains a JWT for a signed in user.

---

>POST: `/api/posts/`

Requires:  
```javascript
{ title: String, content: String, author: ObjectID }
```
Modifies: Creates a new post and adds it to the users posts array

Returns: An error or success message.

>GET: `/api/posts/:id`

Requires: The id parameter to be a valid post Id

Modifies: Nothing

Returns: The post document with the given Id

>PATCH: `/api/posts/:id`

### Requires: The parameters you wish to update in the post. Options include: 
```javascript
{ title: String, content: String }
```

Modifies: The post document with the given Id

Returns: An error or success message.

>DELETE: `/api/posts/:id`

Requires: The id parameter to be a valid post id

Modifies: Deletes the post document and removes the postId from the currently signed in user's posts array.

Returns: An error or success message.

## Comments
All requests dealing with the comments resource can be accessed from /api/comments/.
The POST, PATCH, and DELETE requests require a cookie name UnToken that contains a JWT for a signed in user.

---
>POST: `/api/comments/`

Requires: 
    
```javascript
{ content: String, postId: ObjectID, author: ObjectID }
```
Modifies: Creates a new comment, adds it to the users comments array, and adds it to the post's (from specified postId) comments array.

Returns: An error or success message.

>GET: `/api/comments/:id`

Requires: The id parameter to be a valid comment Id

Modifies: Nothing

Returns: The comment document with the given Id

>PATCH: `/api/comments/:id`

Requires: 
```javascript
{ content: String }
```

Modifies: The comment document with the given Id

Returns: An error or success message.

>DELETE: `/api/comments/:id`

Requires: The id parameter to be a valid comment id

Modifies: Deletes the comment document, removes the commentId from the currently signed in user's comments array, and removes the commentId from the post's (found from the comment's postId property) comments array.

Returns: An error or success message.