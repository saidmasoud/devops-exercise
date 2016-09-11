# Data Service

This service provides the ability to put and get `accounts` to the MongoDB database. It requires authentication
`tokens` from the Auth Service.

You must have a valid `token` and `user` in the Auth Service before using this service. User creation outside the scope of this service. You must create users manually or through some other application.

## Dependencies
This service requires a valid MongoDB connection string provided in an environment var:

```
export MONGODB=mongodb://<user>:<pass>@<host>:<port>/
```

Refer to the [MongoDB Documentation](https://docs.mongodb.com/manual/reference/connection-string/) for more.

### Data Model

This service assumes usage both the `auth` (see Auth Service) and `data` databases
in MongoDB. It assumes the `accounts` collection exists and reads/writes records to it.

Tokens and users are out of scope. See the Auth Service.

#### accounts

Example model:
```
{
  "employees": 12,
  "_id": {
    "$oid": "57d3013be3174f735d857c4f"
  },
  "valuation": 100,
  "name": "helloworld"
},
```

## Usage

### `/accounts`

Supported methods: `GET`, `POST`

#### `GET`

Headers: `token=<auth_token>`
Returns: `200` and array of `account` objects or `401` if not authorized.
```
[{
  "employees": 12,
  "_id": {
    "$oid": "57d3013be3174f735d857c4f"
  },
  "valuation": 100,
  "name": "helloworld"
}]
```

Example:

```
GET http://localhost:5000/accounts

HEADERS
token=12398472895nfewnrfjkwerfn203r2h4895ry3y498th3843t04
```

#### `POST`

Parameters:
- `name` - string name of `account`.
- `valuation` - numeric valuation of the account
- `employees` - numeric value of employees at the company.
Returns: `201` if created. `401` if not authorized.

Example:

```
POST http://localhost:5000/accounts?name=google&valuation=9999999&employees=3000

HEADERS
token=12398472895nfewnrfjkwerfn203r2h4895ry3y498th3843t04
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
