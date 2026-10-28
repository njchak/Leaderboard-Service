# Leaderboard Service

This is a backend Leaderboard service that tracks players' score and rank. A player contains a name and score, and the service also returns rankings of top players.

## Quick start

**Requirements:** 
- Go 1.27
- *Optional*: Docker

**Run locally**  
`go run .` (Does not include any data)  
`go run . -seed` (Includes seeded data)  

**Run with Docker**  
`docker build -t leaderboard .`  
`docker run --rm -p 8080:8080 leaderboard`  
`docker run --rm -p 8080:8080 leaderboard --seed`  

The server listens on `localhost:8080` by default. Set `LISTEN_ADDR` to change it.  

## API

### POST /addToScore
Given a name and score in the request body, either add the score to the already existing player, or if player does not exist add them with the given score.  

**Request body example:**
```
{
  "name": "Player400",
  "score": 1000,
}
```
Cannot have a zero or negative score, and cannot have a blank username.


### GET /rank?username=NAME
Returns the rank (as an integer) of the player with the name passed in the request. Example for `/rank?username=Player400` on a new leaderboard would be `1`  

Can

### GET /leaderboard?n=N
Returns the top N players on the leaderboard. N must be greater or equal to 1, and if less than N players exist on the leaderboard, all players will be returned.  

**Example output for /leaderboard?n=5:**  
```
[
    {
        "name": "TheKing",
        "score": 20000,
        "rank": 1
    },
    {
        "name": "Billy",
        "score": 2000,
        "rank": 2
    },
    {
        "name": "BillyB",
        "score": 2000,
        "rank": 2
    },
    {
        "name": "player5",
        "score": 100,
        "rank": 4
    },
    {
        "name": "player1",
        "score": 64,
        "rank": 5
    }
]
```

