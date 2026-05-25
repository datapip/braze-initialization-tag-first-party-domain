# Braze Web SDK Initialization Tag for Google Tag Manager (First-Party Domain)

[![GTM Template](https://img.shields.io/badge/GTM-Web_Template-blue.svg)](https://tagmanager.google.com/)
[![License](https://img.shields.io/badge/License-Apache_2.0-green.svg)](https://opensource.org/licenses/Apache-2.0)
[![Maintained by](https://img.shields.io/badge/Maintained_by-datapip.de-orange.svg)](https://datapip.de)

This custom Web Google Tag Manager (GTM) tag template simplifies loading and initializing the **Braze Web SDK** through a custom tracking endpoint (First-Party Domain). By routing the SDK fetch through your own subdomain, you significantly improve data quality and bypass client-side privacy filters.

*This template is based on the official Braze GTM Tag and has been enhanced to natively support structured proxy endpoints.*

---

## 🚀 The Core Problem: Data Loss via Third-Party CDNs
Standard tracking scripts loaded via public CDNs (`js.appboycdn.com`) are heavily blocked by modern privacy browsers (Brave, Safari) and standard ad-blocking extensions. This leads to **15% to 40% data loss** in your behavioral marketing automation and user analytics.

By routing the SDK request through your own infrastructure (e.g., `data.yourdomain.com`), the script loading context becomes **First-Party**, making it invisible to standard blacklists.

---

## 🛠️ Installation & GTM Setup

### 1. Import the Template
1. Download the `template.tpl` file from this repository.
2. In your Web GTM Container, navigate to **Templates** -> **Tag Templates** -> Click **New**.
3. Click the three vertical dots in the top-right corner and select **Import**.
4. Choose the `template.tpl` file and click **Save**.

### 2. Configure Tag Fields
Create a new Tag using this template and fill out the configuration fields:
* **Braze API Key:** Your official Braze App Group API Key.
* **Custom Tracking Domain (Base URL):** Enter your custom sGTM domain environment (e.g., `data.yourdomain.com`). Do **not** include `https://`.
* **SDK Version:** Specify the target Web SDK v6 version (e.g., `6.7`).

The tag automatically calculates the dynamic asset path and loads the required SDK layer:
`https://data.yourdomain.com/web-sdk/6.7/braze.no-amd.min.js`

### 3. Important: Update GTM Template Permissions
Because GTM enforces a strict Content Security Policy (CSP) inside custom templates, you **must** allow your custom domain to be injected:

1. Go to **Templates** -> **Tag Templates** and click on **Braze Initialization Tag with First-Party Domain** to open the editor.
2. Click on the **Permissions** tab at the top.
3. Find the **Inject Scripts** permission row and click to expand it.
4. Under **Allowed URL Matches**, add your custom domain with a wildcard at the end so GTM is allowed to load the script:
   `https://data.yourdomain.com/web-sdk/*`
5. Click **Save** in the top-right corner.

*Note: If you skip this step, GTM will throw a console error (`Permission denied to inject script`) and the Braze SDK will not load.*

---

## 🔒 Required: The Server-Side Proxy Client

> **This Web GTM Tag only handles the frontend initialization.** 
> To serve the script files and correctly route the backend tracking requests (`/api/v3/` endpoints), you require a matching server-side architecture inside your server-side Google Tag Manager (sGTM) container.

To handle the server-side traffic validation, security hardening, and endpoint mapping, you can deploy our production-ready [**Braze sGTM Proxy Client**](https://datapip.gumroad.com/l/braze-sgtm-proxy).

### Why you need the sGTM Companion Client:
* **Complete SDK Delivery:** Streams `braze.min.js` (and `.map` debugging assets) directly from your server container.
* **Endpoint Proxying:** Securely forwards `/api/v3/` tracking requests, session beacons, content cards, and feature flags straight to your regional Braze API cluster.
* **Security Hardening:** Includes enterprise-level origin allowlisting (CORS restriction) and explicit API Key validation to prevent malicious unauthorized endpoint abuse.

👉 **[Get the production-ready Braze sGTM Proxy Client on Gumroad](https://datapip.gumroad.com/l/braze-sgtm-proxy)**


---

## ⚖️ License & Attribution
This project is based on the official [Braze GTM Tag](https://github.com/braze-inc/braze-gtm-tag), Copyright Braze, Inc. It is modified and distributed under the terms of the **Apache License 2.0**. 

*Disclaimer: This is an unofficial community integration. It is not affiliated with, endorsed by, or supported by Braze, Inc. Braze™ is a trademark of Braze, Inc.*

---

## 💼 Need Support?
Need professional help with implementation or custom tracking? – Contact me directly via  [datapip.de](https://datapip.de)