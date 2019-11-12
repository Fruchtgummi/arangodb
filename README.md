# arangodb
arangodb docker-compose with treafik


```
version: '3'
networks:
  web:
    external: true

volumes:
  arangodbdev:

services:
  arangodb:
    image: arangodb/arangodb:latest
    volumes:
      - arangodbdev:/data
    ports:
      - 8529:8529
    environment:
      - ARANGO_ROOT_PASSWORD=mypasswort
    networks:
      - web
      - default
    expose:
      - "3000"
    labels:
      - traefik.docker.network=web
      - traefik.enable=true
      - traefik.port=8529
      - traefik.frontend.rule=Host:db.mydomain.com
    restart: always
```
