# FSND-capstone

## Getting Started

### Installing Dependencies

#### Python 3.8

Install the latest version of python at https://www.python.org/downloads/

#### Virtual Environment

Install, create, and activate a virtual environment at https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/

#### PIP Dependencies

Once the virtual environment is activated, run the command:

```bash
pip install -r requirements.txt
```

or 

```bash
pip3 install -r requirements.txt
```

This will install all the required packages to run this app.

## Running the server
#### Local development:
With postgresql set up, run the command:
```
createdb cast
```

Then, comment out this line which is located on line 7 in models.py:
```bash
database_path = os.environ.get("DATABASE_URL")
```
and uncomment this line, which is located on line 8 in models.py:
```bash
# database_path = "postgresql://{}/{}".format(':5433', database_name)
```

Then run:

```bash
source setup.sh
flask run
```
The endpoints can be accessed at this url: http://127.0.0.1:5000


#### Deployed server:

The endpoints can be accessed at this url: https://fsnd-cast-app.herokuapp.com

## API
```
Endpoints:

GET '/actors'
GET '/movies'
POST '/actors'
POST '/movies'
PATCH '/actors/id'
PATCH '/movies/id'
DELETE '/actors/id'
DELETE '/movies/id'

GET '/actors'
- Fetches a list called actors comprising of a dictionary for each actor
- Request arguments: None
Returns: A list of dictionaries called actors with each dictionary representing an actor in the database, a boolean called "success" indicating if the request was successful or not
{
  "actors": [
    {
      "age": age of the actor,
      "gender": gender of the actor,
      "id": id of the actor,
      "movies": list of movies the actor is in,
      "name": name of the actor
    },
    ...
   ],
   "success": true
}

GET '/movies'
- Fetches a list called movies comprising of a dictionary for each movie
- Request arguments: None
Returns: A list of dictionaries called movies with each dictionary representing a movie in the database, a boolean called "success" indicating if the request was successful or not
{
  "movies": [
    {
      "actors": list of actors the movie has,
      "id": id of the movie,
      "release_date": released date of the movie in YYYY-MM-DD 00:00:00 GMT format,
      "title": title of the movie
    },
    ...
   ],
   "success": true
}

POST '/actors'
- Create a new actor to be saved in the database
- Request arguments: age, gender, movies, name; name and age are required
Returns: a dictionary of the actor that was created, a boolean called "success" indicating if the request was successful or not
{
    "actor": {
      "name": name of the actor, 
      "age": age of the actor,
      "gender": gender of the actor,
      "movies": list of movie titles that the actor has been in
     },
     "success": true
}

POST '/movies'
- Create a new movie to be saved in the database
- Request arguments: title, release_date, actors; title and release_date are required
Returns: a dictionary of the movie that was created, a boolean called "success" indicating if the request was successful or not
{
  "movie": {
      "title": title of the movie,
      "release_date": released date of the movie in the YYYY-MM-DD format,
      "actors": list of actors' names that have been in the movie
   ,
  "success": true
}

PATCH '/actors/id'
- Modify the actor with the passed in id
- Request arguments: age, gender, movies, name; name and age are required
Returns: a dictionary of the actor that was modified, a boolean called "success" indicating if the request was successful or not
{
    "actor": {
      "name": name of the actor, 
      "age": age of the actor,
      "gender": gender of the actor,
      "movies": list of movie titles that the actor has been in
     },
     "success": true
}

PATCH '/movies/id'
- Modify the movie with the passed in id
- Request arguments: title, release_date, actors; title and release_date are required
Returns: a dictionary of the movie that was modified, a boolean called "success" indicating if the request was successful or not
{
  "movie": {
      "title": title of the movie,
      "release_date": released date of the movie in the YYYY-MM-DD format,
      "actors": list of actors' names that have been in the movie
   ,
  "success": true
}

DELETE '/actors/id'
- Delete the actor with the passed in id
- Request arguments: None
Returns: the id of the actor that was deleted, , a boolean called "success" indicating if the request was successful or not
{
  "id_deleted": if of the actor that was deleted,
  "success": true
}

DELETE '/movies/id'
- Delete the movie with the passed in id
- Request arguments: None
Returns: the id of the movie that was deleted, , a boolean called "success" indicating if the request was successful or not
{
  "id_deleted": if of the moviet that was deleted,
  "success": true
}
```

## Authentication Roles / RBAC
There are three roles that can interact with this application:
<ol>
<li>Casting Assistant</li>
  <ol><li>Can view actors and movies</li></ol>
<li>Casting Director</li>
  <ol><li>Can view actors and movies</li>
  <li>Can add or delete an actor</li>
  <li>Can modify actors or movies</li></ol>
<li>Executive Producer</li>
  <ol><li>Can view actors and movies</li>
  <li>Can add or delete an actor</li>
  <li>Can modify actors or movies</li>
  <li>Can add or delete a movie</li></ol>
</ol>

The JWT token required for each role can be found in setup.sh in between single quotes '' as:
- ASSISTANT for JWT of Casting Assistant
- DIRECTOR for JWT of Casting Director
- PRODUCER for JWT of Executive Producer

Use these tokens in a request's headers like so:
```
  headers = {
    "Authorization": "Bearer JWT_TOKEN"
  }
```

## Testing
To run the tests for local development, run:
```bash
python test_app.py
```

or

```bash
python3 test_app.py
```


