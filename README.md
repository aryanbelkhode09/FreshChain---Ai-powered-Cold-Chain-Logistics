# FreshChain: AI-powered cold-chain logistics (React + Vite)

The whole site in React: home page, six service pages with 3D trackers, the fleet manager,
the interactive journey, key figures, the gallery and the Request Pilot booking page.

## Run it

    npm install
    npm run dev       # http://localhost:5173
    npm run build     # output in dist/ (works from any folder)

Needs Node 18 or newer. All data is simulated (no backend, nothing is sent anywhere).

## Where things live

    src/
      App.jsx                 page router (hash links: #road-freight, #rail, #air-cargo,
                              #ocean-freight, #warehousing, #customs, #pilot) + scroll restore
      index.css               all styles (light and dark mode via prefers-color-scheme)
      components/
        Header, Hero            3D journey scene with station tabs (temperature badges on the 3D models)
        Sections.jsx            Problem, Journey (interactive), Solution, Tracks, FleetTruck,
                                Services (shows each service's fleet), Gallery, KeyFigures, Impact, Contact, Footer
        Demo.jsx                mission control: fleet, map, failure test, offline queue, liability docket;
                                click the status tag of the selected vehicle to deselect it
        FleetForm.jsx           add-vehicle form; the number asked for changes with the vehicle type;
                                optional alert mobile number (default "+91 ", 8 to 15 digits)
        ServicePage.jsx         video hero, search by number or by product + quantity, fleet panel, 3D tracker
        Tracker.jsx             side panel: zone temperatures, warehouse pallet status, customs timeline
        PilotPage.jsx           booking form with inline validation
        AlertCenter.jsx         on-screen toast "Alert for <phone>" (auto-hides after 30 s)
        Chat.jsx                floating "Ask FreshChain AI" button and chat panel
        Count.jsx               count-up numbers
      lib/
        fleet.js                vehicle types, sample fleet, per-type number rules and validation, simulated ETA
        fleetStore.js           shared fleet + simulation (temperatures, anomaly prediction, rerouting,
                                ETA delay of 40 min on failure, on-screen phone alerts)
        alertStore.js           state of the on-screen phone alert toast
        chat.js                 askAI(messages, systemPrompt): POSTs to VITE_CHAT_URL
        products.js             product catalogue: every product has its own colours, icon, safe temperature and 3D shape
        services.js             service copy, tracker settings, journey text
        gallerySvg.js           the four illustrated gallery scenes
      three/
        hero.js                 isometric 3D world on the home page (plain three.js)
        models.js               truck, train, aircraft, ship, warehouse and the product shapes inside the crates
        engine.js               tracker renderer (X-ray view, temperature badges, pallet marker)
      hooks/                    useFleet (store), useTrackerSim (zone simulation), useScrolled
    public/videos/              one looping video per service (replace the files, keep the names)

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
