# mongodb-sync-example
Purpose of this repo is to provide a getting started example of setting up mongodb synchorinization across multiple mongodb instances.

# No Sync Setup
To start with, we have a docker-compose up file (docker-compose-no-sync.yml) with 3 separate mongodb instances. We use mongo express for connecting and visualizing the data in each of these mongodb instances.

To run this setup, use the command:
```
docker-compose -p mongo-no-sync -f docker-compose-no-sync.yml up -d
```
This would launch 3 instances of mongodb and 3 mapped instances of mongo express. Mongo express can be accessed in browser via port exposed. Eg: http://localhost:8101/

Here there is no synchornization and each mongodb instance is separate. When you add an item via one of the mongo express instances, it would not sync in other two instances.


# Sync Setup
Next, we have a separate docker compose file (docker-compose-no-sync.yml), similar to the no-sync setup, but with the synchronization options set.

To run this setup, use the command:
```
docker-compose -p mongo-sync -f docker-compose-sync.yml up -d
```
This would launch 3 instances of mongodb and 3 mapped instances of mongo express. Mongo express can be accessed in browser via port exposed. Eg: http://localhost:8201/

When you add an item via one of the mongo express instances, it would showup in other two instances, proving the synchronization across the mongo databases.

The command under healthcheck of mongo-s1 is for setting up the replica set. This needs to be executed only once and under only one instance. The command rs.status() will result in error when the replica set is not configured, using which we can execute this command to be executed only once.

# Credits
- https://medium.com/workleap/the-only-local-mongodb-replica-set-with-docker-compose-guide-youll-ever-need-2f0b74dd8384
