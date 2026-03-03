# Deployment Guide — Render

This guide explains how to deploy the Aishani E-commerce (Next.js 14) app to [Render](https://render.com/) using **Neon PostgreSQL** as the database.

---

## 🛠 Prerequisites

- A [Render](https://render.com/) account
- Code pushed to a GitHub repository
- A [Neon](https://neon.tech/) PostgreSQL database (already configured)
- All environment variables ready (see below)

---

## 🚀 Step-by-Step Deployment

### 1. Push to GitHub
```bash
git add .
git commit -m "Deploy to Render"
git push origin main
```
> ⚠️ Make sure `.env` and `.env.local` are listed in `.gitignore` — never push secrets!

---

### 2. Create a Web Service on Render

1. Go to [render.com](https://render.com) → **New** → **Web Service**
2. Connect your GitHub repository
3. Configure the following settings:

| Setting | Value |
|---------|-------|
| **Environment** | `Node` |
| **Build Command** | `npm install && npx prisma generate && npm run build` |
| **Start Command** | `npm start` |
| **Node Version** | `18` or higher |

---

### 3. Add Environment Variables

In Render dashboard → your service → **Environment** tab, add:

| Variable | Value |
|----------|-------|
| `DATABASE_URL` | Your Neon connection string (pooler URL) |
| `NEXTAUTH_SECRET` | Same value from your `.env` |
| `NEXTAUTH_URL` | Your Render URL, e.g. `https://your-app.onrender.com` |
| `STRIPE_SECRET_KEY` | Your Stripe secret key |
| `STRIPE_PUBLISHABLE_KEY` | Your Stripe publishable key |
| `CLOUDINARY_CLOUD_NAME` | Your Cloudinary cloud name |
| `CLOUDINARY_API_KEY` | Your Cloudinary API key |
| `CLOUDINARY_API_SECRET` | Your Cloudinary API secret |

> ⚠️ **Important:** Set `NEXTAUTH_URL` to your actual Render deployed URL — you'll get this after the first deploy.

---

### 4. Deploy

- Click **Create Web Service**
- Render will build and deploy automatically
- Every `git push` to `main` triggers a redeploy

---

## 🗄 Database (Neon PostgreSQL)

This project uses **Neon** cloud PostgreSQL — no separate database setup on Render is needed.

- The schema is already pushed via `prisma db push`
- Demo users and products are already seeded
- Just set the correct `DATABASE_URL` (Neon connection string) in Render's env vars

To re-seed locally at any time:
```bash
npm run db:seed
```

---

## 🔍 Post-Deployment Checklist

- [ ] App loads at the Render URL
- [ ] `/login` works with demo credentials (`admin@aishani.com` / `admin123`)
- [ ] `/register` creates a new user successfully
- [ ] Products load on the homepage
- [ ] Logout redirects correctly (check `NEXTAUTH_URL` is set to Render URL)

---

## 💡 Tips

| Issue | Fix |
|-------|-----|
| App is slow on first load | Free tier sleeps after inactivity — upgrade to paid plan |
| Logout redirects to wrong URL | Update `NEXTAUTH_URL` env var to your Render URL |
| DB connection fails | Make sure `DATABASE_URL` is the Neon **pooler** connection string |
| Build fails | Check that `npx prisma generate` runs before `npm run build` |
