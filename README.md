# DARBS AI

DARBS (Diagnostic Assistant for Repair, Bugs and Support) is a React/Vite
troubleshooting assistant backed by an Express server and the xAI Grok API.

## Requirements

- Node.js 20 or newer
- An xAI API key with access to the configured Grok models

## Configure

Create a `.env.local` file in the project root and set:

```env
XAI_API_KEY=your_key_here
GROK_MODEL=grok-2-latest
GROK_VISION_MODEL=grok-2-vision-1212
PORT=3000
```

Keep the key server-side: never place it in frontend code or commit `.env.local`.

## Run locally

```sh
npm install
npm run dev
```

The Express server serves the Vite app and API on port `3000` by default. Set
`PORT` in the environment to use a different port.

## Build and deploy

Deploy as a Node.js web service, not as a static-only site:

1. Install dependencies with `npm install`.
2. Build with `npm run build`.
3. Start with `npm start`.
4. Configure `XAI_API_KEY` in the hosting provider's environment settings.
   The host should supply `PORT`; the server binds to `0.0.0.0`.
5. Configure the provider's health check to use `/api/health`.

The build creates the static frontend and bundled Express server in `dist/`.
The production server serves both the frontend and `/api/*` routes from the
same origin.

## Important authentication limitation

The sign-in and registration UI currently stores account data in the browser;
it is a demo-only gate, not real authentication. Anyone can register or alter
browser storage, and the API routes do not require a signed-in user. Do not use
this setup to protect private data or expose an unrestricted production Gemini
key. Add server-side authentication and API abuse protections before a public
production launch.
