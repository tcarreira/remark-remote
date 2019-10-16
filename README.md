[![Build Status](https://travis-ci.org/tcarreira/remark-remote.svg?branch=master)](https://travis-ci.org/tcarreira/remark-remote)
# Presenter Switch

The goal of this project is to allow automated triggering of content into HTTP clients listening on a [SSE](https://en.wikipedia.org/wiki/Server-sent_events) connection.

Ultimately, this allows having multiple clients listening to different URLs for specific content and allows you to change the room's content remotely or automatically (if you create a bot). 

At Ubucon Europe 2019, we will have 4 rooms to manage, each with their own schedule and non-overlapping terms. This server allows some clients to connect and we can change the content of the template by calling a POST method against the API. Provided we will have an iCal calendar, we can automate this process by building another bot that will trigger the HTTP events on time, thus dynamically changing the room's displayed text.

You may also change the slides (next/previous slide) using the admin interface (remote control).

## Running

Check out the repository and simply install the binaries (requires [Go](https://golang.org/) to be installed on your machine:

```
git clone https://github.com/ubuconeurope/present-switch
cd present-switch/
go build && ./present-switch
```
The server should then start listening on port `3000`.


## Using

Open your browser at http://localhost:3000/rooms/1/

Then, you may change the information with the API via curl, or via [Admin page](#admin-page)

Via curl:

```
curl -X POST -H 'Content-Type: application/json'  "http://localhost:3000/rooms/1" -d '{"room": "Master Room", "title": "Presentation Title", "speaker": "Speaker Name", "time": "00:01", "n_title": "This is the Title of the Next Presentation", "n_speaker": "Another Speaker", "n_time": "23:59", "auto-loop-sec": 5}'
```

If you set the environment variables `ROOMS_AUTH_USERNAME` and `ROOMS_AUTH_PASSWORD`, 
this updates (POST) are protected with BasicAuth

If you want to run this in a raspberry pi via ssh, you may open the browser using:
```
chromium-browser --app=http://localhost:3000/rooms/1 --display=:0 --start-fullscreen
```

## Admin page

You may update RoomInfo using the `admin` interface (instead of curl)
You may admin the room #1 through http://localhost:3000/admin/1/ 

You may update all information available through the API (curl) and control the slides.

If you set the environment variables `ADMIN_AUTH_USERNAME` and `ADMIN_AUTH_PASSWORD`, 
this admin pages are protected with BasicAuth


## Contributing

Check the issues page to know where your skills can be useful.
