# ETS SF Website

Static website (HTML, CSS, JavaScript). English and French. Login with email/password and Google
(Supabase Auth). Quote and contact forms (Netlify Forms). No build step.

## Structure
```
index.html        page shell + hidden Netlify form definitions
css/style.css     all styles
js/config.js      THE ONLY FILE YOU EDIT: phone, email, WhatsApp, address, social, Supabase keys
js/data.js        photos map, projects, English and French text
js/app.js         pages, navigation, forms, login
images/           photos and logo (replace a file, keep its name)
vendor/           Supabase client (MIT licence included)
netlify.toml      Netlify settings and headers
```

## Run locally
`npm start` (or `python3 -m http.server 3000`) then open http://localhost:3000
Forms only send once the site is on Netlify. Login works once Supabase is configured (below).

## Push to Git
This folder is already a Git repository with the first commit made. Create an empty repository on GitHub, then:
```
git remote add origin https://github.com/YOUR-USER/ets-sf-website.git
git push -u origin main
```
(If the .git folder is missing: `git init -b main && git add . && git commit -m "ETS SF website"` first.)

## Deploy on Netlify
1. Netlify > Add new site > Import from Git > choose the repo.
2. Build command: leave empty. Publish directory: `.`  Deploy.
3. Forms > Form notifications > add the ETS SF email (forms `contact` and `quote` appear after the first deploy).
Quick option without Git: drag this folder onto https://app.netlify.com/drop

## Turn on login (Supabase, free)
1. https://supabase.com > New project.
2. Authentication > Providers > Email: enabled.
3. Authentication > URL Configuration: set Site URL to your Netlify address and add it (and http://localhost:3000) to Redirect URLs.
4. Google: in Google Cloud Console > APIs & Services > Credentials, create an OAuth client (Web).
   Authorized redirect URI: `https://YOUR-PROJECT-REF.supabase.co/auth/v1/callback`.
   Paste the Client ID and Secret in Supabase > Authentication > Providers > Google.
5. Supabase > Project Settings > API: copy the Project URL and the anon public key into `js/config.js`
   (`supabaseUrl`, `supabaseKey`). The anon key is meant to be public.
6. Commit and push. Until the keys are set, the login page shows "Sign-in is not set up yet."

Signed-in users get their email and name prefilled in the forms. Accounts are managed in Supabase > Authentication > Users.

## Adding company details later
Everything is in `js/config.js`. Leave a value empty and that item is simply not shown.
- Contact: `phone`, `whatsapp`, `email`, `address`, `mapsEmbed`, `facebook`, `instagram`
- Text: `history_en/fr`, `mission_en/fr`, `vision_en/fr`, `standards_en/fr`, `area_en/fr`
- Photos: replace files in `images/` and keep the names.
- `showIllustrativeLabel:true` puts an "Illustrative example" tag on every photo.
- After you have a domain, add a `sitemap.xml` and a Sitemap line in `robots.txt`.
The login icon appears in the header once `supabaseUrl` and `supabaseKey` are set.

## Notes
- Icons: Font Awesome Free (CC BY 4.0), inlined as SVG.
- Do not claim fire, weather or warranty performance on the Materials page without supplier data.
