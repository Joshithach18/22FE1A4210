# URL Shortener Backend (TypeScript + Express)

This is a backend implementation for a URL shortener service built with **TypeScript**, **Express**, and an in-memory store.  
It includes support for generating short links, redirecting, tracking clicks, and sending logs to the AffordMed evaluation server.

---

## ⚠️ Important Note
I could not obtain the **ClientID** and **ClientSecret** from the AffordMed evaluation server at the start, so I was not able to fully perform and test the **logging functionality** against their API.  

I hope the provided code works as expected once valid credentials are supplied.

---

## 📂 Project Structure
backend/
├── src/
│ ├── index.ts # Main entrypoint (Express server + routes)
│ ├── logging.ts # Handles log sending to AffordMed evaluation server
│ ├── store.ts # In-memory storage for URLs & click tracking
│ ├── validators.ts # Input validation helpers
│ └── types.ts # Shared TypeScript types
├── .env.example # Example environment variables
├── tsconfig.json # TypeScript config
├── package.json # Dependencies & scripts
└── README.md # Project documentation



---

## ⚙️ Setup Instructions

1. **Clone the repository**  
   ```bash
   git clone <repo-url>
   cd backend
   ```
2. **Install dependencies**
```bash
npm install
```
3. **Environment variables**

```bash
PORT=3000

AM_EMAIL=your_college_email@xyz.edu
AM_NAME=Your Name
AM_ROLLNO=Your RollNo
AM_ACCESS_CODE=code_from_affordmed

AM_CLIENT_ID=your_client_id   # not available to me
AM_CLIENT_SECRET=your_secret  # not available to me
```
4. **Run the development server**
```
npm run dev
```

** API Endpoints**
Create a short URL

POST /shorturls
```
{
  "url": "https://example.com/very/long/link",
  "validity": 30,
  "shortcode": "abcd1"
}
```

Response
```
{
  "shortLink": "http://localhost:3000/abcd1",
  "expiry": "2025-09-04T12:00:00.000Z"
}
```

Redirect to original URL

GET /:shortcode → redirects to the original URL and records click info.

Get stats for a short URL

GET /shorturls/:shortcode

Returns click count, original URL, expiry, and list of clicks.

📝 Logging

The logging.ts module automatically obtains a token from the AffordMed evaluation server and sends logs for every action.

⚠️ Due to missing credentials, I couldn’t verify this end-to-end. Once valid ClientID/Secret are provided, logging should work as expected.

## Conclusion

Core shortener functionality is implemented and tested locally.

Logging code is in place but untested (needs valid AffordMed credentials).

I hope the evaluators can confirm that the solution works as intended once configured.
