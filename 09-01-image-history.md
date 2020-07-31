# Image History

In this lesson, see how to get more information about an image by looking at its history.

Show the history of an image:
```
docker image history <IMAGE>
docker image history --no-trunc <IMAGE>
docker image history --quiet <IMAGE>
docker image history --quiet --no-trunc <IMAGE>
```

Get the image history for Node:
```
docker image history node:latest
```

Get the image history for weather-app:
```
docker image history rivethead42/weather-app:latest
```

Get the image history weather-app:v1 with the no-truncm flag:
```
docker image history --no-trunc linuxacademy/weather-app:v1
```

Save the output using the no-truncm flag to a file:
```
docker image history --no-trunc linuxacademy/weather-app:v1 > output.txt
```

View the contents:
```
vi output.txt
```

Use the quiet flag to list the image IDs:
```
docker image history --quiet linuxacademy/weather-app:v1
```

Use the quiet flag to list the image IDs, then save the output to a file using the no-truncm flag:
```
docker image history --quiet --no-trunc linuxacademy/weather-app:v1
```
