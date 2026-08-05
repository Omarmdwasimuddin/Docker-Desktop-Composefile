# Docker Desktop: Docker Compose (compose.yaml)

## Compose কী?

Docker Compose হলো একটি tool, যা `compose.yaml` ফাইল ব্যবহার করে একাধিক Container-এর configuration define করে এবং একটি single command (`docker compose up`) দিয়ে সেগুলো build ও run করতে সাহায্য করে।

---

## ১. Project Root-এ `compose.yaml` File তৈরি করা

```yaml
services:
  img:
    build: .
    container_name: my-containers
    ports:
      - 3000:3000
```

> এখানে `services` এর ভেতরে `img` নামে একটি service define করা হয়েছে। `build: .` মানে current directory-এর `Dockerfile` ব্যবহার করে image build হবে। `container_name` দিয়ে container-এর নাম নির্ধারণ করা হয়েছে, এবং `ports` দিয়ে host machine-এর port-কে container-এর port-এর সাথে map করা হয়েছে।

---

## ২. Terminal-এ Command চালানো

```bash
docker compose up
```

---

## ফলাফল

এই command চালানোর পর Docker Desktop-এ image এবং container build হয়ে যাবে, এবং browser-এ server running অবস্থায় দেখা যাবে।

---
