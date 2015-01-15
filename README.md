
Documment For API's
===================

1. Registration for service
2. Job request for application


### Registration

To register your application with the service you will need to pass a CURL request to the 
service.The curl request must contain Header "Content-Type" which can be either json/xml,body part contains a hash 
which will contain domain name which you want to register with service and the API end point.For eg.

Usage of Service
----------------

### API End Points:

| METHOD | End-Points       | Usage                                              | Returns                                                  |
|--------|------------------|----------------------------------------------------|----------------------------------------------------------|
| POST	 | /v1/registration	| Registration of you application to voodoo service. | Access key for accessing service(API-KEY)                |

### API-End Points and Parameters
#### For end point /v1/registration
|    Key   |Description                                          |
|----------|-----------------------------------------------------|
|app_domain| name of the domain you want to register into service|

* Example

```ruby
{"app_domain":"encrypted.google.com"}

For eg.
curl --header "Content-Type: application/json" --data '{"app_domain":"www.google.com"}' http://localhost:9292/v1/registration

### Job Request

The service supports 2 types of job requests.
1.Image processing request
2.Video processing request

#### You can do following operations on Images
* Crop
* Change Resolution
* Thumbnail
* Rotate
* Scale

#### Supported image formats
* jpg/jpeg
* png
* gif

You can do following operations on Videos
* Change the resolution
* Change the video format
* Video bitrate
* Split
* 

##### Supported video formats
* mp4
* avi
* ogg
* mkv
* wav
* mov
* m4a
* webm
* flv


Usage of Service
----------------

### API End Points:
| METHOD | End-Points       | Usage                                              | Returns                                                  |
|--------|------------------|----------------------------------------------------|----------------------------------------------------------|
| POST	 | /v1/create/job	| To submit a Job to service for process.            | Destination Url from where to collect your processed job |


### API-End Points and Parameters
#### For end point /v1/registration
|    Key   |Description                                          |
|----------|-----------------------------------------------------|
|app_domain| name of the domain you want to register into service|

* Example

```ruby
{"app_domain":"encrypted.google.com"}
```

#### For end point /v1/create/job
|Key             |Description                                                            |
|----------------|-----------------------------------------------------------------------|
|api_key         | Provided at the time of registration of the your application to system.|
|source_url      | Source of the file needed to be transformed.                          |
|notification_url| URL at which you need to be notified once job is complete.            |
|actions         | list of all the transformations need to be performed on your file.     |

* Example

```ruby
 {
  "api_key": "78bd3f81a861ce84",
  "source_url": "https://encrypted.google.com/images/srpr/logo11w.png",
  "actions": 
  {
    "rotate": 180
  },
  "notification_url": "http://encrypted.google.com/notificationpath"
}
```

Dependencies
------------

### FFmpeg:
It is the leading multimedia framework, able to decode, encode, transcode, stream, filter and play pretty much anything that humans and machines have created. It supports the most obscure ancient formats up to the cutting edge. No matter if they were designed by some standards committee, the community or a corporation.

### Imagemagick:
It is a software suite to create, edit, compose, or convert bitmap images. It can read and write images in a variety of formats (over 100) including GIF, JPEG, PDF, PNG, etc.ImageMagick used resize, flip, mirror, rotate, distort, shear and transform images, adjust image colors, apply various special effects, or draw text, lines, polygons, ellipses and Bézier curves.

### NSQ (New Simple Queue)
Installation
http://nsq.io/deployment/installing.html

### STEPS to Run Service

#### Change Directory

Change to voodoo Directory
```Shell
cd voodoo
```

#### START NSQ

##### Run binaries in nsq-0.3.0.linux-amd64.go1.3.3


* Start **`nsqlookupd daemon`** 
```Shell
bin/nsqlookupd
```
* Start **`nsqd daemon`**
```Shell
bin/nsqd --lookupd-tcp-address=127.0.0.1:4160
```
* Start **`NSQ Admin`**
```Shell
bin/nsqadmin --lookupd-http-address=127.0.0.1:4161
```


##### Run the commands if you are first time user of service 

* Install the dependencies
```Shell
bundle install
```
* Edit config/database.yml according to your database server

* Run the migrations

```Shell
ruby bin/migration_up
```


##### Commands to run service:

* Start **`RACK server`** on one console
```Shell
rackup
```
* Start **`Image consumer`** on new console
```Shell
ruby bin/image_consumer
```
* Start the **`Video Consumer`** on new console
```Shell
ruby bin/vidoe_consumer
```