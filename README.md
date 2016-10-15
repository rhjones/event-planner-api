# Event Planner API

## API

Scripts are included in [`scripts`](scripts) to test actions.

### Authentication

| Verb   | URI Pattern            | Controller#Action |
|--------|------------------------|-------------------|
| POST   | `/sign-up`             | `users#signup`    |
| POST   | `/sign-in`             | `users#signin`    |
| PATCH  | `/change-password/:id` | `users#changepw`  |
| DELETE | `/sign-out/:id`        | `users#signout`   |

#### POST /sign-up

Request:

```sh
curl --include --request POST http://localhost:3000/sign-up \
  --header "Content-Type: application/json" \
  --data '{
    "credentials": {
      "email": "an@example.email",
      "username" : "Robin",
      "password": "an example password",
      "password_confirmation": "an example password"
    }
  }'
```

```sh
scripts/sign-up.sh
```

Response:

```md
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{
  "user": {
    "__v": 0,
    "updatedAt": "2016-10-15T18:37:02.637Z",
    "createdAt": "2016-10-15T18:37:02.637Z",
    "email":"an@example.email", 
    "username":"Robin", 
    "_id":"1"
  }
}
```

#### POST /sign-in

Request:

```sh
curl --include --request POST http://localhost:3000/sign-in \
  --header "Content-Type: application/json" \
  --data '{
    "credentials": {
      "email": "an@example.email",
      "password": "an example password"
    }
  }'
```

```sh
scripts/sign-in.sh
```

Response:

```md
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{
  "user": {
    "_id": "1",
    "updatedAt": "2016-10-15T18:38:40.496Z",
    "createdAt": "2016-10-15T18:37:02.637Z",
    "email": "an@example.email",
    "username": "Robin",
    "token": "33ad6372f795694b333ec5f329ebeaaa",
    "__v": 0
  }
}
```

#### PATCH /change-password/:id

Request:

```sh
curl --include --request PATCH http://localhost:3000/change-password/$ID \
  --header "Authorization: Token token=$TOKEN" \
  --header "Content-Type: application/json" \
  --data '{
    "passwords": {
      "old": "an example password",
      "new": "super sekrit"
    }
  }'
```

```sh
ID=1 TOKEN=33ad6372f795694b333ec5f329ebeaaa scripts/change-password.sh
```

Response:

```md
HTTP/1.1 200 OK
```

#### DELETE /sign-out/:id

Request:

```sh
curl --include --request DELETE http://localhost:3000/sign-out/$ID \
  --header "Authorization: Token token=$TOKEN"
```

```sh
ID=1 TOKEN=33ad6372f795694b333ec5f329ebeaaa scripts/sign-out.sh
```

Response:

```md
HTTP/1.1 200 OK
```

### Users

| Verb | URI Pattern | Controller#Action |
|------|-------------|-------------------|
| GET  | `/users`    | `users#index`     |
| GET  | `/users/1`  | `users#show`      |

#### GET /users

Request:

```sh
curl --include --request GET http://localhost:3000/users \
  --header "Authorization: Token token=$TOKEN"
```

```sh
TOKEN=33ad6372f795694b333ec5f329ebeaaa scripts/users.sh
```

Response:

```md
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{
  "users": [
    {
      "id": 2,
      "email": "another@example.email"
    },
    {
      "id": 1,
      "email": "an@example.email"
    }
  ]
}
```

#### GET /users/:id

Request:

```sh
curl --include --request GET http://localhost:3000/users/$ID \
  --header "Authorization: Token token=$TOKEN"
```

```sh
ID=2 TOKEN=33ad6372f795694b333ec5f329ebeaaa scripts/user.sh
```

Response:

```md
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{
  "user": {
    "id": 2,
    "email": "another@example.email"
  }
}
```

### Events

| Verb | URI Pattern | Controller#Action |
|------|-------------|-------------------|
| GET  | `/events`    | `events#index`     |
| GET  | `/events/1`  | `events#show`      |
| POST  | `/events`  | `events#create`      |
| PATCH  | `/events/1`  | `events#update`      |
| DELETE  | `/events/1`  | `events#destroy`      |

#### GET /events

Request:
```sh
curl --include --request GET http://localhost:3000/events \
  --header "Authorization: Token token=$TOKEN"
```

```sh
TOKEN=33ad6372f795694b333ec5f329ebeaaa scripts/event-index.sh
```

Response: 
```md
{
  "events": [
    {
      "_id": "580280b22b4c41285571bc2f",
      "updatedAt": "2016-10-15T19:28:38.885Z",
      "createdAt": "2016-10-15T19:17:06.555Z",
      "title": "Even Better Bagel Party",
      "location": "GA Boston",
      "date": "2016-10-16T00:00:00.000Z",
      "_owner": "5802774e25d55121d3948041",
      "__v": 0,
      "questions": [
        {
          "text": "Are you coming?",
          "options": ["Yes","No","Maybe"]
        }
      ],
      "id":"580280b22b4c41285571bc2f"
    },
    {
      "_id": "580280b22b4c41285571bc30",
      "updatedAt": "2016-10-16T19:28:38.885Z",
      "createdAt": "2016-10-16T19:17:06.555Z",
      "title": "Pizza Party",
      "location": "GA Boston",
      "date": "2016-10-31T00:00:00.000Z",
      "_owner": "5802774e25d55121d3948041",
      "__v": 0,
      "questions": [
        {
          "text": "Are you coming?",
          "options": ["Yes","No","Maybe"]
        }
      ],
      "id":"580280b22b4c41285571bc30"
    },
  ]
}
```

#### GET /events/:id

Request:
```sh
curl --include --request GET http://localhost:3000/events/$ID \
  --header "Authorization: Token token=$TOKEN"
``` 
```sh
ID=58 TOKEN=33ad6372f795694b333ec5f329ebeaaa scripts/event-show.sh
```

Response:
```md
{
  "event": {
    "_id": "580280b22b4c41285571bc2f",
    "updatedAt": "2016-10-15T19:28:38.885Z",
    "createdAt": "2016-10-15T19:17:06.555Z",
    "title": "Even Better Bagel Party",
    "location": "GA Boston",
    "date": "2016-10-16T00:00:00.000Z",
    "_owner": "5802774e25d55121d3948041",
    "__v": 0,
    "questions": [
      {
        "text": "Are you coming?",
        "options": ["Yes","No","Maybe"]
      }
    ],
    "id": "580280b22b4c41285571bc2f"
  }
}
```

#### POST /events

Request:
```sh
curl --include --request POST http://localhost:3000/events \
  --header "Content-Type: application/json" \
  --header "Authorization: Token token=$TOKEN" \
  --data '{
    "event": {
      "title": "Bagel Party",
      "location": "GA Boston",
      "date": "2016-10-15"
    }
  }'
```

```sh
TOKEN=33ad6372f795694b333ec5f329ebeaaa scripts/event-create.sh
```

Response from POST: 

```md
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{
  "event": {
    "__v": 0,
    "updatedAt": "2016-10-15T19:17:06.555Z",
    "createdAt": "2016-10-15T19:17:06.555Z",
    "title": "Bagel Party",
    "location": "GA Boston",
    "date": "2016-10-15T00:00:00.000Z",
    "_owner": "5802774e25d55121d3948041",
    "_id": "580280b22b4c41285571bc2f",
    "questions": [
      {
        "options": ["Yes","No","Maybe"],
        "text": "Are you coming?"
      }
    ],
    "id": "580280b22b4c41285571bc2f"
  }
}
```

#### PATCH /events/:id

Request:
```sh
curl --include --request PATCH http://localhost:3000/events/$ID \
  --header "Content-Type: application/json" \
  --header "Authorization: Token token=$TOKEN" \
  --data '{
    "event": {
      "title": "Even Better Bagel Party",
      "location": "GA Boston",
      "date": "2016-10-16"
    }
  }'
```

```sh
ID=58 TOKEN=33ad6372f795694b333ec5f329ebeaaa scripts/event-create.sh
```

Response:
```md
HTTP/1.1 200 OK
```

#### DELETE /events/:id

Request:
```sh 
curl --include --request DELETE http://localhost:3000/events/$ID \
  --header "Authorization: Token token=$TOKEN"
``` 

```sh
ID=58 TOKEN=33ad6372f795694b333ec5f329ebeaaa scripts/event-destroy.sh
```

Response: 
```md
HTTP/1.1 200 OK
```

## [License](LICENSE)

1.  All content is licensed under a CC­BY­NC­SA 4.0 license.
1.  All software code is licensed under GNU GPLv3.
