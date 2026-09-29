<<<<<<< HEAD
# IGNITE Freshers Event

A responsive single-page React/Vite event site for the upcoming IGNITE freshers celebration hosted by the Master of Computer Applications Department at Centurion University of Technology and Management. The poster releases on 5 October 2026 and the main event is on 9 October 2026.

## Registration architecture

Registration now follows this serverless flow:

```text
React IGNITE site → Vercel Function /api/register → Supabase registrations table
                                           └──────→ QR generation → Resend student email
```

The Vercel function creates a unique `IGNITE-2026-XXXXXXXXXX` registration code, saves the student record in Supabase, generates a QR code containing the non-sensitive registration code, and emails the QR image to the student through Resend. After a successful submission, the registration modal also displays the QR code and provides an immediate download button. Supabase and Resend secrets are server-only and are never exposed to the browser.

## Services and setup

1. Create a Supabase project.
2. Run [`supabase/schema.sql`](supabase/schema.sql) in the Supabase SQL Editor.
3. Create a Resend account and verify the sending domain used by `RESEND_FROM_EMAIL`.
4. Copy `.env.example` to `.env.local` for local Vercel testing, or add the same variables in the Vercel project settings:

   ```text
   SUPABASE_URL
   SUPABASE_SERVICE_ROLE_KEY
   RESEND_API_KEY
   RESEND_FROM_EMAIL
   ```

5. Deploy the project to Vercel. The API endpoint will be available at `/api/register`.

Never commit `.env.local`, the Supabase service-role key, or the Resend API key. The service-role key bypasses Supabase Row Level Security and must only be used inside the serverless function.

The current managed Preview can build and display the frontend, but automatic QR email delivery requires deployment of the `/api/register` function with the four secrets configured.

## Other frontend forms

Contact and Feedback still use the shared Formspree endpoint `https://formspree.io/f/myezojna`. Activity Participation is configured as `https://formspree.io/f/mgavdyjg`. The old Registration Formspree endpoint `https://formspree.io/f/mdekbzvl` remains documented in `src/config.js` for reference, but the Registration modal now posts to `/api/register` so that QR generation and email delivery happen securely.

## Install and run

```bash
npm install
npm run dev
```

The development server listens on `http://localhost:3000`. To create a production build:

```bash
npm run build
npm run preview
```

For local API testing, use the Vercel CLI after setting `.env.local`:

```bash
npx vercel dev
```

## File tree

```text
.
├── .env.example
├── api
│   └── register.js                 # Vercel serverless registration + QR + email
├── app.config.ts
├── ideas.md
├── index.html
├── package.json
├── package-lock.json
├── pnpm-workspace.yaml
├── supabase
│   └── schema.sql                  # registrations table and constraints
├── vercel.json
├── vite.config.js
├── public
│   ├── ignite-invitation.png
│   ├── manus-routes.json
│   ├── ignite-mark.svg
│   ├── ignite-logo.png              # optional alternate logo asset
│   ├── ignite.mp4                   # optional official video
│   └── videos
│       ├── poster1.mp4
│       └── poster2.mp4
└── src
    ├── App.jsx
    ├── config.js
    ├── index.css
    ├── main.jsx
    └── components
        ├── AboutSection.jsx
        ├── ActivityRegistrationModal.jsx
        ├── ContactSection.jsx
        ├── CountdownTimer.jsx
        ├── EventSection.jsx
        ├── Footer.jsx
        ├── FeedbackSection.jsx
        ├── HeroSection.jsx
        ├── InvitationSection.jsx
        ├── LoadingScreen.jsx
        ├── MemoriesSection.jsx
        ├── Navigation.jsx
        ├── ParticleBackground.jsx
        ├── RegistrationModal.jsx
        ├── SectionShell.jsx
        ├── Video.jsx
        └── index.js
```

## Editing event content

Event timing, venue, poster-release date, Formspree endpoints, source media paths, and download names live in `src/config.js`. The serverless registration endpoint has its own validated request contract in `api/register.js` and persists records using `supabase/schema.sql`.

## Technology

- React 19 + Vite
- Vercel Functions
- Supabase PostgreSQL
- Resend transactional email
- `qrcode` server-side QR generation
- framer-motion
- three.js
- CSS custom properties and inline style objects
- Frontend and serverless browser-data flow
=======
# IGNITE-FRESHERS
>>>>>>> 9b8ecf4c299dc6449d5146ce44acc0cbf4030115
