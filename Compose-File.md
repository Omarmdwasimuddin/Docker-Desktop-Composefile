# Docker Compose

## Compose কি?

Docker Compose হলো একটা tool, যেটা দিয়ে **multiple container** একসাথে define এবং run করা যায়, একটা single command দিয়ে।

মনে করো তোমার একটা app চালাতে লাগে:
- একটা backend container
- একটা database container
- একটা redis container

এই তিনটা container আলাদা আলাদা `docker run` command দিয়ে চালানো, network connect করা, dependency handle করা — এইসব manually করা কষ্টকর এবং error-prone। Compose এই পুরো process-কে সহজ করে দেয়।

## Compose File কি?

Compose File হলো একটা YAML file (সাধারণত নাম `docker-compose.yml`), যেখানে তুমি লিখে রাখো:

- কোন কোন **service** (container) লাগবে
- প্রতিটা service কোন **image** থেকে বানানো হবে
- কোন **port** expose হবে
- কোন **environment variable** লাগবে
- service গুলা একে অপরের সাথে কিভাবে **connect** হবে
- কোন **volume** বা **bind mount** ব্যবহার হবে

## উদাহরণ

```yaml
version: "3.9"
services:
  backend:
    build: ./backend
    ports:
      - "5000:5000"
    environment:
      - DATABASE_URL=postgres://user:pass@db:5432/mydb
    depends_on:
      - db

  db:
    image: postgres:15
    environment:
      - POSTGRES_PASSWORD=pass
    volumes:
      - db-data:/var/lib/postgresql/data

volumes:
  db-data:
```

এখানে দুইটা service আছে: `backend` আর `db`। Compose নিজে থেকেই দুইটা container-এর মধ্যে একটা internal network বানিয়ে দেয়, তাই `backend` থেকে `db` কে service name (`db`) দিয়েই access করা যায়।

## কিভাবে চালানো হয়

```bash
docker compose up
```

এই একটা command দিলেই Compose file অনুযায়ী সব service (container) build এবং start হয়ে যায়।

```bash
docker compose down
```

সব container stop এবং remove করে দেয়।

## Compose কেন দরকার

- Multiple container-কে **এক জায়গায় define** করা যায় (single source of truth)
- Service গুলার মধ্যে **networking automatically** হয়ে যায়
- **Startup order** (`depends_on`) control করা যায়
- Development environment সহজে **reproduce** করা যায় — যেকোনো machine-এ একই command দিয়ে একই setup পাওয়া যায়

## সংক্ষেপে

- **Docker** → একটা single container চালায়
- **Docker Compose** → multiple container-কে একসাথে, coordinated ভাবে চালায়, একটা YAML file-এর মাধ্যমে
