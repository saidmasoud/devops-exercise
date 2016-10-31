# Auth Service

This service vends authentication `tokens` to valid `users` that have `key`s and
`secret`s. The `tokens` vended are used to access `data_service`.

## Dependencies
This service requires a valid MongoDB connection string provided in an environment var:

```
export MONGODB=mongodb://<user>:<pass>@<host>:<port>/
```

Refer to the [MongoDB Documentation](https://docs.mongodb.com/manual/reference/connection-string/) for more.

### Data Model

This service assumes usage of a top-level database called `auth` and two collections
inside it called `users` and `tokens`. The databases and collections are accessed lazily.

User creation outside the scope of this service. You must create users via code or a MongoDB Desktop Client.

#### users

Example model:
```
{
  "email": "something@somewhere.com"
  "key": "abc1234567890"
  "secret": "mnb0987654321"
}
```

#### tokens

Tokens are created when an authenticated user calls `GET /token` and returned in the JSON response.

```
{
  "token": <random sha256 utf-8 string>
}
```

## Usage

### `/token`

Supported methods: `GET`
Parameters:
- `key` - string access key for user.
- `secret` - string secret access key for user.
Returns: `201`

```
{
  "token": "string"
}
```

Example:

```
GET http://localhost:5000/token?key=myaccesskey123&secret=mysecret123
```

### `/health`

Supported methods: `GET`
Returns: `201` and JSON as long as the service is up.

## Running

This app runs on Python 3.5. Make sure you have Python and Virtual envionment tools.

```
# Ensure you have set `MONGODB` in some manner (see above).
virtualenv -p python3 env
source env/bin/activate.sh
pip install -r requirements.txt
python api.py
```
