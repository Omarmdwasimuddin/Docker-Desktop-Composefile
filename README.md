## Docker-Desktop: Compose File (docker-compose.yml)

> #### Compose কি?
> Docker Compose হলো একটা tool, যেটা দিয়ে multiple container একসাথে define এবং run করা যায়, একটা single command দিয়ে।

#### project root e create koro compose.yaml file
```bash
services:
  img:
    build: .
    container_name: my-containers
    ports:
      - 3000:3000

```
---

#### terminal e command daw
```bash
docker compose up
```
---
