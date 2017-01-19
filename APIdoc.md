# API Documentation

## /api/1.0/GPS

### POST params: geometry, accuracy, timestamp

inserts the values (got from the body of the http request) into the database
- geometry, add the current position as Geometry with longitude and latitude with the default spatial reference identifier 4326
- accuracy, the number of digits from the geometry as Integer
- timestamp, the current timestamp as the geometry is inserted into the database

example: curl --data "type=Feature&properties%5Btime%5D=17.1.2017%2C+11%3A30%3A38&properties%5Baccuracy%5D=1766&geometry%5Btype%5D=Point&geometry%5Bcoordinates%5D%5B%5D=51.9623597&geometry%5Bcoordinates%5D%5B%5D=7.6084083"<br>
response: 'Inserted history into the DB'

### GET returns params: id, ST_X(geom), ST_Y(geom), time, accuracy, crs

returns the following values from the database as json
- id, the identifier of the location
- ST_X(geom), the x-coordinate of the geometry as longitude
- ST_Y(geom), the y-coordinate of the geometry as latitude
- time, the timestamp of the location
- accuracy, the number of digits from the geometry as Integer
- crs, the coordinate reference system as String, as default 'WGS84'

example: curl --insecure https://giv-project13.uni-muenster.de:8443/api/1.0/GPS<br>
response:

## /api/1.0/timeslider/:string/:bounds

### POST params: string, bounds, timestamp

inserts the values (from the URL parameter) into the database
- string, the path of the wms as varchar
- bounds, the boundingbox of the wms as varchar (containing two points indicating the diagonal)
- timestamp, the current timestamp as the geometry is inserted into the database

example: curl --data https://giv-project13.uni-muenster.de:8443/api/1.0/timeslider/:/:<br>
response: 'Inserted history into the DB'

## /api/1.0/timeslider/:number

### GET returns params: time, path

returns the values of the wms from the last ':number' minutes as json
- time, the timestamp of the wms
- path, the path of the wms as varchar 

example: curl --insecure https://giv-project13.uni-muenster.de:8443/api/1.0/timeslider/10<br>
response: [{"time":"2017-01-17T11:36:11.781Z","path":"/var/img/test0001.png"}]

## /api/1.0/currentPicture

### GET returns params: path, bbox

returns the following values of the latest wms from the database as json
- path, the path of the wms as varchar
- bbox, the boundingbox of the wms as varchar (containing two points indicating the diagonal)

example: curl --insecure https://giv-project13.uni-muenster.de:8443/api/1.0/currentPicture<br>
response: [{"time":"2017-01-17T11:36:11.781Z","path":"/var/img/test0001.png"}]