# TrendBite Services – Zero‑budget SMM panel

This repository contains the code for **TrendBite Services**, a mobile‑first social media marketing panel built entirely on free tiers. It lets visitors browse a catalog of services, place orders that open a pre‑filled WhatsApp message and (optionally) logs orders into a Google Sheet via a lightweight Apps Script web app.

## Live site

After pushing this repository and enabling hosting, the site will be available at:

```
<LIVE_SITE_URL>
```

Replace `<LIVE_SITE_URL>` above with the actual deployment link (e.g. `https://your-subdomain.vercel.app` or GitHub Pages URL) once you’ve deployed.

## Sheets & API endpoints

For logging and exposing data the panel uses Google Sheets. Create the following sheets under your Google account:

| Sheet | Purpose | Required columns |
|------|---------|-----------------|
| **Services** | Holds catalog of available services. Published as CSV/JSON for the front‑end to consume. | `id`, `service`, `category`, `price`, `min`, `max`, `avg`, `desc` |
| **Orders** | Records submitted orders. | `ts`, `name`, `link`, `qty`, `serviceId`, `price`, `eta`, `status` |
| *Optional* **Leads** | Captures exit‑intent leads. | `ts`, `number`, `status` |

You can publish the **Services** sheet as a CSV/JSON feed (File → Share → Publish to web) and update the `services.json` fetch URL in `app.js` accordingly. The **Orders** sheet should be connected via a Google Apps Script Web App that appends rows on `POST` requests. Paste the web app URL into the `YOUR_APPS_SCRIPT_URL` placeholder in `app.js`.

### Example endpoints

- **Services CSV/JSON:** `https://docs.google.com/spreadsheets/d/<SERVICES_SHEET_ID>/gviz/tq?tqx=out:csv`
- **Orders append Web App:** `https://script.google.com/macros/s/<DEPLOYMENT_ID>/exec`

Once created, share the **Services** sheet as “Anyone with the link – Viewer” so the front‑end can fetch it. The **Orders** sheet doesn’t need to be public because the Apps Script will write to it.

## Customisation

- **WhatsApp number** – Replace `+923193840214` with your own number in the WhatsApp URL in `index.html` and the `app.js` WhatsApp link builder.
- **Colours & logo** – Update colours in `styles.css` or add your own logo image into `public/assets` and reference it in `index.html`.
- **Analytics** – Uncomment the Google Analytics or Cloudflare snippet in `index.html` and set your measurement ID.
- **Chat widget** – Replace `PROPERTY_ID` in the Tawk.to embed snippet in `index.html` with your own Tawk property ID.

## Deploying

1. **Push this code to your repository.** After cloning the repo locally, run `npm install` if you add any build tooling (not necessary for this plain HTML/JS site). Commit and push to the `main` branch.
2. **Enable hosting:**
   - **GitHub Pages:** Go to your repository’s *Settings → Pages*, select `main` branch and root directory, then click *Save*. Your site will be served at `https://<your-username>.github.io/<repo-name>/` within a few minutes.
   - **Vercel/Netlify/Cloudflare Pages:** Import this repository in the hosting dashboard and deploy. Choose “static” or “HTML” framework. The default build command is not required.
3. **Update the live site URL in this README**.

## Transferring ownership

- To move the repository to your own GitHub account, go to *Settings → Transfer ownership* and follow the prompts.
- For the Sheets, open the sheet and click *Share → Transfer ownership* to your Google account.
- If using Vercel/Netlify, add your own account as a collaborator on the project, then remove this account once you’ve cloned the project.

## A note on the Google Sheet example

This repository includes a `services.json` file with example data so the site works out‑of‑the‑box. For production you should publish a real **Services** sheet and update `app.js` to fetch it instead of the local JSON. Similarly, update the `YOUR_APPS_SCRIPT_URL` placeholder so orders and leads are logged.

---

**TrendBite Services** – Affordable, fast social media growth with a friendly WhatsApp checkout. Built with ❤️ on free tiers.
