Its the same project as the 
```bash
https://github.com/Lewan24/PanelPracowniczy_Scheme
```

but here its uses the Identity system for login, registering etc.

It uses external postgresql database to store all needed data.
You can create that database on docker via docker-compose.yml included into project files

```dockerfile
version: "3.9"

services:
  postgres:
    image: postgres
    environment:
      POSTGRES_USER: root
      POSTGRES_PASSWORD: toor
      POSTGRES_DB: pp
    ports:
      - "5432:5432/tcp"
    networks:
      - demo-net
    deploy:
      restart_policy:
        condition: on-failure
  adminer:
    image: adminer:latest
    ports:
      - "8180:8080/tcp"
    networks:
      - demo-net
    deploy:
      restart_policy:
        condition: on-failure
  server:
    context: .
    dockerfile: Dockerfile
    ports:
      - "5000:80/tcp"
      - "5443:443/tcp"
    networks:
      - demo-net
    deploy:
      restart_policy:
        condition: on-failure

networks:
  demo-net:
```

Currently the app does not work properly on docker. It throws errors while running. But works docker via VS studio and Https.

The app identity system is created by Duende software it needs a valid license key if you want to make the app running on Production version.
For nonprofit apps and small bussiness there is the free license key. But you have to contact to them.
For developing and test purposes, the system is free to use.
