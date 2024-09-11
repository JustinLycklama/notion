# Python for Spotify

Create Virtual Env, then Activate

```jsx
python3 -m venv venv

source venv/bin/activate
```

Install required dependancies

```jsx
pip install spotipy gspread oauth2client
```

Test your script

```jsx
python3 test.py
```

## Authentication

run [auth.py](http://auth.py) and follow the steps to get refresh and access tokens

insert the tokens into the lambda_handler.py function

## Lambda Package

We ned to package relevant libraries with our lambda, like spotipy

### Package

```jsx
mkdir -p package
pip install --target ./package spotipy boto3
```

### Zip

```jsx
cd package
zip -r9 ../function.zip .
cd ..
zip -g function.zip lambda_function.py
```

### Update

```jsx
aws lambda update-function-code --function-name SpotifySync --zip-file fileb://function.zip

```

# Stuck at Spotify Auth

To keep authenticated, need to store access token and refresh token, and perform refreshed. Probably some kind of database?  A lot of work for a simple thing

Good example:

[https://github.com/resident-archive/core/tree/a869b73f1f64538343be1604d43693b6165cc58a/functions/to-spotify](https://github.com/resident-archive/core/tree/a869b73f1f64538343be1604d43693b6165cc58a/functions/to-spotify)