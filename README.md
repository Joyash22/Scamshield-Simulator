
# ScamShield Simulator 🛡️

An AI-powered, browser-based fraud awareness simulator that teaches users how to identify and avoid online scams through realistic, game-based scenarios and a live machine learning detection engine.

---

## Features

- 10 interactive scam scenarios — email, WhatsApp, SMS, phone calls, pop-ups, Telegram, and Instagram DMs rendered as realistic UI mockups
- TensorFlow.js ML engine — a neural network trained in the browser that classifies scam text in real time
- Live scam detector — paste any suspicious message and get instant ML-powered analysis with confidence scores and red flag breakdown
- AI chatbot assistant — answers questions about OTP fraud, phishing, UPI scams, investment fraud, and more
- Score and badge system — earn points for correct decisions, lose points for mistakes, unlock achievement badges
- Per-scenario ML confidence — after each answer, the model shows its own probability estimate alongside your feedback
- Session analytics dashboard — scam detection rate, average model confidence, per-category accuracy breakdown
- Fully offline — runs entirely in the browser with no backend, no API keys, no installation

---

## Tech Stack

UI: Vanilla HTML, CSS, JavaScript
ML / AI: TensorFlow.js 4.15.0 (loaded from CDN)
Model architecture: Dense(32, ReLU) → Dropout(0.2) → Dense(16, ReLU) → Dense(1, Sigmoid)
Training: In-browser, synthetic dataset of 30 scam + 30 legit messages
Features: 20 hand-engineered text features (urgency, credentials, fees, domains, etc.)
Chatbot: Rule-based keyword matching with curated responses
Hosting: Any static file server or direct browser open

---

## Getting Started

Option 1 — Open directly in browser

Just double-click scamshield_simulator.html in your file manager. No server required. The TensorFlow.js model trains itself in the browser on first load (takes 1–2 seconds).

Option 2 — Serve locally

Using Python:
python -m http.server 8000

Using Node.js:
npx serve .

Then open http://localhost:8000/scamshield_simulator.html

Option 3 — Deploy to GitHub Pages / Netlify / Vercel

Just upload the single HTML file. No build step, no dependencies, no configuration.

---

## Project Structure

scamshield_simulator.html — Everything in one file
README.md — This file

The entire application is self-contained in a single HTML file:

scamshield_simulator.html
  style tag      — CSS: dark theme, layout, component styles
  body tag       — HTML: home, game, and results screens
  script tag
    ML Engine    — TensorFlow.js model build, train, inference
    Features     — 20-feature text extractor
    Chatbot      — Keyword-based scam Q&A assistant
    Scenarios    — 10 scenario definitions with renders and feedback
    Game Logic   — Screen routing, scoring, results, ML dashboard

---

## ML Engine Details

Model Architecture:

Input (20 features)
  → Dense(32, activation=relu)
  → Dropout(rate=0.2)
  → Dense(16, activation=relu)
  → Dense(1, activation=sigmoid)
  → Output: scam probability between 0 and 1

Compiled with adam optimizer and binaryCrossentropy loss. Trained for 80 epochs in-browser on page load.

Feature Engineering (20 features):

1.  Urgency language — "urgent", "immediately", "within N hours", "act now"
2.  Credential request — "otp", "password", "pin", "cvv", "card number"
3.  Payment language — "pay", "fee", "charge", "deposit", "transfer"
4.  Fake prize — "congratulations", "won", "winner", "lottery", "prize"
5.  Suspicious link — "click here", "click this", "follow link"
6.  Non-corporate email — gmail.com, yahoo.com, hotmail.com senders
7.  Indian currency — ₹, Rs., INR, lakh, crore
8.  Verification ask — "verify", "confirm", "update", "validate"
9.  Unrealistic promise — "free", "guaranteed", "no risk", "100%", "double your"
10. Bank threat — "bank", "account", "blocked", "suspend", "deactivated"
11. Document request — "aadhaar", "pan card", "passport", "kyc"
12. Investment claim — "invest", "earn", "profit", "scheme", "roi"
13. Suspicious URL — HTTP links not matching known legitimate domains
14. Long message — Text length over 200 characters
15. All-caps words — More than 3 ALL-CAPS word clusters
16. Secrecy tactic — "don't tell", "secret", "between us", "confidential"
17. Upfront fee — "registration fee", "processing fee", "activation fee"
18. Remote access — "teamviewer", "anydesk", "remote access"
19. QR scam pattern — "qr code", "scan to receive", "scan money"
20. Job scam signals — "work from home", "no interview", "no experience"

Scam Type Classification — detects these categories:
- OTP / Bank fraud
- Job / Internship scam
- Lottery scam
- Investment fraud
- UPI / Payment scam
- Phishing
- Tech support scam
- Impersonation scam

---

## Scenarios

1.  Internship offer scam — Email — Beginner
2.  OTP phone scam — Phone call transcript — Beginner
3.  Fake UPI payment screenshot — WhatsApp chat — Intermediate
4.  Phishing email — Email with fake URL bar — Intermediate
5.  Fake job offer letter — Email — Beginner
6.  Lottery / prize scam — SMS — Beginner
7.  Tech support pop-up — Browser pop-up mockup — Intermediate
8.  QR code payment scam — WhatsApp chat — Expert
9.  Social media impersonation — Instagram DM — Intermediate
10. Investment / Ponzi scheme — Telegram group — Expert

---

## Scoring

Correct answer (all correct options selected): +100 points
Wrong answer: -30 points
Minimum score: 0 (never goes negative)

Achievement Badges:

🛡️ Perfect Shield — All 10 scenarios correct
👁️ Eagle Eye — 7 or more correct
🏆 Fraud Fighter — Score of 800 or above
⭐ Untouchable — Zero mistakes
🎯 On Track — 5 to 6 correct
📚 Learning — Participation badge

---

## Customization

Adding a new scenario — add an object to the scenarios array in the script section with these fields: id, title, tag, risk (0–100), diff (easy/med/hard), category, render function returning HTML string, options array, correct array of zero-indexed correct options, points, and a feedback object containing title, flags array, and learn string.

Improving the ML model — edit the scamTexts and legitTexts arrays inside buildMLModel() and increase epochs for higher accuracy. Current setting is 80 epochs.

Adding chatbot responses — add key-value pairs to the chatResponses object where the key is the trigger word and the value is the response string.

---

## Browser Compatibility

Chrome 90+: Full support
Firefox 88+: Full support
Safari 14+: Full support
Edge 90+: Full support
Mobile Chrome / Safari: Full support, responsive layout

Requires JavaScript enabled. TensorFlow.js uses WebGL acceleration when available, falls back to CPU automatically.

---

## Educational Purpose

Every scenario teaches warning signs (specific red flags to look for), verification methods (how to check legitimacy independently), safe practices (what to do and not do), and real consequences (what happens if you fall for the scam).

Fraud Reporting Resources for India:
- National Cyber Crime Portal: cybercrime.gov.in
- Cyber Fraud Helpline: 1930
- SEBI (Investment fraud): sebi.gov.in
- RBI Ombudsman: rbi.org.in

---

## License

MIT License — free to use, modify, and distribute for educational purposes.

---

## Author

Built with HTML, CSS, JavaScript, and TensorFlow.js.
Designed for students, job seekers, senior citizens, and general internet users.