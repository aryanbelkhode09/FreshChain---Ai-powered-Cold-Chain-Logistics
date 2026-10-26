# FreshChain: AI-powered cold-chain logistics (React + Vite)

The whole site in React: home page, six service pages with 3D trackers, the fleet manager,
the interactive journey, key figures, the gallery and the Request Pilot booking page.

## Run it

    npm install
    npm run dev       # http://localhost:5173
    npm run build     # output in dist/ (works from any folder)

Needs Node 18 or newer. All data is simulated (no backend, nothing is sent anywhere).

## Where things live

 # FreshChain — AI-Powered Cold Chain Logistics

A web-based cold-chain logistics project designed to support shipment visibility and the management of temperature-sensitive goods.

## Overview

FreshChain brings together logistics workflows, shipment tracking, and AI-powered conversational assistance in one application.

## Key Features

- Shipment tracking and logistics workflow management
- Role-based interfaces for supported supply-chain users
- AI-powered chatbot using the Groq API
- Shipment and temperature-risk information, where implemented
- React-based user interface

## Technology Stack

| Component | Technology |
| Backend | Python, FastAPI |
| Frontend | React, Vite, JavaScript |
| AI Chatbot | Groq API |
| Database | Add the database actually used |

## Getting Started

1. Clone this repository.
2. Install the backend dependencies using the provided requirements file.
3. Configure the required environment variables in a local `.env` file.
4. Start the FastAPI backend.
5. Install frontend dependencies and start the Vite development server.

Refer to the backend and frontend folders for the exact setup commands.

## Project Screenshots

<img width="1900" height="963" alt="image" src="https://github.com/user-attachments/assets/da26e763-aee0-4a8c-95c9-b9b8f6ded139" />


## Future Improvements

- Enhanced shipment monitoring
- Improved logistics analytics
- Additional automated risk-detection capabilities


## Notes

- three.js is pinned to 0.128.0 so colours match the original design.
- Simulation, not AI: there is no trained model. Alerts come from threshold and trend rules.
- Gallery tiles are illustrations; swap them for photos in `src/lib/gallerySvg.js` / `Gallery`.

## Alerts to a vehicle's mobile number

A vehicle can have an optional alert mobile number. When it gets a transport warning, a temperature
breach or a spoilage-risk alert, the page shows a toast ("Alert for +91 ...") and writes a log line.
It is shown on screen only. **Nothing is sent**: no SMS, WhatsApp or e-mail, and the page contains no
wa.me or sms: links. Real delivery would need a backend (see the chat section for the same pattern).

## AI chat ("Ask FreshChain AI")

The floating button opens a chat panel. It answers from the current simulated fleet. The browser
never holds an API key. `askAI(messages, systemPrompt)` in `src/lib/chat.js` POSTs JSON to your own
endpoint, set at build time:

    # .env  (see .env.example)
    VITE_CHAT_URL=https://your-server.example/api/chat

    POST  { "system": "<system prompt>", "messages": [{ "role": "user" | "assistant", "content": "..." }] }
    200   { "text": "<reply>" }

Your endpoint calls the model of your choice and keeps the key on the server. Allow CORS for the
site's origin if it is on a different domain. If `VITE_CHAT_URL` is not set, the chat panel opens
and tells the visitor that a chat backend needs to be configured.
