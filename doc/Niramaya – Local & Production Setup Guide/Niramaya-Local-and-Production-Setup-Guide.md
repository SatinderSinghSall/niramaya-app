# Niramaya --- Local Development, Production Mode & Environment Setup Guide

> **Purpose:** A practical reference for setting up, running, and
> preparing the Niramaya full-stack application in local development and
> production environments.
>
> **Project:** Full-Stack Niramaya App\
> **Backend:** Node.js, Express 5, MongoDB/Mongoose\
> **Mobile:** React Native, Expo SDK 58, Expo Router\
> **Package manager commands shown:** npm\
> **Shell examples:** Git Bash / VS Code terminal on Windows

---

## 1. Project structure

The repository is organised into separate backend, mobile, and
documentation areas:

```text
Full-Stack Niramaya App/
├── backend/
│   ├── doc/
│   ├── src/
│   ├── .env.development
│   ├── .env.example
│   ├── .env.production
│   ├── package.json
│   └── package-lock.json
├── doc/
└── mobile/
    ├── .expo/
    ├── .vscode/
    ├── android/
    ├── assets/
    ├── dist/
    ├── scripts/
    ├── src/
    ├── .env.example
    ├── .env.local
    ├── app.json
    ├── eas.json                 # verify whether this file exists
    ├── package.json
    └── package-lock.json
```

The screenshots show the `backend/.env.example` and
`mobile/.env.example` files. The actual contents of `.env.development`,
`.env.production`, and `.env.local` were not provided, so this guide
does not assume their values.

**Important:** `.env` files can contain database credentials, JWT
secrets, administrator credentials, and deployment URLs. Never commit
real secret values to Git or paste them into public issue trackers.

---

## 2. Prerequisites

Install and configure the following before starting the project:

- Node.js (use a version compatible with the installed Expo SDK and
  backend dependencies).
- npm, which is installed with Node.js.
- Git.
- Visual Studio Code or another editor.
- MongoDB access: a local MongoDB server or a MongoDB Atlas connection
  string.
- Expo Go for a compatible development workflow, or an Android
  emulator / physical Android device.
- Android Studio and Android SDK if you intend to run a native Android
  build locally.

Check the installed tools:

```bash
node --version
npm --version
git --version
```

Run commands from the correct project directory. Backend and mobile have
separate `package.json` files and separate dependency installations.

---

## 3. First-time project setup

Open the repository root in VS Code.

### 3.1 Install backend dependencies

```bash
cd backend
npm install
```

### 3.2 Install mobile dependencies

Open another terminal, or return to the repository root first:

```bash
cd mobile
npm install
```

Do not run backend commands from `mobile/`, or mobile commands from
`backend/`, unless the command explicitly says otherwise.

---

## 4. Environment configuration overview

Niramaya uses separate environment configuration for the backend and
mobile application.

---

Location File Purpose

---

`backend/` `.env.example` Template showing
backend variable names

`backend/` `.env.development` Backend
local-development
values

`backend/` `.env.production` Backend production-mode
values

`mobile/` `.env.example` Template showing mobile
public API URL

`mobile/` `.env.local` Local Expo environment
configuration

---

The example files are templates. Copy them or use them as a reference
when creating the real environment files. Do not overwrite a working
environment file without backing it up.

### 4.1 Backend environment variables

The supplied `backend/.env.example` screenshot shows these variables:

```dotenv
NODE_ENV=development
PORT=5000

MONGODB_URI=

JWT_ACCESS_SECRET=
JWT_REFRESH_SECRET=

JWT_ACCESS_EXPIRES_IN=
JWT_REFRESH_EXPIRES_IN=

CLIENT_URL=

JWT_ADMIN_ACCESS_SECRET=use-a-long-random-secret-here
JWT_ADMIN_REFRESH_SECRET=use-another-long-random-secret-here

JWT_ADMIN_ACCESS_EXPIRES_IN=15m
JWT_ADMIN_REFRESH_EXPIRES_IN=30d

ADMIN_FIRST_NAME=
ADMIN_LAST_NAME=
ADMIN_EMAIL=
ADMIN_PASSWORD=
ADMIN_ROLE=
```

#### Variable reference

---

Variable Purpose / configuration guidance

---

`NODE_ENV` Selects the intended runtime
environment, such as `development`
or `production`. The npm scripts
set this value using `cross-env`.

`PORT` Port on which the Express server
listens. The example uses `5000`.

`MONGODB_URI` MongoDB connection URI for the
relevant environment/database.

`JWT_ACCESS_SECRET` Private signing secret for normal
user access tokens. Use a strong,
unique secret.

`JWT_REFRESH_SECRET` Private signing secret for normal
user refresh tokens. Use a separate
strong secret.

`JWT_ACCESS_EXPIRES_IN` Access-token lifetime. Set a value
supported by the backend token
implementation.

`JWT_REFRESH_EXPIRES_IN` Refresh-token lifetime. Set a value
supported by the backend token
implementation.

`CLIENT_URL` Allowed client origin or URL used
by backend configuration, commonly
relevant to CORS. Confirm the exact
use in the backend source.

`JWT_ADMIN_ACCESS_SECRET` Separate private signing secret for
administrator access tokens.

`JWT_ADMIN_REFRESH_SECRET` Separate private signing secret for
administrator refresh tokens.

`JWT_ADMIN_ACCESS_EXPIRES_IN` Administrator access-token
lifetime. The example shows `15m`.

`JWT_ADMIN_REFRESH_EXPIRES_IN` Administrator refresh-token
lifetime. The example shows `30d`.

`ADMIN_FIRST_NAME` First name for the administrator
account created by the seed
process, if used by that script.

`ADMIN_LAST_NAME` Last name for the administrator
account.

`ADMIN_EMAIL` Email address for the administrator
account.

`ADMIN_PASSWORD` Initial administrator password. Use
a strong secret and do not commit
it.

`ADMIN_ROLE` Role value expected by the
application's administrator
model/seed script.

---

The screenshot includes example text for the admin JWT secrets. Replace
those example values with long, random, private values in real
environment files. Do not reuse the example secrets in production.

#### Development and production values

Use separate database credentials and secrets for development and
production. A typical arrangement is:

- `backend/.env.development`: local development database, development
  JWT secrets, local client URL.
- `backend/.env.production`: production database, production-only JWT
  secrets, deployed client URL, production administrator configuration
  if required.

These are configuration examples, not literal values to copy:

```dotenv
# backend/.env.development — illustrative placeholders
NODE_ENV=development
PORT=5000
MONGODB_URI=<development MongoDB connection URI>
JWT_ACCESS_SECRET=<development-only random secret>
JWT_REFRESH_SECRET=<different development-only random secret>
CLIENT_URL=<local or development client origin>
```

```dotenv
# backend/.env.production — illustrative placeholders
NODE_ENV=production
PORT=<port supplied by hosting platform, if applicable>
MONGODB_URI=<production MongoDB connection URI>
JWT_ACCESS_SECRET=<unique production random secret>
JWT_REFRESH_SECRET=<different unique production random secret>
CLIENT_URL=<deployed client origin>
```

Add the admin variables and token-expiry variables required by the
application to both files as appropriate. The placeholders above are not
valid credentials.

### 4.2 Mobile environment variable

The supplied `mobile/.env.example` screenshot shows:

```dotenv
EXPO_PUBLIC_API_URL=http://IPV4:PORT/api/v1
```

This is the API base URL used by the Expo application. Replace the
placeholder with the address of the backend that the device can reach.

Examples:

```dotenv
# Local backend accessed from a physical phone on the same Wi-Fi
EXPO_PUBLIC_API_URL=http://192.168.1.10:5000/api/v1
```

```dotenv
# Local backend accessed from an Android emulator
EXPO_PUBLIC_API_URL=http://10.0.2.2:5000/api/v1
```

Use the actual LAN IPv4 address of your development computer in the
physical-device example. The address `192.168.1.10` is only
illustrative.

#### Which address should I use?

---

Where the mobile app runs API host to consider

---

Physical Android device Your computer's LAN IPv4 address

Android Studio emulator Usually `10.0.2.2` for the host
computer

iOS simulator on macOS Often `localhost` for a backend on
the same Mac

Web browser on the same computer Usually `localhost`

Deployed mobile application Publicly reachable production API
hostname using HTTPS

---

A physical phone's `localhost` points to the phone itself, not your
development computer. The phone and computer should normally be on the
same network, and the computer firewall must allow connections to the
backend port.

**Expo public-variable warning:** Variables prefixed with `EXPO_PUBLIC_`
are intended to be included in the client bundle and must not contain
secrets. Never put MongoDB URIs, JWT signing secrets, administrator
passwords, or private credentials in the mobile environment file.

For a production mobile build, configure `EXPO_PUBLIC_API_URL` to the
deployed HTTPS API endpoint before creating the build. A locally built
or distributed app cannot reach your computer's private LAN address when
used outside your local network.

---

## 5. Important: make sure the backend loads the intended env file

The supplied backend scripts set `NODE_ENV`:

```json
"dev": "cross-env NODE_ENV=development nodemon src/server.js",
"start": "cross-env NODE_ENV=production node src/server.js"
```

Setting `NODE_ENV` does **not by itself guarantee** that dotenv loads
`.env.development` or `.env.production`.

Check the backend environment-loading code, likely in `src/server.js` or
a configuration module. Confirm that it explicitly selects the correct
file based on `NODE_ENV`, or that the deployment platform injects the
variables into the process environment.

For example, if the project uses the `dotenv` package directly, the
configuration may need logic conceptually similar to:

```js
import dotenv from "dotenv";

const envFile =
  process.env.NODE_ENV === "production"
    ? ".env.production"
    : ".env.development";

dotenv.config({ path: envFile });
```

This is an example of the required selection logic, **not a claim that
your current `server.js` already contains it**. Adapt it to the existing
project structure and ensure it runs before modules that read
`process.env`.

If the hosting platform supplies environment variables directly, you may
not need to upload an `.env.production` file. Follow the host's
secret/environment-variable configuration instead.

---

## 6. Run the backend locally (development)

### Step 1 --- configure development environment

Make sure `backend/.env.development` exists and contains valid
development values:

- `NODE_ENV=development`
- `PORT=5000` (or your chosen available port)
- `MONGODB_URI` pointing to your development database
- Development JWT secrets and expiry values
- `CLIENT_URL` appropriate for your local client
- Any other variables required by the backend

### Step 2 --- start MongoDB access

Make sure the configured MongoDB instance is running and reachable. If
using MongoDB Atlas, verify the connection string, database user
permissions, and network access rules.

### Step 3 --- start the backend

From the repository root:

```bash
cd backend
npm run dev
```

This executes:

```bash
cross-env NODE_ENV=development nodemon src/server.js
```

Expected behaviour:

- `NODE_ENV` is set to `development`.
- Node runs `src/server.js`.
- Nodemon watches for changes and restarts the server when watched
  files change.
- The server listens on the configured `PORT`, provided the
  application is configured correctly.

Keep this terminal open while developing.

### Step 4 --- check the server

Use the actual health-check route if the backend defines one. No
health-check endpoint was provided in the supplied material, so do not
assume a particular route exists.

If no health-check route exists, check the backend startup logs for
successful database connection and server-listening messages.

---

## 7. Run the backend in production mode

Your backend package defines:

```json
"start": "cross-env NODE_ENV=production node src/server.js"
```

### Step 1 --- configure production environment

Set the production database URI, production JWT secrets, production
client URL, and all other required variables. Use a production database
separate from development.

### Step 2 --- start in production mode

```bash
cd backend
npm start
```

This runs Node directly without Nodemon and sets:

```text
NODE_ENV=production
```

### Important distinction

`npm start` starts the backend process in production mode on the machine
where you run it. It does **not** automatically:

- Deploy the API to a hosting provider.
- Create a public HTTPS endpoint.
- Configure DNS, TLS certificates, firewall rules, or a reverse proxy.
- Provision MongoDB.
- Configure production environment variables on a hosting platform.
- Keep the process alive after the machine shuts down.

For a real production deployment, deploy the backend to a server or
hosting platform, configure its environment variables and network
access, and use the platform's process management and logging
facilities. The exact deployment steps depend on the hosting provider
and are not specified in the supplied project files.

---

## 8. Run the mobile app locally with Expo

### Step 1 --- configure the local API URL

Ensure `mobile/.env.local` contains the correct `EXPO_PUBLIC_API_URL`
for the device or emulator you are using.

Example for a physical phone:

```dotenv
EXPO_PUBLIC_API_URL=http://<YOUR_COMPUTER_LAN_IPV4>:5000/api/v1
```

Replace the placeholder with your computer's actual LAN IP address.

### Step 2 --- start the Expo development server

```bash
cd mobile
npx expo start -c
```

The `-c` option clears the Metro/Expo bundler cache before starting.
This is useful after changing environment values, dependencies, or
configuration.

You can then:

- Scan the QR code using Expo Go if the project and native
  dependencies are compatible.
- Press `a` to open an available Android emulator.
- Use the terminal's displayed options to select another supported
  target.

The mobile app and backend should run in separate terminals.

**Typical local workflow:**

Terminal 1:

```bash
cd backend
npm run dev
```

Terminal 2:

```bash
cd mobile
npx expo start -c
```

The mobile app calls the backend using `EXPO_PUBLIC_API_URL`.

### Troubleshooting local connectivity

If the app cannot connect to the API:

1.  Confirm the backend process is running.
2.  Confirm the backend is listening on the expected port.
3.  Confirm the mobile API URL uses the correct host and `/api/v1` path.
4.  For a physical phone, use the computer's LAN IPv4 address, not
    `localhost`.
5.  Confirm both devices are on a network that permits communication.
6.  Check Windows Firewall and any VPN settings.
7.  Confirm the backend CORS configuration permits the relevant client
    origin when applicable.
8.  Restart Expo with `npx expo start -c` after changing the environment
    value.

---

## 9. Production mobile app: build and release

`npx expo start -c` is for local development. It is not the command that
creates a store-ready production application.

The supplied `mobile/package.json` contains these scripts:

```json
"start": "expo start",
"android": "expo run:android",
"ios": "expo run:ios",
"web": "expo start --web",
"lint": "expo lint"
```

There is no production build script shown in the supplied package
configuration. The supplied `app.json` includes an EAS project ID, which
indicates EAS project configuration, but the `eas.json` build profiles
were not supplied.

### Before creating a production build

1.  Set `EXPO_PUBLIC_API_URL` to the deployed production API URL, using
    HTTPS.
2.  Confirm the production backend is deployed and reachable from the
    public internet.
3.  Confirm the production backend connects to the production database.
4.  Confirm the Android package identifier is correct:
    `com.satinder_singh_sall.niramaya`
5.  Review the app version and Android version code in `app.json`.
6.  Check that `eas.json` exists and contains the intended build
    profiles.
7.  Confirm EAS credentials and project access are configured.

If EAS CLI and a suitable `eas.json` profile are configured, a typical
Android production build command is:

```bash
cd mobile
npx eas-cli build --platform android --profile production
```

This command assumes that a `production` profile exists in `eas.json`.
If it does not, configure the profile first or use the profile actually
defined in that file. Do not assume this command is ready to run until
the build configuration is checked.

For a production iOS build, use the corresponding iOS platform and
ensure Apple signing and account requirements are configured.

---

## 10. Available backend npm scripts

The supplied backend `package.json` defines:

---

Command Purpose

---

`npm run dev` Start the backend in development
mode with Nodemon

`npm start` Start the backend in production
mode with Node

`npm test` Placeholder script; currently
prints that no tests are specified
and exits with an error

`npm run seed:ayurveda:dev` Run the Ayurveda seed script in
development mode

`npm run seed:yoga:dev` Run the Yoga seed script in
development mode

`npm run seed:ayurveda` Run the Ayurveda seed script in
production mode

`npm run seed:yoga` Run the Yoga seed script in
production mode

`npm run seed:admin:dev` Run the administrator seed script
in development mode

`npm run seed:admin` Run the administrator seed script
in production mode

---

Run seed scripts from the `backend/` directory.

Examples:

```bash
cd backend

# Development seed operations
npm run seed:ayurveda:dev
npm run seed:yoga:dev
npm run seed:admin:dev
```

Production seed scripts target the production environment. Use them only
when you intentionally want to seed the production database and have
verified the active environment and database URI:

```bash
npm run seed:ayurveda
npm run seed:yoga
npm run seed:admin
```

**Caution:** A seed script may insert or modify database records.
Inspect the relevant seed file and verify the selected database before
running it, especially in production.

---

## 11. Mobile npm scripts

The supplied mobile `package.json` defines:

---

Command Purpose

---

`npm start` Start Expo

`npx expo start -c` Start Expo and clear the bundler
cache

`npm run android` Run the native Android development
command (`expo run:android`)

`npm run ios` Run the native iOS development
command (`expo run:ios`)

`npm run web` Start Expo for web

`npm run lint` Run Expo lint

`npm run reset-project` Run the project's reset script

---

Examples:

```bash
cd mobile

# Start local Expo development
npx expo start -c

# Run on Android with a configured native development environment
npm run android

# Run on web
npm run web

# Run lint
npm run lint
```

`npm run android` may require the Android SDK, emulator, and native
project setup. It is not a production store build command.

---

## 12. Recommended daily development workflow

Use two terminals in VS Code.

### Terminal A --- backend

```bash
cd backend
npm run dev
```

### Terminal B --- mobile

```bash
cd mobile
npx expo start -c
```

Before testing:

- Verify the correct backend environment file is loaded.
- Verify MongoDB is reachable.
- Verify the mobile API URL points to the correct backend host.
- Keep the backend and Expo terminals running.
- Check logs in both terminals if a request fails.

When changing only backend source code, Nodemon should restart the
backend automatically. When changing Expo configuration or environment
values, restart Expo; use `-c` when a cache clear is appropriate.

---

## 13. Security and environment-file rules

- Keep `.env.development`, `.env.production`, and `.env.local` out of
  Git.
- Commit `.env.example` templates with placeholder values only.
- Never put server secrets in `mobile/.env.local` or any
  `EXPO_PUBLIC_` variable.
- Use different JWT secrets for development and production.
- Use a separate production MongoDB database and credentials.
- Use strong, unique production administrator credentials.
- Restrict production database network access.
- Use HTTPS for the production API.
- Do not print secrets in logs or error messages.
- Rotate any secret that has been exposed or committed accidentally.

Check the repository `.gitignore` files to confirm real environment
files are excluded. If a secret was committed previously, deleting the
file in a later commit does not remove it from Git history; rotate the
secret.

---

## 14. Common problems and quick checks

---

Symptom Checks

---

Backend cannot connect to MongoDB Check `MONGODB_URI`, database
availability, credentials,
IP/network allowlist, and logs.

Backend starts on an unexpected Check the loaded `PORT` value and
port hosting platform port requirements.

Backend uses the wrong environment Check `NODE_ENV` and the dotenv
file-selection logic in the backend
source.

Mobile app cannot reach backend Check `EXPO_PUBLIC_API_URL`, device
network, firewall, backend port,
and server binding address.

Physical phone cannot reach Use the computer's LAN IPv4 address
`localhost` instead.

Expo still uses an old API URL Restart Expo and try
`npx expo start -c`.

Production app calls a local IP Set the production API URL before
building and create a new app
build.

CORS error in web client Check the backend's CORS
configuration and `CLIENT_URL`
usage.

EAS production build profile not Inspect `mobile/eas.json`; the
found supplied information does not
include its profiles.

---

---

## 15. Configuration items to verify in the source code

The following details cannot be confirmed from the supplied screenshots
and package configuration alone. Check them in the repository before
relying on the commands in a deployment:

- **Backend env loading:** Verify exactly how `src/server.js` or its
  imported configuration loads `.env.development` and
  `.env.production`.
- **Server binding:** Verify the Express server listens on the correct
  host/interface and uses `process.env.PORT`.
- **API prefix:** Confirm that the backend actually mounts its routes
  under `/api/v1`, matching the mobile example URL.
- **CORS:** Verify how `CLIENT_URL` is used and which origins are
  allowed.
- **Mobile env loading:** Verify Expo loads the intended `.env.local`
  values and that the API client reads `EXPO_PUBLIC_API_URL`.
- **EAS build configuration:** Inspect `mobile/eas.json` for the
  actual build profiles and environment configuration.
- **Git ignore rules:** Confirm real environment files are excluded
  from version control.
- **Production hosting:** Document the actual backend hosting
  provider, domain, process manager, TLS, and deployment procedure
  once selected.

Do not assume a route, health-check endpoint, hosting provider, EAS
profile, or environment-loading behaviour that has not been verified in
the source.

---

## 16. Quick command reference

### Start both services locally

Backend terminal:

```bash
cd backend
npm run dev
```

Mobile terminal:

```bash
cd mobile
npx expo start -c
```

### Start backend in production mode on the current machine

```bash
cd backend
npm start
```

### Run mobile lint

```bash
cd mobile
npm run lint
```

### Run Android native development

```bash
cd mobile
npm run android
```

### Create an EAS Android production build (only after checking `eas.json`)

```bash
cd mobile
npx eas-cli build --platform android --profile production
```

---

## 17. Final checklist

### Local development

- [ ] Backend dependencies installed.
- [ ] Mobile dependencies installed.
- [ ] `backend/.env.development` configured.
- [ ] Development MongoDB connection verified.
- [ ] Backend env-file loading verified.
- [ ] `mobile/.env.local` points to the reachable local API.
- [ ] Backend started with `npm run dev`.
- [ ] Expo started with `npx expo start -c`.
- [ ] App successfully communicates with the backend.

### Production preparation

- [ ] Production backend environment variables configured securely.
- [ ] Production MongoDB connection verified.
- [ ] Production JWT secrets are unique and private.
- [ ] Backend deployed to a production hosting environment.
- [ ] Public HTTPS API URL is available.
- [ ] CORS and allowed client origins verified.
- [ ] Production `EXPO_PUBLIC_API_URL` configured before app build.
- [ ] `eas.json` production profile verified.
- [ ] App identifiers, version, and Android version code checked.
- [ ] Production build tested against the production API.
- [ ] No real environment files or secrets are committed to Git.

---

## Appendix: package configuration supplied for this guide

### Backend scripts and dependencies

The supplied backend package configuration identifies:

- Package name: `backend`
- Version: `1.0.0`
- Entry point: `src/server.js` via the npm scripts
- Runtime: Node.js ES modules (`"type": "module"`)
- Development server: Nodemon
- Environment selection: `cross-env`
- Main dependencies: Express, Mongoose, dotenv, CORS, Helmet, Morgan,
  Zod, JSON Web Token, and bcryptjs

### Mobile configuration supplied for this guide

The supplied mobile package configuration identifies:

- Package name: `mobile`
- Entry point: `expo-router/entry`
- Expo SDK: `~58.0.25`
- Expo Router: `~58.0.31`
- React: `19.3.0`
- React Native: `0.88.1`
- TypeScript: `~6.0.3`
- Start script: `expo start`
- Android script: `expo run:android`
- iOS script: `expo run:ios`
- Web script: `expo start --web`
- Lint script: `expo lint`

The supplied `app.json` identifies:

- App name: `Niramaya`
- Slug: `niramaya`
- App version: `1.1.11`
- Android package: `com.satinder_singh_sall.niramaya`
- Android version code: `13`
- iOS build number: `13`
- EAS project ID: `e5f80bb1-37bf-442d-aef5-13eecd4f9eb9`

These values are recorded from the configuration supplied for this
documentation. Update this guide when the package scripts, app
identifiers, versions, environment variables, or deployment setup
change.
