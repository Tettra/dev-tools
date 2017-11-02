**Note** : Platform versions >= 1.9.86 include a timed service to clean up after Docker. However, it may be necessary to run the below steps manually immediately following an appliance upgrade.

If you see the `/` filling up, the first thing you look at should be: https://app.getguru.com/\#/facts/b2819a3f-5b18-4f58-b7f7-87f9d77c1b21

If that isn't the problem, proceed.

To clean up old, dead Docker containers that are using up all the space on an appliance's `/` drive, use the following command: `docker ps -a | grep 'weeks ago' | awk '{print $1}' | xargs --no-run-if-empty docker rm`

Depending on how long it has been since a cleanup, might also need to run with `'months ago'`

Second: If the appliance is very very old, it may have tens of secure container images, each taking up 1-2gb each. You can remove the oldest images by doing

`docker images | grep secure`

Then run

`docker rmi <img id>`

This will let you clear up 1-2GB per old image. Running this command can take some time, between 15 seconds and 2 minutes while docker sorts out what cached slabs it needs to keep and what it can delete.

The following commands can be run on a system that is currently *up* and *working* to remove stale containers and images in a single shot; containers and images that are *currently in use* will not be removed. **Exercise caution.** If any `:latest` image versions required by the system are not currently in use by a running container, the following commands will remove them.

Delete all containers
`docker rm $(docker ps -a -q)`
Delete all images
`docker rmi $(docker images -q)`

See also: this card on expanding a drive
https://app.getguru.com/\#/facts/c196b8d6-37a2-4b01-9105-d2e8ce36403e
