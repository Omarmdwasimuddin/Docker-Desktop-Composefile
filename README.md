## Docker Desktop: Docker Compose (compose.yaml)

> #### Compose কি?
> Docker Compose হলো একটি tool, যা compose.yaml ফাইল ব্যবহার করে একাধিক Container-এর configuration define এবং একটি single command (docker compose up) দিয়ে সেগুলো build ও run করতে সাহায্য করে।

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
> docker desktop e images and containers build hoye jabe and brower e server running hobe.
