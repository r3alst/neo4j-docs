### Backup Neo4j Community Database
```shell
export NEO4J_DATA_PATH="$(pwd)/neo4j/data"
export BACKUP_DATA_PATH="$(pwd)/backups"
export NEO4J_CONTAINER_ID="45ba9c959d78"
docker container stop $NEO4J_CONTAINER_ID
docker run --interactive --tty --rm --volume=$NEO4J_DATA_PATH:/data --volume=$BACKUP_DATA_PATH:/backups neo4j/neo4j-admin:4.4.9-community neo4j-admin dump --to=/backups
docker container start $NEO4J_CONTAINER_ID
```

### Restore Neo4j Community Database
```shell
export NEO4J_DATA_PATH="$(pwd)/neo4j/data"
export BACKUP_DATA_PATH="$(pwd)/backups"
export NEO4J_CONTAINER_ID="45ba9c959d78"
docker container stop $NEO4J_CONTAINER_ID
docker run --interactive --tty --rm --volume=$NEO4J_DATA_PATH:/data --volume=$BACKUP_DATA_PATH:/backups neo4j/neo4j-admin:4.4.9-community neo4j-admin load --from=/backups/neo4j.dump --force
docker container start $NEO4J_CONTAINER_ID
```