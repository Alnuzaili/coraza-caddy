# coraza-caddy

## How to run

```
docker-compose up
```

if you have faced this error

```
/bin/sh: [./entrypoint.sh]: not found
```

run:

```
dos2unix entrypoint.sh
```

After all your containers are running, send some attack to an exposed juiceshop, for example: curl http://prod.juiceshop.external/?id='%20''='
The previous payload should trigger a SQL injection event and create an audit log that we should be able to catch by running the following steps:

    1. Go to http://127.0.0.1:5601/app/management/kibana/dataViews (Stack Management → Data Views)
    2. Select “Create data view”
    3. Create an index pattern that matches the indices names, like coraza_*
    4. Select “Save data view to Kibana”
    5. Now we should see a list of fields like client_ip, client_port, etc

Now go to the “Discover” view, and we should see our recent event. If your recently created event is here, it means everything worked, and we are done :)