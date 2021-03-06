# project-management-api

## Overview ##
This repository contains the necessary files to host restful API's using Protocol Buffers (a.k.a protobuf) under golang to run a database. Information on protocol buffers
can be found on [protobufs Google Developers site](https://developers.google.com/protocol-buffers/docs/proto3).
All of the endpoints are hosted using [Heroku](https://www.heroku.com). The database was implemented using [MongoDB](https://mongodb.com)
with the help of the public MongoDB driver [mgo](https://github.com/globalsign/mgo) and is being hosted using [mLab](https://mlab.com).
This repository handles requests from the project dashboard and all of its components.

## Program Execution ##
Make sure [mgo](https://github.com/globalsign/mgo), [glog](https://github.com/golang/glog), [grpc-gateway](https://github.com/grpc-ecosystem/grpc-gateway), 
[cors](https://github.com/rs/cors), and [grpc](https://godoc.org/google.golang.org/grpc) are installed in your golang environment. To execute the program 
run the server.go file as follows,

	go run server.go

This will execute the server file.

## Endpoints ##
Each endpoint expects to receive specific fields to process a request. The following are the expectations for each endpoint and the response. The API link is https://tea-project-management-api.herokuapp.com/. Note that each endpoint only accepts POST requests, so the link will only display a "Not Found" message since GET requests aren't supported.

| Endpoint | Request | Response |
|:--------:|---------|----------|
| addmilestone   | string xid = 1;<br>string title = 2;<br>string description = 3;<br>repeated string users = 4;<br>int32 weight = 5; | bool success = 1; |
| editmilestone    | string milestoneid = 1;<br>string title = 2;<br>string description = 3;<br>repeated string users = 4;<br>int32 weight = 5| bool success = 1;|
| deletemilestone | string xid = 1;<br>string milestoneid = 2; | bool success = 1; |
| milestonecompletion | string milestoneid = 1; | bool success = 1; |
| getallmilestones | repeated string milestoneid = 1; | bool success = 1;<br>repeated MilestoneModel milestones = 2;|
| getprojectmembers | string xid = 1;<br>repeated string memberslist = 2; | bool success = 1;<br>repeated UserTuple users = 2;|
| inviteuser | string xid = 1;<br>string recipientemail = 2;<br>string senderemail = 3; | bool success = 1; |
| acceptinvitation | string email = 1;<br>string xid = 2; | bool success = 1; |
| rejectinvitation | string email = 1;<br>string xid = 2; | bool success = 1; |
| adduser | string xid = 1;<br>string email = 2; | bool success = 1; |
| removeuser | string xid = 1;<br>string email = 2; | bool success = 1; |
| rejectuser | string xid = 1;<br>string email = 2; | bool success = 1; |
| transferleader | string xid = 1;<br>string newleader = 2; | bool success = 1; |
| announcement | string xid = 1;<br>string poster = 2;<br>string message = 3;<br>bool pin = 4; | bool success = 1; |
| removenotification | string notification = 1;<br>string user = 2; | bool success = 1; |
| toggledone | string xid = 1;<br>bool prevdone = 2; | bool success = 1; |
| updatepercentage | string xid = 1;<br>string percent = 2; | bool success = 1; |


## Types ##
These are the outlines of some of the custom types which are returned.

| Type | Fields |
|:--------:|---------|
| MilestoneModel   | string milestoneid = 1;<br>string title = 2;<br>string description = 3;<br>repeated string users = 4;<br>int32 weight = 5;<br>bool done = 6; |
| UserTuple   | string email = 1;<br>string firstname = 2; |
