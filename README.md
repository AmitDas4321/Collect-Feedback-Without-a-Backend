<h1 align="center">Backendless Feedback Page</h1>

<p align="center">
  Collect feedback or form submissions <b>without any backend</b> — using your Google Form as a hidden data collector.
</p>

---

## 🧩 Overview

This project shows how to connect your website’s HTML form directly to a **Google Form** without needing a backend server.  
Your custom HTML form silently submits user data to Google’s form endpoint, and responses appear in your linked Google Sheet.

---

## 🪜 Step 1 — Create a Google Form

1. Go to [Google Forms](https://forms.google.com) and create your form.  
2. Add a few questions — for example:
   - “Why did you uninstall?”  
   - “Your email (optional)”
3. Once your form is ready, click the **Send** button (top right) → copy the **link**.

Your form link will look like this:

```

https://docs.google.com/forms/d/e/1FAIpQLBuB4ibr8e9OObakx7_bJTx9DR4EN1EFdil7MIuSvW_eXjVS_2/viewform

```

Here, your **Form ID** is:
```

1FAIpQLBuB4ibr8e9OObakx7_bJTx9DR4EN1EFdil7MIuSvW_eXjVS_2

```

---

## 🧩 Step 2 — Build the Form Endpoint

Once you have the Form ID, your **submission URL** should be:

```

https://docs.google.com/forms/d/e/1FAIpQLBuB4ibr8e9OObakx7_bJTx9DR4EN1EFdil7MIuSvW_eXjVS_2/formResponse

````

> Note the difference:
> - `/viewform` → is for filling the Google Form UI  
> - `/formResponse` → is the endpoint you’ll use in your own website form  

---

## 💻 Example HTML Code

Here’s an example of how to use that Form ID inside your custom HTML form:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Feedback Form</title>
</head>
<body>
  <h2>We value your feedback 💬</h2>

  <form id="feedback-form"
        action="https://docs.google.com/forms/d/e/1FAIpQLBuB4ibr8e9OObakx7_bJTx9DR4EN1EFdil7MIuSvW_eXjVS_2/formResponse"
        method="POST"
        target="hidden_iframe"
        enctype="text/plain">

    <label for="entry.1727297528">Why did you uninstall?</label><br>
    <textarea id="entry.1727297528" name="entry.1727297528" placeholder="Your answer..." required></textarea><br>

    <label for="entry.1112510081">Your Email (optional)</label><br>
    <input type="email" id="entry.1112510081" name="entry.1112510081" placeholder="you@example.com"><br>

    <!-- Hidden field for browser info -->
    <input type="hidden" name="entry.280742688" id="entry.280742688">

    <input type="submit" value="Submit">
  </form>

  <iframe name="hidden_iframe" style="display:none;"></iframe>

  <p id="thank-you" style="display:none;">✅ Thank you! Your feedback has been submitted.</p>

  <script>
    const form = document.getElementById('feedback-form');
    form.addEventListener('submit', () => {
      document.getElementById('entry.280742688').value = navigator.userAgent;
      setTimeout(() => {
        form.style.display = 'none';
        document.getElementById('thank-you').style.display = 'block';
      }, 400);
    });
  </script>
</body>
</html>
````

---

## 🧠 Notes

* Replace the **entry IDs** (`entry.1727297528`, `entry.1112510081`, etc.) with your own from the Google Form’s source.
* Always use `/formResponse` instead of `/viewform`.
* You can add hidden fields for browser info, page URL, or timestamp.

---

## ✅ Example Output

* When a user submits the form, the data is instantly stored in your Google Form’s **Responses → Spreadsheet** tab.
* No server, no API key, no database required.

---

## 🧾 License

Released under the **MIT License** — free to use and modify.

---

## 👨‍💻 Author

| [<img src="https://avatars.githubusercontent.com/u/112541611?v=4" width="60" alt="Amit Das"/>](https://amitdas.site) |
| :------------------------------------------------------------------------------------------------------------------: |
|                                           [Amit Das](https://amitdas.site)                                           |

---

---

> 💬 *Collect feedback directly in Google Sheets — no backend, no form embedding, 100% client-side.*
