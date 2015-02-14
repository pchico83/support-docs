## Deploy the app as a Tutum service

In this step you will deploy the app as a Tutum Service. Remember that a service is a group of containers of the same **image:tag**. 

``` 
$ tutum service run -p 80 --name web tutum.co/$TUTUM_USER/quickstart-go
```

If you don't have Docker installed locally and you have been following this tutorial, it's likely that you don't have the `quickstart-go` image in your private registry at Tutum. For this reason the command above won't work. To deploy the service in this case, you can use the public image `tutum/quickstart-go` available from the Docker Hub. To do this execute the following command:

``` 
$ tutum service run -p 80 --name web tutum/quickstart-go
```

The `run` command will **create and run** the service using the image *tutum.co/golang-user/quickstart-go* or *tutum/quickstart-go*. The **-p 80** flag will publish (make publicly accessible) port 80 in the container and map it to a dynamically assigned port in the node. 

It will take up to a few minutes to get your service up and **running**. To check on the status of your service execute the following command:

```
NAME         UUID      STATUS          #CONTAINERS  IMAGE                                      DEPLOYED      PUBLICDNS
web          1ecbf656  ▶ Running                 1  tutum.co/golang-user/quickstart-go:latest  1 minute ago  web.borjaburgos.svc.tutum.io
```

Check to make sure that the **STATUS** is **Running**. Now let's visit the app at the URL generated by its service name. 

```
$ tutum container ps --service web
NAME                   UUID      STATUS     IMAGE                                          RUN COMMAND          EXIT CODE  DEPLOYED      PORTS
web-1                  6c89f20e  ▶ Running  tutum.co/golang-user/quickstart-go:latest  python app.py                   1 minute ago  web-1.golang-user.cont.tutum.io:49162->80/tcp
```

The **PORTS** column contains the URL we'll use to see our service running in our browser. Open a browser to that URL (in the example above, it is [web-1.golang-user.cont.tutum.io:49162](web-1.golang-user.cont.tutum.io:49162)). 

Alternatively, you can use *curl*:

    $ curl web-1.$TUTUM_USER.cont.tutum.io:49162
    <h1>hello, world</h1>
    <b>Hostname: </b>web-1<br><b>MongoDB Status: </b>Not available%

**CONGRATULATIONS!** You've deployed your first service using Tutum.

Next: [Define environment variables](https://tutum.freshdesk.com/support/solutions/articles/5000559794).
