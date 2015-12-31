# Flask based RESTful webservice demo 

Based on : http://blog.miguelgrinberg.com/post/designing-a-restful-api-with-python-and-flask

Simple "todo" webservice running in Docker.  There are lots of these tutorials online.  This is just for fun.

## Usage 

### Build the Docker image 
```
docker build -t thshaw/todo .
```
### Start the container
```
docker run --name todo_app -d -p 80:80 thshaw/todo
```

### Check that Flask is running ok
```
docker logs todo_app 
```

You should see something like :
```
2015-12-29 18:52:52,514 INFO success: nginx entered RUNNING state, process has stayed up for > than 1 seconds (startsecs)
2015-12-29 18:52:52,515 INFO success: app entered RUNNING state, process has stayed up for > than 1 seconds (startsecs)
```

The Flask app is just storing todo items in memory.  Removing the container will remove any changes you make.

## Test it works 

### Get all todo tasks
```
curl -i -u rest:restdemo http://localhost/todo/api/v1.0/tasks
```

### Get todo task id 1
```
curl -u rest:restdemo http://localhost/todo/api/v1.0/tasks/1
```

### Add a new todo item 
```
curl -i -u rest:restdemo -H "Content-Type: application/json" -X POST -d '{"description":"War and Peace", "title":"Read Book"}' http://localhost/todo/api/v1.0/tasks
```
### Update an existing item
```
curl -i -u rest:restdemo -H "Content-Type: application/json" -X PUT -d '{"done":false}' http://localhost/todo/api/v1.0/tasks/1
```

Delete a todo item 
```
curl -i -u rest:restdemo -H "Content-Type: application/json" -X DELETE http://localhost/todo/api/v1.0/tasks/2
```

### Teardown
```
docker rm -f todo_app
```
