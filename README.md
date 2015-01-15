
Usage of Service
================

1. Registration for service
2. Job request for application

### Registration

To register your application with the service you will need to pass a CURL request to the service.

#### API End Point:

| Method | End-Point        | Usage                                              | Returns                                                  |
|--------|------------------|----------------------------------------------------|----------------------------------------------------------|
| POST	 | /v1/registration	| Registration of you application to voodoo service. | Access key for accessing service(API-KEY)                |

#### Registration Parameters
#### For end point /v1/registration

|    Key   |Description                                          |
|----------|-----------------------------------------------------|
|app_domain| name of the domain you want to register into service|

* Example

```ruby
{"app_domain":"encrypted.google.com"}
```
Curl Request Example.
```
curl --header "Content-Type: application/json" --data '{"app_domain":"www.google.com"}' http://localhost:9292/v1/registration
```
#### Job Request

The service supports 2 types of job requests.

1. Image processing request
2. Video processing request

### You can do following operations on Images
* Crop
* Change Resolution
* Thumbnail
* Rotate
* Scale

### Supported image formats
* jpg/jpeg
* png
* gif

### You can do following operations on Videos
* Change the resolution
* Change the video format
* Video bit-rate
* Split

#### Supported video formats
* .mp4
* .avi
* .ogg
* .mkv
* .wav
* .mov
* .m4a
* .webm
* .flv


Usage of Service
----------------

### API End Point:
| METHOD | End-Point        | Usage                                              | Returns                                                  |
|--------|------------------|----------------------------------------------------|----------------------------------------------------------|
| POST	 | /v1/create/job	| To submit a Job to service for process.            | Destination Url from where to collect your processed job |


#### For end point /v1/create/job
|Key             |Description                                                             |
|----------------|------------------------------------------------------------------------|
|api_key         | Provided at the time of registration of the your application to system.|
|source_url      | Source of the file needed to be transformed.                           |
|notification_url| URL at which you need to be notified once job is complete.             |
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

Curl Request Example
```
curl --header "Content-Type: application/json" --data '{"api_key":"bbeb4924d066922f", "src_url": "http://www.imagica.com/pathtomedia.jpg", "actions": {"resize": 50000, "quality": 50}, "notification_url": "http://www.imagica.com/notificationpath"}' -X POST http://localhost:9292/v1/create/job
```