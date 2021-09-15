# Simple Docker Compose Example

[![Alt text](https://tech.4germany.org/wp-content/uploads/2020/01/Logo-Final-02-copy-1-300x109-1.png)](https://tech.4germany.org)

Container `ping` will call `ping pong` command, to `ping` container `pong`.

```sh
+----------+        +----------+
|          |------->|          |
|   ping   |        |   pong   |
|          |< - - - |          |
+----------+        +----------+
```

## How to execute

1. Start the containers: `docker-compose up`
2. Stop the containers: `docker-compose down`
