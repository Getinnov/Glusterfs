# Docker swarm gluster

Using gluster from inside container to sync two directories 
**Warning** still in early developpement use with caution

Change:
 * `{your_registry}` by your private repository address

Build the image and send it to your private repo
```bash
docker-compose -f build_gluster.yml build
docker-compose -f build_gluster.yml push
```

Tag a manager node with label `db=main` and a worker node with label `db=save`

Launch it

```bash
docker stack deploy -c gluster.yml gluster
```
