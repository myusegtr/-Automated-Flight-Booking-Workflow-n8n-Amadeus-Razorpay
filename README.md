# -Automated-Flight-Booking-Workflow-n8n-Amadeus-Razorpay

## 📌 Aim of the Project

This project is an end-to-end automated flight search and payment workflow built using n8n, **powered by the Amadeus Flight API** for fetching flight options and Razorpay for generating instant payment links.
The workflow takes user input via Webhook, searches flights, formats the best results, prepares payment, emails the customer, and responds back programmatically.

## 🛠️ Tools & Technologies Used

**n8n (Workflow automation platform)**

**Amadeus Self-Service API (Flight offers search)**

**Razorpay API (Payment link generation)**

**SMTP Email (Gmail / Outlook / SendGrid)**

**Webhook Trigger (Incoming POST request)**


## 🚀 Project Features

**Live flight search using Amadeus API**

**Automatic token generation using OAuth2**

**Clean formatting of flight results**

**Razorpay payment link auto-creation**

**Email delivery of payment link**

**Webhook-based request–response cycle**

**Fully automated booking workflow**


## 🗂️ Workflow Structure (n8n)

```bash
├── Webhook (POST /flight-search)
├── Workflow Configuration (API credentials)
├── Amadeus – Get Token
├── Amadeus – Search Flights
├── Format Flights (JavaScript)
├── Prepare Payment Data
├── Create Payment Link (Razorpay)
├── Send Payment Email (SMTP)
└── Respond to Webhook




## 🧱 Steps to Build the Workflow
## 🛠️ 1. Configure Workflow Credentials

Open the Workflow Configuration node and fill the following:

| **Parameter**           | **Value**                        |
| ------------------- | ------------------------------------ |
| amadeusClientId     | Your Amadeus Client ID               |
| amadeusClientSecret | Your Amadeus Client Secret           |
| razorpayKeyId       | Razorpay Key ID                      |
| razorpaySecret      | Razorpay Key Secret                  |
| fromEmail           | The email used to send payment links |



## 🔑 2. Setup Razorpay API (Create Payment Link Node)

Authentication Type: Basic Auth

Username → razorpayKeyId

Password → razorpaySecret

The API used:
```bash
POST https://api.razorpay.com/v1/payment_links


## 📧 3. Setup SMTP Email (Send Payment Email Node)

## Configure:

SMTP Host → e.g., smtp.gmail.com

Username → Your email

Password → App Password (recommended)

Port → 465 (SSL) or 587 (TLS)

From → Same as fromEmail parameter


🌐 4. Set Up Webhook Trigger

Webhook URL format:

https://<your-workspace>.app.n8n.cloud/webhook/flight-search


This endpoint receives flight search requests.




🧪 Testing the Workflow

Send a POST request using Postman or CURL:

URL

https://<your-workspace>.app.n8n.cloud/webhook/flight-search


Request Body

{
  "origin": "DEL",
  "destination": "BOM",
  "departureDate": "2024-12-25",
  "adults": "1",
  "email": "customer@example.com"
}

🟢 Expected Flow Behavior

Amadeus generates access token

Flight search is performed

Best flight option is extracted

Razorpay payment link is created

Email with payment link is delivered

Webhook returns:

{
  "status": "Payment link sent successfully",
  "email": "customer@example.com"
}

🔐 Authentication Details
Amadeus

Uses OAuth2 Client Credentials

Base URL:

https://test.api.amadeus.com

Razorpay

Uses Basic Auth

Amount must be in paise (INR × 100)

SMTP Email

Recommended: Use App Password (secure)

🔬 Advanced Testing Scenarios
✅ Test Cases

“Search for flights from BLR to HYD for Jan 10, 2025”

“2 adults, DEL → GOI, return date required”

“Send payment link again if previous payment failed”

🎯 Enterprise-Grade Enhancements (Future Add-Ons)
Feature	Description
✈️ Return Flight Support	Add round-trip search in Amadeus
💬 WhatsApp Notification	Send payment link via WhatsApp Cloud API
📊 Logging	Log all flight searches in Google Sheets / Notion
🔁 Retry Logic	Re-run flight search if user rejects results
🧾 PDF Invoice	Auto-generate invoice after payment success
🔔 Payment Status Webhook	Automatically detect payment success/failure





