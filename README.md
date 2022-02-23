# image-shell is no longer actively maintained by VMware, Inc.

# Spring XD Shell
A Docker image that runs a Spring XD Shell.

There currently isn't any way to specify the Admin URL when launching a shell 
(see [this issue](https://jira.spring.io/browse/XD-2072)), so you'll need to use

    xd:>admin config server http://host:ip

to connect to the running admin server.

As an example, if using the springxd/admin image:

	docker run --name admin \
	    --link zookeeper:zookeeper \
	    --link hsqldb:hsqldb \
	    --link redis:redis \
	    -d \
	    - 9393:9393\
	    springxd/admin

Note how we exposed the `9393` port above. The, run this image:

	docker run --name shell \
	    -it \
	    springxd/shell

and use

    xd:>admin config server http://localhost:9393

Replacing `localhost` with your host running Docker (if running inside boot2docekr for example, one can use 
`boot2docker ip` to get the IP to connect to). 

**Note** that http://localhost:9393 is actually the shell default, so if running with a local Docker demon
and mapping 9393 to 9393, you're actually good to go.
