# The City Language Academy — Landing Page

A single-file landing page for The City Language Academy (Kamra Kalan, Pakistan) covering IELTS, TOEFL iBT, PTE Academic, Cambridge English and the Duolingo English Test, with an online enrollment form that emails each request to you through [EmailJS](https://www.emailjs.com).

Everything lives in `index.html` (HTML, CSS and JavaScript in one file), so it deploys anywhere with no build step.

---

## 1. Connect the enrollment form (EmailJS)

The form sends enrollment requests straight to your inbox using EmailJS. This runs fully in the browser, so no server is needed. Free tier allows a few hundred emails per month.

### Step by step

1. Create a free account at **https://www.emailjs.com**.
2. **Add an email service**: dashboard → *Email Services* → *Add New Service* (Gmail works well for `nafehawan94@gmail.com`). Copy the **Service ID**.
3. **Create a template**: dashboard → *Email Templates* → *Create New Template*.
   - In the template **To email** field, put your address: `nafehawan94@gmail.com` (or use `{{to_email}}`).
   - In **Reply-To**, put `{{reply_to}}` so you can reply directly to the student.
   - Use these variables anywhere in the subject/body:
     ```
     Name:     {{from_name}}
     Email:    {{reply_to}}
     Phone:    {{phone}}
     Test:     {{program}}
     Batch:    {{schedule}}
     Message:  {{message}}
     ```
   - Copy the **Template ID**.
4. Get your **Public Key**: dashboard → *Account* → *General* → **Public Key**.
5. Open `index.html`, find the config block near the bottom (inside the last `<script>`), and paste your three values:
   ```js
   const EMAILJS_PUBLIC_KEY  = "YOUR_PUBLIC_KEY";
   const EMAILJS_SERVICE_ID  = "YOUR_SERVICE_ID";
   const EMAILJS_TEMPLATE_ID = "YOUR_TEMPLATE_ID";
   const NOTIFY_EMAIL        = "nafehawan94@gmail.com";
   ```

Until those are filled in, the form validates input and shows a friendly "not connected yet" message instead of failing silently.

---

## 2. Before you publish — replace the placeholders

Search `index.html` for these and update them with real details:

- **Phone number** — currently `+92 000 0000000` (in the contact section and the `tel:` link).
- **Email address** — currently `info@thecitylanguageacademy.com`.
- **Class hours** — currently `Monday to Saturday, 9:00 to 20:00`.
- **Testimonials** — the three student quotes are clearly marked sample content (`<!-- SAMPLE testimonials -->`). Swap in real names and quotes, or remove any you cannot verify. Avatars are auto-generated initials, so there are no photos to add.
- **Hero band goal** — the hero card shows a `7.5` target as an example. Adjust it if you prefer a different headline number.
- **Photos** — the hero, the IELTS card, the "why us" panel and the "Inside the academy" gallery load real photos from `loremflickr.com` (topical stock imagery). These are placeholders so the layout looks complete now. **Replace them with your own photos** of the academy, classes and students before publishing: search `index.html` for `loremflickr.com` and swap each URL for your image path (e.g. `images/classroom.jpg`). Every photo sits over a brand-coloured gradient with a solid colour behind it, so if an image is ever slow or missing you get a coloured panel, never a blank box.

The Google Map already points at the academy address on Qutba Road, Kamra Kalan.

---

## 3. Publish it

Any static host works. Two easy options:

**GitHub Pages**
1. Push this repo to GitHub.
2. Repo *Settings* → *Pages* → set the branch to your published branch and folder to `/ (root)`.
3. Your site goes live at `https://<username>.github.io/<repo>/`.

**Netlify / Vercel / Cloudflare Pages**
- Drag the folder in, or connect the repo. No build command needed; the output is `index.html` itself.

To preview locally, just open `index.html` in a browser, or run a tiny server:
```bash
python3 -m http.server 8000    # then visit http://localhost:8000
```

---

## Design notes

- **One locked light theme**, a single burnt-coral accent used consistently, Bricolage Grotesque + Instrument Sans type.
- **Motion** is scroll-reveal plus hover feedback only, and it respects `prefers-reduced-motion`.
- **Accessibility**: labels sit above every input, focus rings are visible, and buttons meet contrast targets.
- Fonts are linked from Google Fonts for single-file convenience. For maximum performance you can self-host them later.
