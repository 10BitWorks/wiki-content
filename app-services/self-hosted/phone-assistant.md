---
title: Phone Assistant
created: 2026-06-15
updated: 2026-06-15
type: service
tags: service, link-hosted, voice, members
description: "AI phone receptionist for 10BitWorks, powered by Pipecat and Gemini Live."
isPublished: true
---

The Phone Assistant is a locally hosted [Pipecat](https://pipecat.ai/) instance that routes audio between Twilio and the Gemini Live API. It answers calls to the 10BitWorks phone number and acts as a receptionist for prospective and current members.

## Configuration

- **Host:** [Docker (Portainer) Host on Link](/app-services/self-hosted/docker-portainer-host-on-link) (`10.7.1.25`)
- **Container port:** 8000
- **Published port:** `17293`
- **Model:** `gemini-3.1-flash-live-preview`
- **Environment variables** (set in Portainer):
  - `GOOGLE_API_KEY`
  - `TWILIO_ACCOUNT_SID`
  - `TWILIO_AUTH_TOKEN`
- **Reverse proxy:** Nginx Proxy Manager forwards `https://phone.10bitworks.org/` to `10.7.1.25:17293` with WebSockets support enabled
- **TwiML App Voice Request URL:** `https://phone.10bitworks.org/twiml` (HTTP GET)

## How it works

1. Twilio sends a GET request to `/twiml` when a call arrives.
2. The assistant responds with TwiML instructions to connect the call to a WebSocket stream at `/ws`.
3. `FastAPIWebsocketTransport` handles bidirectional audio with Twilio.
4. `GeminiLiveLLMService` provides real-time speech-to-speech interaction.

## Assistant behavior

- Speaks as the voice of 10BitWorks itself.
- Uses a deep, informative, unexcitable tone.
- Answers only from known knowledge; does not guess.
- Can query internal support tools for Slack-informed answers.
- Can transfer calls to known support volunteers via CiviCRM integration.
- Responds in the caller's language if not English.
- Closes calls with the tagline: "Come and Make It!"

## Knowledge gaps

If the assistant cannot answer a relevant 10BitWorks question, it logs the gap with a `report_missing_knowledge` tool for developer review.

## Related

- [Docker (Portainer) Host on Link](/app-services/self-hosted/docker-portainer-host-on-link)
- [WordPress + CiviCRM](/app-services/self-hosted/wordpress-civicrm)
- [Hosted Services Maintenance Policy](/policies/hosted-services-maintenance)
