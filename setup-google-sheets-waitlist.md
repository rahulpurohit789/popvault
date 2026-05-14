# PopVault — Google Sheets Waitlist Setup

**5-minute setup.** No backend, no monthly cost, unlimited submissions, all data lives in a Google Sheet you own.

## How it works

```
User submits form on popvault.com
        ↓
   POST to Google Apps Script Web App URL
        ↓
   Apps Script appends a row to your Sheet
        ↓
   You open your Sheet and see every signup, sorted by time
```

---

## Step 1 — Create the Google Sheet

1. Open **[sheets.google.com](https://sheets.google.com)** → click **Blank**
2. Rename the sheet (top-left) to **`PopVault Waitlist`**
3. In **row 1**, add these column headers exactly:

   | A | B | C | D | E |
   |---|---|---|---|---|
   | Timestamp | Email | Source (USD/INR/JPY) | Referrer | User Agent |

4. Optional: bold the header row → **View → Freeze → 1 row**

---

## Step 2 — Add the Apps Script

1. From the same Sheet: **Extensions → Apps Script**
2. Delete whatever's in the default `Code.gs` file
3. Paste the entire snippet below:

```javascript
// PopVault waitlist endpoint — appends form submissions to this Sheet.
// Deployed as a Web App with "Anyone" execute access so the public form can POST.

const SHEET_NAME = 'Sheet1'; // change if you renamed the tab

function doPost(e) {
  try {
    const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName(SHEET_NAME)
                  || SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    const p = e.parameter || {};

    sheet.appendRow([
      new Date(),
      (p.email || '').toString().trim().toLowerCase(),
      p.source || '',
      p.referrer || '',
      (e.parameter && e.parameter.userAgent) || ''
    ]);

    return ContentService
      .createTextOutput(JSON.stringify({ ok: true }))
      .setMimeType(ContentService.MimeType.JSON);
  } catch (err) {
    return ContentService
      .createTextOutput(JSON.stringify({ ok: false, error: String(err) }))
      .setMimeType(ContentService.MimeType.JSON);
  }
}

// Health check — visit your Web App URL in a browser to see "ok"
function doGet() {
  return ContentService
    .createTextOutput(JSON.stringify({ ok: true, app: 'PopVault waitlist' }))
    .setMimeType(ContentService.MimeType.JSON);
}
```

4. **File → Save** (or ⌘S). Name the project **`popvault-waitlist`**.

---

## Step 3 — Deploy as a Web App

1. Top right → **Deploy → New deployment**
2. Click the ⚙️ gear next to "Select type" → **Web app**
3. Fill in:
   - **Description:** `PopVault waitlist`
   - **Execute as:** `Me (your@email.com)`
   - **Who has access:** `Anyone` ⚠️ this is important — without it, the form can't POST
4. Click **Deploy**
5. Google will ask you to **Authorize access** → click through → choose your Google account → click **Advanced → Go to popvault-waitlist (unsafe)** → **Allow** (it says "unsafe" because the script is unverified; it's your own code, it's fine)
6. Copy the **Web app URL** that appears. It looks like:
   ```
   https://script.google.com/macros/s/AKfycby...long...string/exec
   ```

---

## Step 4 — Wire it into popvault.html

Open `index.html` (or `popvault.html`) and find this line:

```html
<form class="wl-form" id="wlForm" action="https://script.google.com/macros/s/YOUR_SCRIPT_ID/exec" method="POST" novalidate>
```

Replace **`YOUR_SCRIPT_ID`** with everything between `/s/` and `/exec` from the URL you just copied.

Example: if your URL is
`https://script.google.com/macros/s/AKfycbyABC123xyz/exec`

then the action becomes:
`https://script.google.com/macros/s/AKfycbyABC123xyz/exec`

Save. Re-deploy your site (push to GitHub / re-upload to Vercel / Netlify).

---

## Step 5 — Test it

1. Open your live site
2. Submit a test email through the waitlist form
3. Open your `PopVault Waitlist` Sheet
4. New row should appear within ~2 seconds with timestamp, email, currency they viewed, referrer

If it doesn't appear:
- Open browser DevTools → Network tab → submit again → look for the `script.google.com` request. If you see a CORS error, double-check that the deployment's "Who has access" is set to **Anyone** (not "Anyone with Google account").
- Visit your Web App URL directly in a browser. You should see `{"ok":true,"app":"PopVault waitlist"}`. If not, the Apps Script wasn't deployed correctly — redo Step 3.

---

## Bonus features you can add later

**Email yourself on every signup:**
Add this inside `doPost` before the return:
```javascript
MailApp.sendEmail({
  to: 'support@weseegpt.com',
  subject: 'New PopVault waitlist signup: ' + (p.email || ''),
  body: 'Email: ' + (p.email || '') + '\nSource: ' + (p.source || '') + '\nReferrer: ' + (p.referrer || '')
});
```

**Auto-respond with a confirmation email:**
```javascript
if (p.email) {
  MailApp.sendEmail({
    to: p.email,
    subject: 'You\'re on the PopVault waitlist',
    htmlBody: '<h2>Welcome to the Vault.</h2><p>You\'re in. We\'ll notify you the moment your Royal Pop colorway is ready.</p><p>— PopVault</p>'
  });
}
```
*Note: Apps Script free tier allows ~100 sent emails/day.*

**Block duplicate emails:**
```javascript
const existing = sheet.getRange('B:B').getValues().flat().map(s => s.toLowerCase());
if (existing.includes(p.email.toLowerCase())) {
  return ContentService.createTextOutput(JSON.stringify({ ok: true, duplicate: true })).setMimeType(ContentService.MimeType.JSON);
}
```

**View the sheet on mobile:**
- Install the **Google Sheets app** → your `PopVault Waitlist` sheet is there
- Or: **File → Share → Get shareable link** → bookmark it on your phone

---

## Privacy & GDPR notes

- Add a tiny privacy line under the form: *"We'll only email you about Royal Pop drops. Unsubscribe anytime."*
- If you collect EU/UK/India users at scale, eventually move to a real email tool (Klaviyo free tier is generous).

---

*Setup time: ~5 minutes. Cost: ₹0. Submission limit: unlimited.*
