# LocalAI-agent
Eliminates missed calls for small businesses — AI answers every inbound call, collects booking details naturally, and logs to Airtable in real time. Zero code. Under $10/month.



# 📞 LocalIQ AI — Voice Receptionist Pipeline

> An AI receptionist that answers inbound calls 24/7, books appointments 
> conversationally, and logs every booking to a live dashboard automatically.
> Built and deployed in 72 hours. Zero code written.

![Built with Retell AI](https://img.shields.io/badge/Built%20with-Retell%20AI-blue?style=flat-square)
![ElevenLabs](https://img.shields.io/badge/Voice-ElevenLabs-purple?style=flat-square)
![Twilio](https://img.shields.io/badge/Phone-Twilio-red?style=flat-square)
![Status](https://img.shields.io/badge/Status-Live-brightgreen?style=flat-square)

---

## 🚨 The Problem

Independent salons and gyms miss 30–40% of inbound calls daily.
The owner is with a client. The phone rings. Nobody answers.
That missed call is a lost booking — and lost revenue.

Hiring a receptionist costs $35,000–$50,000/year.
An answering service costs $500–$1,500/month and still misses calls.

**This system answers every call, every time — for under $10/month.**

---

## 📊 Business Outcomes

| Metric | Before | After |
|--------|--------|-------|
| Missed calls after hours | 30–40% | 0% |
| Booking availability | Business hours only | 24/7/365 |
| Time to book appointment | 3–5 min (human) | 90 seconds (AI) |
| Data entry to calendar | Manual | Automatic |
| Monthly cost | $500–$1,500 | Under $10 |
| Languages supported | 1 | 5 |
| Build time | Weeks (hiring) | 72 hours |

---

## 🎯 Live Demo

**Call right now:** +1 267 214 3027

Ask to book a hair appointment. Joyce will handle the entire 
conversation and log your booking automatically.

---

## ⚙️ How It Works

Inbound call hits Twilio phone number (+1 267 214 3027)
↓
Retell AI routes call to Joyce (AI voice agent)
↓
ElevenLabs (Rita voice) handles natural conversation
↓
Joyce collects: name → service → date → time → phone
↓
BookAppointment function fires automatically
↓
Make.com webhook receives booking data
↓
Airtable creates new record instantly
↓
Business owner sees booking on live dashboard in real time

---

## 🛠 Tech Stack

| Tool | Role |
|------|------|
| Retell AI | Voice agent platform — hosts Joyce |
| ElevenLabs (Rita voice) | Natural voice synthesis |
| Twilio | Real US phone number + SIP trunking |
| Make.com | Post-call webhook automation |
| Airtable | Booking database + live owner dashboard |

**Monthly cost: under $10 for a small business**

---

## 🧠 Joyce's System Prompt — 8 Steps

Joyce follows a strict conversation flow — one question at a time,
never robotic, always warm:

1. Greet the caller warmly
2. Ask for their name
3. Ask what service they need
4. Ask for their preferred date
5. Ask for their preferred time
6. Say exactly: *"Perfect! Let me get that booked for you right now."*
7. Fire BookAppointment function immediately — mandatory, never skip
8. Confirm booking and close warmly



---

---

## 🐛 Bugs Debugged — The Real Build Story

This is where the actual engineering happened.

**Bug 1 — Empty Airtable records appearing on every call**

Root cause: An agent-level webhook in Retell AI was firing on every
`call_started` event — even before anyone spoke.
Fix: Removed the agent-level webhook entirely. Kept the webhook
only inside the BookAppointment function. Empty records stopped immediately.

**Bug 2 — Joyce collecting details but not booking**

Root cause: Joyce was completing the conversation but ending the call
without firing the BookAppointment function.
Fix: Updated the function description to say "ALWAYS call this function
immediately" and added Step 6 — the exact phrase 
"Perfect! Let me get that booked for you right now" — as a 
trigger signal before the function fires.

**Bug 3 — Twilio SIP not connecting to Retell AI**

Root cause: Wrong Origination URI format.
Fix: The correct URI requires the `sip:` prefix.
`sip.retellai.com` fails silently. `sip:sip.retellai.com` works.

**Lesson:** Production AI voice systems fail in very specific,
non-obvious ways. Debugging them requires understanding the full
call routing pipeline — not just the AI layer.

---

## 📁 BookAppointment Function — Parameters

```json
{
  "name": "BookAppointment",
  "description": "ALWAYS call this function immediately after caller 
  confirms booking details. MUST be called before ending call.",
  "parameters": {
    "caller_name": "string — required",
    "service": "string — required", 
    "date": "string — required",
    "time": "string — required",
    "phone": "string — required"
  }
}
```

---

## 📋 Airtable Schema

| Field | Type | Source |
|-------|------|--------|
| Caller Name | Text | Joyce via BookAppointment |
| Service | Text | Joyce via BookAppointment |
| Appointment Date | Date | Joyce via BookAppointment |
| Appointment Time | Text | Joyce via BookAppointment |
| Phone Number | Phone | Joyce via BookAppointment |
| Status | Text | Hardcoded: "Booked" |
| Business Name | Text | Hardcoded: "Hair and Nail Salon" |

---

## 🚀 Replicate This for Your Business

1. Create accounts: Retell AI, ElevenLabs, Twilio, Make.com, Airtable
2. Buy a Twilio phone number ($1/month)
3. Build your agent in Retell AI — copy the 8-step system prompt above
4. Configure Twilio SIP trunk using the settings above
5. Create BookAppointment function with the 5 required parameters
6. Build Make.com scenario: Webhook → Airtable Create Record
7. Map the 5 parameters to your Airtable fields
8. Test with a real call — fix the 3 bugs above before they find you

**Timeline: 72 hours from zero to live**

---

**Follow the full build:** 
[LinkedIn](https://www.linkedin.com/in/gowravi-p-146567179) | 
[GitHub](https://github.com/Pillarisetti-Gowravi)

---

*Built by [Gowravi Pillarisetti](https://www.linkedin.com/in/gowravi-p-146567179)*
*AI Operations Analyst & Automation Builder *
