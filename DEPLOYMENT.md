# Deployment Guide - Render

This guide explains how to deploy the Aishani E-commerce Next.js application to [Render](https://render.com/).

## 🛠 Prerequisites
- A Render account.
- A Postgre SQL database (can be created on Render).
- Environment variables configured.

---

## 📝 Configuration Settings

### Build & Start Settings
| Setting | Value |
|---|---|
| **Runtime** | Node |
| **Build Command** | `npm install; npx prisma generate; npm run build` |
| **Start Command** | `npm run start` |

---

## 🔑 Environment Variables

Required variables on Render:

| Variable | Description |
|---|---|
| `DATABASE_URL` | Your PostgreSQL connection string (provided by Render DB) |
| `NEXTAUTH_SECRET` | A random string for session encryption |
| `NEXTAUTH_URL` | Your deployment URL (e.g., `https://your-app.onrender.com`) |
| `STRIPE_SECRET_KEY` | Your Stripe secret key for payments |
| `STRIPE_WEBHOOK_SECRET` | Secret for verifying Stripe webhooks |
| `CLOUDINARY_CLOUD_NAME` | Cloudinary cloud name for images |
| `CLOUDINARY_API_KEY` | Cloudinary API key |
| `CLOUDINARY_API_SECRET` | Cloudinary API secret |

---

## 🚀 Deployment Steps

1. **Create a Web Service**: Connect your GitHub repository.
2. **Set Build/Start Commands**: Use the table above.
3. **Add Environment Variables**: Copy from your `.env.local`.
4. **Deploy**: Click "Create Web Service".

---

## 🏗 Database Setup (Render Postgres)

1. Create a **New PostgreSQL** instance on Render.
2. Copy the **Internal Database URL**.
3. Set it as the `DATABASE_URL` in your Web Service settings.
4. Prisma will automatically handle migrations during the build step (`npx prisma generate`).

---

## 🔍 Post-Deployment Check
- Verify that the App loads at the provided URL.
- Test the login/register flow.
- Ensure images from Cloudinary are loading correctly.
