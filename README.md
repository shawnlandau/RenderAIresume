# Project Plan: Deploy Resume Customizer on Render

This plan will take you step-by-step from code to production for your full-stack project on Render.

---

## 1. Prepare Your Codebase

- Ensure your repo structure is:
  ```
  /
    client/    # React + Vite + Tailwind frontend
    server/    # Node.js + Express backend
  ```
- Add a `.env.example` file for required environment variables (e.g., `OPENAI_API_KEY`).
- Make sure both `client` and `server` have their own `package.json` and can run independently.

---

## 2. Deploy the Backend (Express API) on Render

1. **Push your latest code to GitHub.**
2. Go to [Render Dashboard](https://dashboard.render.com/).
3. Click **"New +" → "Web Service"**.
4. Connect your GitHub repo.
5. Select the `server` directory as the root.
6. Set environment:
    - **Environment:** Node
    - **Build Command:** `npm install`
    - **Start Command:** `npm start` or your server's start script
7. **Add Environment Variables:**
    - `OPENAI_API_KEY` (and any others your backend needs)
8. Click **"Create Web Service"**.
9. Wait for deployment and copy your backend's URL (e.g., `https://resume-customizer-backend.onrender.com`).

---

## 3. Deploy the Frontend (React) on Render

1. On the Render Dashboard, click **"New +" → "Static Site"**.
2. Connect the same GitHub repo.
3. Select the `client` directory as the root.
4. Set:
    - **Build Command:** `npm run build`
    - **Publish Directory:** `dist`
5. **Set Environment Variables** (if your frontend uses any at build time, e.g., `VITE_API_URL`):
    - Set `VITE_API_URL` to your backend’s Render URL.
6. Click **"Create Static Site"**.
7. Wait for deployment and copy your frontend URL.

---

## 4. Update Frontend API URLs

- Make sure your frontend (`client/src`) is configured to use the correct API base URL (e.g., `import.meta.env.VITE_API_URL`).
- For local dev, this might be `localhost:5000`, but for production it should be your Render backend URL.

---

## 5. Test End-to-End

- Visit your frontend's Render URL.
- Upload resumes, enter job descriptions, and confirm all features work.
- Check logs in Render dashboard for any errors.

---

## 6. Enable CORS on Backend

- Ensure your Express backend allows requests from your frontend domain:
  ```js
  const cors = require('cors');
  app.use(cors({ origin: 'https://your-frontend.onrender.com' }));
  ```
- For dev/testing, you can use `{ origin: '*' }` but restrict in production.

---

## 7. (Optional) Set Up Custom Domain

- In Render dashboard, add your custom domain to the frontend/static site.
- Follow Render’s instructions for DNS updates.

---

## 8. (Optional) Set Up Automatic Deploys

- Enable auto-deploys in Render so every push to `main` triggers a new build.

---

## 9. Final Checklist

- [ ] Backend deployed and live
- [ ] Frontend deployed and live
- [ ] Environment variables set
- [ ] CORS configured
- [ ] Frontend points to backend API
- [ ] All core flows tested (upload, parse, tailor, generate, export)
- [x] Documentation (README) updated

---

**You’re done!**  
Your full-stack app is live on Render, scalable, and maintainable.

If you need code samples for any step or run into issues, just ask!
