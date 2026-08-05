# Docker Compose

## Compose কী?

Docker Compose হলো একটি tool, যার মাধ্যমে **একাধিক (multiple) container**-কে একটি configuration file ব্যবহার করে define, build এবং run করা যায় **একটি মাত্র command** দিয়ে।

ধরো তোমার একটি application চালানোর জন্য লাগে:

* একটি **Backend Container**
* একটি **Database Container**
* একটি **Redis Container**

যদি এগুলো আলাদা আলাদা `docker run` command দিয়ে চালাও, তাহলে প্রতিটি container-এর port, network, volume, environment variable এবং dependency আলাদাভাবে configure করতে হবে। Project বড় হলে এই process জটিল এবং error-prone হয়ে যায়।

Docker Compose এই পুরো process-কে অনেক সহজ করে দেয়।

---

## Compose File কী?

Compose File হলো একটি **YAML configuration file**, যার recommended নাম **`compose.yaml`**।

এই ফাইলে তুমি define করে রাখো:

* কোন কোন **Service (Container)** থাকবে
* প্রতিটি Service কোন **Image** ব্যবহার করবে অথবা **Dockerfile** থেকে build হবে
* কোন **Port** expose হবে
* কোন **Environment Variable** ব্যবহার হবে
* কোন **Volume** বা **Bind Mount** ব্যবহার হবে
* Service গুলো একে অপরের সাথে কীভাবে **Connect** হবে
* কোন Service-এর উপর অন্য Service **Depend** করবে

---

## উদাহরণ

```yaml
services:
  backend:
    build: ./backend
    container_name: backend
    ports:
      - "5000:5000"
    environment:
      DATABASE_URL: postgres://user:pass@db:5432/mydb
    depends_on:
      - db

  db:
    image: postgres:15
    container_name: postgres-db
    environment:
      POSTGRES_PASSWORD: pass
    volumes:
      - db-data:/var/lib/postgresql/data

volumes:
  db-data:
```

এখানে দুটি Service আছে:

* `backend`
* `db`

Docker Compose স্বয়ংক্রিয়ভাবে এই দুইটি Service-এর জন্য একটি **Internal Network** তৈরি করে।

তাই `backend` Container থেকে Database-এ connect করার সময় IP Address ব্যবহার করতে হয় না। শুধু Service Name (`db`) ব্যবহার করলেই হয়।

---

## কিভাবে চালানো হয়

সব Service Build এবং Start করতে:

```bash
docker compose up
```

Background-এ চালাতে:

```bash
docker compose up -d
```

সব Container, Network এবং Compose Resources Stop ও Remove করতে:

```bash
docker compose down
```

---

## Docker Compose কেন দরকার?

* এক জায়গায় **সব Container Configuration** রাখা যায়
* একাধিক Container **একটি Command** দিয়ে চালানো যায়
* Service গুলোর মধ্যে **Automatic Networking** তৈরি হয়
* **Startup Order** (`depends_on`) নির্ধারণ করা যায়
* **Volume** এবং **Bind Mount** সহজে configure করা যায়
* Development Environment সহজে অন্য Machine-এ একইভাবে পুনরায় তৈরি (Reproduce) করা যায়

---

## সংক্ষেপে

* **Docker** → একটি Container তৈরি ও চালানোর জন্য ব্যবহৃত হয়।
* **Docker Compose** → একাধিক Container-কে একটি `compose.yaml` file-এর মাধ্যমে একসাথে configure, build এবং run করার জন্য ব্যবহৃত হয়।
