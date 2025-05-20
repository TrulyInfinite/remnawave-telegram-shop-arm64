# 🚀 Deploying `remnawave-telegram-shop` for ARM64 (e.g., Oracle ARM VPS)

This guide helps you build and deploy the `remnawave-telegram-shop` Telegram bot for ARM64 systems using Docker.

---

## 🧰 Prerequisites

- ARM64-based server (e.g., Oracle Cloud ARM instance)
- Docker & Docker Compose installed

---

## 📦 Step 1: Clone the Repository and Modify Architecture

```bash
git clone --single-branch --branch main https://github.com/Jolymmiles/remnawave-telegram-shop/ \
&& cd remnawave-telegram-shop \
&& sed -i 's/amd64/arm64/g' Dockerfile
```

---

## 🛠 Step 2: Edit the Dockerfile

```bash
nano Dockerfile
```

---

## ✏️ Step 3: Modify GitHub Repository Reference

Inside the `Dockerfile`, replace:

```
${GITHUB_REPOSITORY}
```

with:

```
Jolymmiles/remnawave-telegram-shop
```

> 💡 This ensures the build process pulls from the correct GitHub repo.

---

## 🏗 Step 4: Build the Docker Image for ARM64

```bash
docker buildx build \
  --platform linux/arm64 \
  --build-arg TARGETOS=linux \
  --build-arg TARGETARCH=arm64 \
  -f Dockerfile \
  -t remnawave-telegram-shop-bot:latest . --no-cache
```

---

## 🧾 Step 5: Update `docker-compose.yml`

```bash
nano docker-compose.yml
```

---

## 🔁 Step 6: Replace Image Reference

In the `docker-compose.yml`, update the image section:

```yaml
image: remnawave-telegram-shop-bot:latest
```

> ⚠️ Replace any existing image name like `xyz` with the one you just built.

---

## 🚀 Step 7: Run the Bot

```bash
docker compose up -d && docker compose logs -f
```

---

## ✅ Done!

Your `remnawave-telegram-shop` bot should now be up and running on your ARM64 server. You can monitor logs using the last command to ensure everything is working correctly.
