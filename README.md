# see-tclient-traffic
Instructions you can follow that will let you view (plaintext) Temporal 
Client requests and responses. This is helpful for learning about the 
communication between the Client and Temporal Cluster.

Note that these instructions assume that you are using a Mac
and already have the Homebrew and Temporal CLI installed.

## Install `grpc-dump`

```
$ brew install bradleyjkemp/formulae/grpc-tools
```

## Start Temporal Cluster (Using an Alternate Frontend Port)

```bash
$ temporal server start-dev --port 7234
```

## Start `grpc-dump` 

This will capture all Client traffic intended for the
standard Frontend Service port on `localhost`, display
a JSON representation of it to STDOUT, and forward the
gRPC traffic to the Temporal Cluster's Frontend service
on the alternate port (tcp/7234).

Run the following in another terminal window or tab:

```bash
$ grpc-dump --port 7233 --destination localhost:7234
```

# Run Your Worker and Starter

Run your Worker and Starter as normal, and then look
at the tab where you are running `grpc-dump`. You should
then be able to view the Client's request and Cluster's 
responses.
