# OAuth bridge for spotify to react test

This service takes a login request to Spotify and redirects the user to a frontend application specified in the file "server.js" with a valid access_token as a parameter in the url.

## Development mode

In development mode, it assumes you are running the frontend on localhost:3000, but the server itself will be running on localhost:8888.

In order to start developing, register a Spotify Application here:
https://developer.spotify.com/dashboard/applications

On that page, add http://localhost:8888 as a callback url (don't forget to hit save at the bottom of the page)

Write the below commands in your terminal (replacing XXXX AND YYYY with your acutal client id and secret from the page where you registered your application)

```
export SPOTIFY_CLIENT_ID=XXXX
export SPOTIFY_CLIENT_SECRET=YYYY
npm start
```

Then go to http://localhost:8888/login in your browser. This will initiate the login flow and finally redirect to http://localhost:3000?access_token=ZZZZZ where ZZZZZ is a valid access token that you can use to do operations in the Spotify API.

## Deploying to production

This template is indended to be deployed on Heroku. After installing the heroku CLI tools you can run the below commands in the same directory as server.js(replacing abc123, cba456, mybackend and myfrontend with your actual stuff - the below example assume that you already have your frontend running on http://myfrontend.herokuapp.com.

```
heroku create mk3-spotify-backend
heroku config:set SPOTIFY_CLIENT_ID=abc123 --app=mk3-spotify-backend
heroku config:set SPOTIFY_CLIENT_SECRET=cba456 --app=mk3-spotify-backend
heroku config:set REDIRECT_URI=https://mk3-spotify-backend.herokuapp.com/callback --app=mk3-spotify-backend
heroku config:set FRONTEND_URI=https://myfrontend.herokuapp.com --app=mk3-spotify-backend
git push heroku master
```

You should now be able to go to http://mk3-react-backend.herokuapp.com/login and it will eventually redirect to http://myfrontend.herokuapp.com?access_token=ZZZZZwhere ZZZZZ is a valid access token that you can use to do operations in the Spotify API.
