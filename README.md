# 🌿 Niramaya — Full-Stack Wellness & Wellbeing App

[![React Native](https://img.shields.io/badge/React%20Native-0.86.3-61DAFB?logo=react&logoColor=white)](https://reactnative.dev/)
[![Expo](https://img.shields.io/badge/Expo-57-000020?logo=expo&logoColor=white)](https://expo.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-6.0.3-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![NativeWind](https://img.shields.io/badge/NativeWind-4.2.7-38BDF8?logo=tailwindcss&logoColor=white)](https://www.nativewind.dev/)
[![Node.js](https://img.shields.io/badge/Node.js-Backend-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![Express](https://img.shields.io/badge/Express-5.2.1-000000?logo=express&logoColor=white)](https://expressjs.com/)
[![MongoDB](https://img.shields.io/badge/MongoDB-Database-47A248?logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![Mongoose](https://img.shields.io/badge/Mongoose-ODM-880000)](https://mongoosejs.com/)
[![JWT](https://img.shields.io/badge/JWT-Authentication-000000?logo=jsonwebtokens&logoColor=white)](https://jwt.io/)
[![Axios](https://img.shields.io/badge/Axios-HTTP%20Client-5A29E4?logo=axios&logoColor=white)](https://axios-http.com/)
[![MCA Project](https://img.shields.io/badge/MCA-Final%20Year%20Project-4D6A50)](#)
[![Status](https://img.shields.io/badge/Status-Active%20Development-4D6A50)](#)

> **Wellness • Balance • You**

Niramaya is a full-stack mobile wellness application designed to bring personalized wellness guidance, health self-awareness, goals, progress tracking, Ayurveda, Yoga, consultation workflows, notifications, and account management into one mobile experience.

Built as an **MCA Final Year Project**, Niramaya demonstrates a complete mobile-to-API-to-database architecture using **React Native + Expo**, **Node.js + Express**, and **MongoDB + Mongoose**.

---

## 📚 Table of Contents

- [About Niramaya](#-about-niramaya)
- [Why Niramaya](#-why-niramaya)
- [Core Features](#-core-features)
- [Complete Application Flow](#-complete-application-flow)
- [Monorepo Architecture](#-monorepo-architecture)
- [Technology Stack](#-technology-stack)
- [Repository Structure](#-repository-structure)
- [Backend Architecture](#-backend-architecture)
- [Backend API Catalog](#-backend-api-catalog)
- [Authentication API](#-authentication-api)
- [Profile and Settings API](#-profile-and-settings-api)
- [Mobile / Frontend Architecture](#-mobile--frontend-architecture)
- [Frontend Screens](#-frontend-screens)
- [Frontend Services](#-frontend-services)
- [Onboarding](#-onboarding)
- [Personalization](#-personalization)
- [Environment Variables](#-environment-variables)
- [Installation](#-installation)
- [Database Setup and Seeding](#-database-setup-and-seeding)
- [Running the Monorepo](#-running-the-monorepo)
- [API Configuration](#-api-configuration)
- [Authentication and Security](#-authentication-and-security)
- [Design System](#-design-system)
- [Development Guidelines](#-development-guidelines)
- [Troubleshooting](#-troubleshooting)
- [Project Status](#-project-status)
- [Future Enhancements](#-future-enhancements)
- [Authors](#-authors)
- [License](#-license)

---

# 🌿 About Niramaya

**Niramaya** is a personalized wellness and wellbeing mobile application.

The application starts with authentication and a structured multi-step onboarding process. Users can provide information about their personal details, physical health, wellbeing, lifestyle, nutrition, sleep, fitness, yoga experience, and wellness preferences.

That information becomes the foundation for the authenticated application experience:

```text
                    NIRAMAYA
                       │
                       ▼
                Landing / Auth
                       │
                       ▼
                  Onboarding
                       │
                       ▼
                Health Profile
                       │
                       ▼
               Home Dashboard
                       │
       ┌───────────────┼────────────────┐
       ▼               ▼                ▼
     Goals          Progress          Explore
                                         │
                              ┌──────────┼──────────┐
                              ▼          ▼          ▼
                           Ayurveda     Yoga      Search
                              │          │          │
                              └──────────┼──────────┘
                                         ▼
                                    Favorites

       Additional modules:
       Consultation • Notifications • Profile • Settings
```

> **Wellness notice:** Niramaya is a wellness-oriented application. Its information and recommendations are not intended to diagnose, treat, cure, or prevent disease and should not replace qualified professional medical advice.

---

# 💚 Why Niramaya

Niramaya is designed around a simple idea:

> **Understand yourself → Set meaningful goals → Build healthier habits → Track progress → Discover suitable wellness practices.**

Instead of treating wellness features as isolated screens, the application connects:

- User profile
- Health information
- Wellness preferences
- Goals
- Progress history
- Ayurveda
- Yoga
- Recommendations
- Consultation
- Notifications

This creates a foundation for a personalized wellness experience.

---

# ✨ Core Features

## 🔐 Authentication

- Signup
- Login
- Current-user retrieval
- JWT access token
- JWT refresh token
- Protected API routes
- Secure mobile token storage
- Logout
- Password change
- Account deactivation
- Authentication state management with `AuthContext`

---

## 🧾 Multi-Step Onboarding

Niramaya uses eight onboarding stages:

| Step | Screen          | Purpose                                  |
| ---- | --------------- | ---------------------------------------- |
| 1    | About You       | Personal information                     |
| 2    | Physical Health | Physical wellness information            |
| 3    | Wellbeing       | Stress, mood and mental-wellbeing inputs |
| 4    | Lifestyle       | Activity and daily habits                |
| 5    | Nutrition       | Diet and food information                |
| 6    | Sleep           | Sleep patterns and quality               |
| 7    | Fitness & Yoga  | Exercise, yoga and activity information  |
| 8    | Preferences     | Wellness interests and preferences       |

The onboarding architecture supports validation, progress indication, dropdown/selection controls, keyboard handling, and structured data collection.

---

## 🏠 Personalized Dashboard

The Home screen is the main authenticated entry point.

It provides access to:

- Wellness overview
- User greeting/profile information
- Recommended practices
- Goals
- Progress
- Health Profile
- Consultation
- Explore
- Application drawer
- Notifications and account areas

---

## 🎯 Goals

Users can:

- View their goals
- Create goals
- Open goal details
- Track goal progress
- Connect wellness goals with their broader wellbeing journey

---

## 📈 Progress Tracking

Progress records can include:

- Mood
- Energy
- Stress
- Sleep duration
- Sleep quality
- Water intake
- Daily steps
- Exercise minutes
- Yoga minutes
- Meditation minutes
- Weight
- Completed activities
- Notes

Progress functionality includes:

- Progress history
- Add progress
- Edit progress
- Progress summary
- Progress details
- Daily progress handling

---

## 🌿 Ayurveda

The Ayurveda module provides wellness-oriented Ayurvedic content.

Includes:

- Ayurveda listing
- Ayurveda detail pages
- Categories/content discovery
- Personalized recommendation support
- Favorites
- Explore integration
- Search integration
- Seed data for initial content

---

## 🧘 Yoga

The Yoga module provides yoga practice information and recommendations.

Includes:

- Yoga listing
- Yoga detail pages
- Practice categories
- Personalized recommendations
- Favorites
- Explore integration
- Search integration
- Seed data for initial content

---

## 🔎 Explore

Explore acts as a central wellness discovery experience.

It brings together:

- Recommendations
- Yoga
- Ayurveda
- Search
- Favorites
- Content cards
- Category filters

---

## 🔍 Search

Search supports wellness content discovery across the supported content types.

The frontend search flow supports filtering between:

```text
All
Yoga
Ayurveda
```

and uses the backend search service through the mobile API layer.

---

## ❤️ Favorites

Users can save supported wellness content.

Favorites have their own:

- Backend model
- Controller
- Service
- Routes
- Validation
- Mobile service
- Mobile screen

---

## 🩺 Health Profile

The Health Profile module allows users to:

- View health information
- Edit health information
- Update stored wellness information
- Keep health data separate from general account/profile data

---

## 👨‍⚕️ Ayurvedic Consultation

The consultation workflow includes:

- Consultation overview
- Consultation booking/request
- Consultation history
- Consultation details

The backend contains dedicated consultation models, controllers, services, routes and validation.

---

## 🔔 Notifications

The notification module supports:

- Notification listing
- Reading notifications
- Marking notifications as read
- Marking all notifications as read
- Unread count
- Notification preference integration

---

## 👤 Profile

The profile area supports:

- Viewing account information
- Editing profile information
- Password management
- Account-related actions

---

## ⚙️ Settings

Settings include configurable areas for:

- Notifications
- Goal reminders
- Progress reminders
- Consultation updates
- Wellness reminders
- Reminder preferences
- Appearance/theme
- Privacy preferences
- Language/timezone preferences

---

## ☰ Custom Application Drawer

The authenticated application includes a custom overlay drawer.

The drawer provides navigation to:

```text
Home
Goals
Progress
Explore
Ayurveda
Yoga
Favorites
Health Profile
Consultation
Notifications
Settings
Profile
Logout
```

The drawer is implemented using reusable components:

```text
DrawerContext.tsx
AppDrawer.tsx
DrawerItem.tsx
```

---

# 🔄 Complete Application Flow

```text
┌──────────────────────┐
│      Landing         │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│    Login / Signup    │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│ JWT Authentication   │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│     Onboarding       │
│                      │
│ About You            │
│ Physical Health      │
│ Wellbeing            │
│ Lifestyle            │
│ Nutrition            │
│ Sleep                │
│ Fitness & Yoga       │
│ Preferences          │
└──────────┬───────────┘
           │
           ▼
┌─────────────────────────────┐
│       Home Dashboard        │
└─────────────┬───────────────┘
              │
     ┌────────┼─────────┬──────────────┐
     ▼        ▼         ▼              ▼
   Goals   Progress   Explore       Health Profile
                       │
                ┌──────┼──────┐
                ▼      ▼      ▼
             Yoga  Ayurveda Search
                │      │
                └──┬───┘
                   ▼
               Favorites

Additional:
Consultation • Notifications • Profile • Settings
```

---

# 🏗️ Monorepo Architecture

Niramaya is organized as a two-application monorepo:

```text
Full-Stack Niramaya App/
│
├── backend/     → REST API + MongoDB
│
└── mobile/      → React Native + Expo
```

The communication flow is:

```text
React Native / Expo
        │
        │ Axios
        │ JSON / HTTP
        ▼
Node.js + Express
        │
        ├── Authentication
        ├── Validation
        ├── Controllers
        └── Services
                │
                ▼
            Mongoose
                │
                ▼
             MongoDB
```

---

# 🧰 Technology Stack

## Frontend / Mobile

| Technology                     |    Version | Purpose                             |
| ------------------------------ | ---------: | ----------------------------------- |
| React Native                   |   `0.86.3` | Mobile application UI               |
| Expo                           | `~57.0.25` | React Native platform               |
| Expo Router                    | `~57.0.23` | File-based routing                  |
| React                          |   `19.2.3` | UI framework                        |
| TypeScript                     |   `~6.0.3` | Static typing                       |
| NativeWind                     |   `^4.2.7` | Tailwind-style React Native styling |
| Tailwind CSS                   |  `^3.4.17` | Styling configuration               |
| Axios                          |  `^1.20.0` | API communication                   |
| Expo Secure Store              |  `~57.0.4` | Secure token storage                |
| Expo Constants                 | `~57.0.20` | Expo configuration                  |
| Expo Device                    |  `~57.0.2` | Device information                  |
| Expo Image                     |  `~57.0.5` | Image handling                      |
| React Native Safe Area Context |   `~5.7.0` | Safe-area support                   |
| React Native Screens           |  `~4.26.0` | Native navigation support           |
| React Native Reanimated        |    `4.5.1` | Animation support                   |
| React Native Picker            |   `2.11.4` | Picker controls                     |
| DateTimePicker                 |    `9.1.0` | Date/time controls                  |

## Backend

| Technology     |  Version | Purpose                    |
| -------------- | -------: | -------------------------- |
| Node.js        |  Runtime | Backend runtime            |
| Express        |  `5.2.1` | REST API framework         |
| MongoDB        | Database | Persistent storage         |
| Mongoose       | `9.10.2` | MongoDB ODM                |
| JSON Web Token |  `9.0.3` | Authentication             |
| bcryptjs       |  `3.0.3` | Password hashing           |
| Zod            |  `4.6.5` | Request validation         |
| Helmet         |  `8.3.0` | Security headers           |
| CORS           |  `2.8.6` | Cross-origin configuration |
| Morgan         | `1.12.1` | HTTP request logging       |
| dotenv         | `18.0.4` | Environment variables      |
| Nodemon        | `3.1.14` | Development reload         |

---

# 📁 Repository Structure

```text
Full-Stack Niramaya App/
│
├── backend/
│   ├── src/
│   │   ├── config/
│   │   │   ├── db.js
│   │   │   └── env.js
│   │   │
│   │   ├── controllers/
│   │   │   ├── auth.controller.js
│   │   │   ├── ayurveda.controller.js
│   │   │   ├── consultation.controller.js
│   │   │   ├── dashboard.controller.js
│   │   │   ├── favorite.controller.js
│   │   │   ├── goal.controller.js
│   │   │   ├── healthProfile.controller.js
│   │   │   ├── notification.controller.js
│   │   │   ├── profile.controller.js
│   │   │   ├── progress.controller.js
│   │   │   ├── recommendation.controller.js
│   │   │   ├── search.controller.js
│   │   │   ├── user.controller.js
│   │   │   └── yoga.controller.js
│   │   │
│   │   ├── middlewares/
│   │   │   ├── auth.middleware.js
│   │   │   ├── error.middleware.js
│   │   │   ├── notFound.middleware.js
│   │   │   └── validate.middleware.js
│   │   │
│   │   ├── models/
│   │   │   ├── ayurveda.model.js
│   │   │   ├── consultation.model.js
│   │   │   ├── favorite.model.js
│   │   │   ├── goal.model.js
│   │   │   ├── healthProfile.model.js
│   │   │   ├── notification.model.js
│   │   │   ├── progress.model.js
│   │   │   ├── settings.model.js
│   │   │   ├── user.model.js
│   │   │   └── yoga.model.js
│   │   │
│   │   ├── routes/
│   │   │   ├── auth.routes.js
│   │   │   ├── ayurveda.routes.js
│   │   │   ├── consultation.routes.js
│   │   │   ├── dashboard.routes.js
│   │   │   ├── favorite.routes.js
│   │   │   ├── goal.routes.js
│   │   │   ├── healthProfile.routes.js
│   │   │   ├── index.js
│   │   │   ├── notification.routes.js
│   │   │   ├── profile.routes.js
│   │   │   ├── progress.routes.js
│   │   │   ├── recommendation.routes.js
│   │   │   ├── search.routes.js
│   │   │   └── yoga.routes.js
│   │   │
│   │   ├── services/
│   │   │   ├── auth.service.js
│   │   │   ├── ayurveda.service.js
│   │   │   ├── consultation.service.js
│   │   │   ├── dashboard.service.js
│   │   │   ├── favorite.service.js
│   │   │   ├── goal.service.js
│   │   │   ├── healthProfile.service.js
│   │   │   ├── notification.service.js
│   │   │   ├── profile.service.js
│   │   │   ├── progress.service.js
│   │   │   ├── recommendation.service.js
│   │   │   ├── search.service.js
│   │   │   └── yoga.service.js
│   │   │
│   │   ├── utils/
│   │   │   ├── auth.util.js
│   │   │   ├── ayurveda.seed.js
│   │   │   ├── ayurveda.validation.js
│   │   │   ├── consultation.validation.js
│   │   │   ├── favorite.validation.js
│   │   │   ├── goal.validation.js
│   │   │   ├── healthProfile.validation.js
│   │   │   ├── notification.validation.js
│   │   │   ├── profile.validation.js
│   │   │   ├── progress.validation.js
│   │   │   ├── recommendation.validation.js
│   │   │   ├── search.validation.js
│   │   │   ├── user.util.js
│   │   │   ├── validation.util.js
│   │   │   ├── yoga.seed.js
│   │   │   └── yoga.validation.js
│   │   │
│   │   ├── app.js
│   │   └── server.js
│   │
│   ├── .gitignore
│   ├── README.md
│   ├── package.json
│   └── package-lock.json
│
├── mobile/
│   ├── assets/
│   ├── scripts/
│   ├── src/
│   │   ├── app/
│   │   │   ├── (main)/
│   │   │   ├── (onboarding)/
│   │   │   ├── (public)/
│   │   │   ├── _layout.tsx
│   │   │   └── index.tsx
│   │   ├── components/
│   │   ├── constants/
│   │   ├── context/
│   │   ├── hooks/
│   │   ├── services/
│   │   ├── types/
│   │   ├── utils/
│   │   └── global.css
│   ├── .gitignore
│   ├── AGENTS.md
│   ├── LICENSE
│   ├── app.json
│   ├── babel.config.js
│   ├── expo-env.d.ts
│   ├── metro.config.js
│   ├── nativewind-env.d.ts
│   ├── package.json
│   ├── package-lock.json
│   ├── tailwind.config.js
│   └── tsconfig.json
│
├── .gitignore
└── README.md
```

---

# ⚙️ Backend Architecture

The backend follows a layered architecture:

```text
HTTP Request
     │
     ▼
Route
     │
     ▼
Middleware
     │
     ├── Authentication
     ├── Validation
     ├── Error Handling
     └── Not Found
     │
     ▼
Controller
     │
     ▼
Service
     │
     ▼
Mongoose Model
     │
     ▼
MongoDB
     │
     ▼
HTTP Response
```

## Backend configuration

```text
src/config/
├── db.js
└── env.js
```

## Controllers

```text
auth
ayurveda
consultation
dashboard
favorite
goal
healthProfile
notification
profile
progress
recommendation
search
user
yoga
```

## Services

Business logic is separated into:

```text
auth
ayurveda
consultation
dashboard
favorite
goal
healthProfile
notification
profile
progress
recommendation
search
yoga
```

## Models

MongoDB/Mongoose collections are represented by:

```text
Ayurveda
Consultation
Favorite
Goal
HealthProfile
Notification
Progress
Settings
User
Yoga
```

## Middleware

```text
auth.middleware.js
error.middleware.js
notFound.middleware.js
validate.middleware.js
```

## Validation

Dedicated validation modules exist for:

```text
Ayurveda
Consultation
Favorite
Goal
Health Profile
Notification
Profile
Progress
Recommendation
Search
Yoga
```

---

# 🌐 Backend API Catalog

The backend API is versioned under:

```text
/api/v1
```

The route registry is maintained by:

```text
backend/src/routes/index.js
```

The current API domains are:

| API Domain      | Route Module               | Main Responsibility                          |
| --------------- | -------------------------- | -------------------------------------------- |
| Authentication  | `auth.routes.js`           | Signup, login, token lifecycle, current user |
| Ayurveda        | `ayurveda.routes.js`       | Ayurveda content                             |
| Consultation    | `consultation.routes.js`   | Consultation workflow                        |
| Dashboard       | `dashboard.routes.js`      | Dashboard data                               |
| Favorites       | `favorite.routes.js`       | Saved content                                |
| Goals           | `goal.routes.js`           | Wellness goals                               |
| Health Profile  | `healthProfile.routes.js`  | Health information                           |
| Notifications   | `notification.routes.js`   | User notifications                           |
| Profile         | `profile.routes.js`        | Account/profile/settings                     |
| Progress        | `progress.routes.js`       | Wellness progress                            |
| Recommendations | `recommendation.routes.js` | Personalized recommendations                 |
| Search          | `search.routes.js`         | Wellness content search                      |
| Yoga            | `yoga.routes.js`           | Yoga content                                 |
| Users           | `user.controller.js`       | User-related backend operations              |

### API architecture

```text
/api/v1
│
├── /auth
├── /ayurveda
├── /consultation
├── /dashboard
├── /favorites
├── /goals
├── /health-profile
├── /notifications
├── /profile
├── /progress
├── /recommendations
├── /search
└── /yoga
```

> **API accuracy note:** The repository tree establishes these route modules and API domains. Exact endpoint methods and paths are defined by the corresponding `*.routes.js` files and should be treated as the authoritative API contract. This README intentionally does not invent undocumented endpoints.

---

# 🔐 Authentication API

Authentication is handled by:

```text
backend/src/routes/auth.routes.js
backend/src/controllers/auth.controller.js
backend/src/services/auth.service.js
backend/src/middlewares/auth.middleware.js
backend/src/utils/auth.util.js
```

The authentication layer covers:

- Registration
- Login
- Current authenticated user
- Access token handling
- Refresh token handling
- Logout
- Protected requests

### Authentication flow

```text
Signup / Login
      │
      ▼
Credentials Validation
      │
      ▼
Password Verification / Hashing
      │
      ▼
JWT Generation
      │
      ├── Access Token
      └── Refresh Token
      │
      ▼
Mobile Secure Storage
      │
      ▼
Axios Authenticated Requests
      │
      ▼
auth.middleware.js
      │
      ▼
Protected Controller
```

---

# 👤 Profile and Settings API

The profile API provides:

| Method   | Endpoint            | Purpose                          |
| -------- | ------------------- | -------------------------------- |
| `GET`    | `/profile`          | Get authenticated user's profile |
| `PATCH`  | `/profile`          | Update profile information       |
| `PATCH`  | `/profile/password` | Change password                  |
| `GET`    | `/profile/settings` | Get application settings         |
| `PATCH`  | `/profile/settings` | Update application settings      |
| `DELETE` | `/profile/account`  | Deactivate account               |

These endpoints are protected by authentication.

The mobile implementation is located in:

```text
mobile/src/services/profile.service.ts
mobile/src/types/profile.ts
```

---

# 📱 Mobile / Frontend Architecture

The mobile application uses **Expo Router** and follows a route-group architecture.

```text
src/app/
│
├── (public)/
│
├── (onboarding)/
│
└── (main)/
```

The application also uses:

```text
src/components/
src/constants/
src/context/
src/hooks/
src/services/
src/types/
src/utils/
```

This separates:

- Screens
- Reusable components
- Global state/context
- API services
- Types
- Utilities
- Constants

---

# 🗺️ Frontend Routes

## Public

```text
(public)/
├── _layout.tsx
├── landing.tsx
├── login.tsx
└── signup.tsx
```

## Onboarding

```text
(onboarding)/
├── _layout.tsx
├── about-you.tsx
├── physical-health.tsx
├── wellbeing.tsx
├── lifestyle.tsx
├── nutrition.tsx
├── sleep.tsx
├── fitness-yoga.tsx
└── preferences.tsx
```

## Main

```text
(main)/
├── _layout.tsx
├── home.tsx
├── explore.tsx
├── goals.tsx
├── goal-create.tsx
├── progress.tsx
├── progress-create.tsx
├── ayurveda.tsx
├── yoga.tsx
├── favorites.tsx
├── search.tsx
├── health-profile.tsx
├── health-profile-edit.tsx
├── consultation.tsx
├── consultation-book.tsx
├── consultation-history.tsx
├── notifications.tsx
├── profile.tsx
├── profile-edit.tsx
├── change-password.tsx
└── settings.tsx
```

## Detail Screens

```text
(main)/
├── ayurveda/[id].tsx
├── yoga/[id].tsx
├── goals/[id].tsx
├── progress/[id].tsx
└── consultation/[id].tsx
```

---

# 🧩 Frontend Components

Reusable components are grouped by purpose:

```text
components/
├── cards/
├── common/
├── explore/
├── forms/
├── home/
├── navigation/
├── onboarding/
└── ui/
```

### Explore

```text
ExploreCategoryChip.tsx
ExploreContentCard.tsx
ExploreEmptyState.tsx
ExploreSectionHeader.tsx
```

### Home

```text
ConsultationCTA.tsx
GoalsCTA.tsx
HealthProfileCTA.tsx
ProgressCTA.tsx
```

### Navigation

```text
AppDrawer.tsx
DrawerContext.tsx
DrawerItem.tsx
```

### Onboarding

```text
OnboardingDropdown.tsx
OnboardingHeader.tsx
OnboardingOption.tsx
OnboardingProgress.tsx
```

### Forms

```text
Input.tsx
PasswordInput.tsx
```

---

# 🔌 Frontend Services

The mobile API layer is organized under:

```text
mobile/src/services/
```

Current services:

| Service                    | Responsibility          |
| -------------------------- | ----------------------- |
| `api.ts`                   | Axios/API configuration |
| `auth.service.ts`          | Authentication          |
| `consultation.service.ts`  | Consultation API        |
| `dashboard.service.ts`     | Dashboard API           |
| `explore.service.ts`       | Explore/discovery API   |
| `goal.service.ts`          | Goals API               |
| `healthProfile.service.ts` | Health Profile API      |
| `notification.service.ts`  | Notifications API       |
| `profile.service.ts`       | Profile/settings API    |
| `progress.service.ts`      | Progress API            |

This keeps API communication separate from screen UI.

---

# 🧠 Frontend Context and State

The application currently contains:

```text
context/
├── AuthContext.tsx
└── OnboardingContext.tsx
```

## AuthContext

Responsible for:

- Current user
- Authentication state
- Login
- Registration
- Logout
- Loading state

## OnboardingContext

Responsible for maintaining onboarding information across the multi-step onboarding process.

---

# 🧾 Frontend Types

Shared TypeScript domain types are maintained under:

```text
mobile/src/types/
```

Current type modules:

```text
auth.ts
consultation.ts
dashboard.ts
explore.ts
goal.ts
healthProfile.ts
notification.ts
profile.ts
progress.ts
```

This provides stronger typing between:

```text
Screen
   ↓
Service
   ↓
API response
```

---

# 🧾 Onboarding Data Model

The onboarding experience is divided into:

### About You

Personal information such as:

- Date of birth
- Gender
- Height
- Weight
- Occupation

### Physical Health

Examples include:

- Energy
- Digestion
- Skin concerns
- Hair concerns
- Body pain
- Other health concerns

### Wellbeing

Examples include:

- Stress
- Mood
- Focus and concentration
- Ability to relax

### Lifestyle

Examples include:

- Activity level
- Smoking
- Alcohol consumption
- Screen time
- Water intake

### Nutrition

Examples include:

- Diet type
- Meals per day
- Food preferences
- Food allergies

### Sleep

Examples include:

- Average sleep hours
- Sleep quality
- Bedtime
- Wake-up time
- Sleep difficulties

### Fitness & Yoga

Examples include:

- Exercise frequency
- Exercise type
- Yoga experience
- Average daily steps

### Preferences

Examples include:

- Wellness interests
- Preferred yoga duration
- Preferred activity time

---

# 🧠 Personalization

Niramaya is designed so that recommendations can be influenced by multiple user data sources.

```text
Onboarding
    │
    ├── Physical Health
    ├── Wellbeing
    ├── Lifestyle
    ├── Nutrition
    ├── Sleep
    ├── Fitness
    └── Preferences
          │
          ▼
       User Profile
          │
          ├── Goals
          └── Progress History
                 │
                 ▼
        Recommendation Layer
                 │
          ┌──────┴──────┐
          ▼             ▼
        Yoga         Ayurveda
```

The backend includes a dedicated:

```text
recommendation.controller.js
recommendation.service.js
recommendation.validation.js
```

which provides a separate place for recommendation logic.

---

# 🔧 Environment Variables

## Backend `.env`

Create:

```text
backend/.env
```

Use:

```env
NODE_ENV=development
PORT=5000

MONGODB_URI=

JWT_ACCESS_SECRET=
JWT_REFRESH_SECRET=

JWT_ACCESS_EXPIRES_IN=
JWT_REFRESH_EXPIRES_IN=

CLIENT_URL=
```

### Backend environment variables

| Variable                 | Required | Purpose                      |
| ------------------------ | -------- | ---------------------------- |
| `NODE_ENV`               | Yes      | Runtime environment          |
| `PORT`                   | Yes      | Express server port          |
| `MONGODB_URI`            | Yes      | MongoDB connection string    |
| `JWT_ACCESS_SECRET`      | Yes      | Access-token signing secret  |
| `JWT_REFRESH_SECRET`     | Yes      | Refresh-token signing secret |
| `JWT_ACCESS_EXPIRES_IN`  | Yes      | Access-token lifetime        |
| `JWT_REFRESH_EXPIRES_IN` | Yes      | Refresh-token lifetime       |
| `CLIENT_URL`             | Yes      | Client/origin configuration  |

---

## Mobile `.env`

Create:

```text
mobile/.env
```

Use:

```env
EXPO_PUBLIC_API_URL=http://YOUR_IPV4:5000/api/v1
```

For a physical Android/iOS device, use the development computer's reachable LAN IPv4 address.

Example:

```env
EXPO_PUBLIC_API_URL=http://192.168.1.10:5000/api/v1
```

Do not automatically use:

```env
EXPO_PUBLIC_API_URL=http://localhost:5000/api/v1
```

when the application is running on a physical device, because `localhost` refers to the device itself.

---

# 🌐 API Configuration

The frontend API client is:

```text
mobile/src/services/api.ts
```

The expected base URL is:

```text
http://YOUR_IPV4:5000/api/v1
```

Therefore an authenticated request conceptually becomes:

```text
Mobile
  │
  ▼
Axios
  │
  ▼
http://YOUR_IPV4:5000/api/v1/...
  │
  ▼
Express
```

During local development, the backend may be visible on the LAN at:

```text
http://YOUR_IPV4:5000
```

---

# 🔒 Authentication and Security

## Password security

Passwords are handled using:

```text
bcryptjs
```

The intended lifecycle is:

```text
Plain Password
      │
      ▼
Password Hash
      │
      ▼
MongoDB
```

Plain-text passwords should never be stored.

## JWT

Authentication uses:

```text
Access Token
Refresh Token
```

JWT secrets belong only in `.env`.

## Secure mobile storage

The mobile app uses:

```text
expo-secure-store
```

for token storage.

## Request validation

The backend uses:

```text
Zod
```

with dedicated validation modules.

## HTTP security

The backend includes:

```text
Helmet
CORS
Morgan
Centralized Error Middleware
Not Found Middleware
Authentication Middleware
```

---

# 🎨 Design System

Niramaya uses a calm, professional wellness visual language.

### Visual direction

- Earthy greens
- Warm/light neutral backgrounds
- White content cards
- Subtle borders
- Controlled corner radius
- Strong typography hierarchy
- Clean spacing
- Minimal visual noise
- Professional rather than overly decorative UI

### Primary palette

Representative application colors include:

```text
Primary Green      #4D6A50
Dark Green         #263F31
Background         #EEF2E6
Secondary Text     #6D796F
Muted Text         #929B92
Danger             #B65D54
```

### Styling

The mobile application uses:

```text
NativeWind
Tailwind CSS
```

instead of relying primarily on large screen-specific StyleSheet definitions.

---

# 🚀 Installation

## Prerequisites

Install:

- Node.js
- npm
- MongoDB / MongoDB Atlas
- Expo-compatible development environment
- Android Studio for Android development, if required
- Xcode for native iOS development on macOS, if required

---

## Clone / open the repository

```bash
cd "Full-Stack Niramaya App"
```

---

## Backend installation

```bash
cd backend
npm install
```

Create:

```text
backend/.env
```

Configure MongoDB and JWT values.

---

## Mobile installation

Open a second terminal:

```bash
cd mobile
npm install
```

Create:

```text
mobile/.env
```

Configure:

```env
EXPO_PUBLIC_API_URL=http://YOUR_IPV4:5000/api/v1
```

---

# 🌱 Database Setup and Seeding

The backend contains seed scripts for initial wellness content.

## Seed Ayurveda

From `backend/`:

```bash
npm run seed:ayurveda
```

## Seed Yoga

```bash
npm run seed:yoga
```

These scripts populate the corresponding content collections.

---

# ▶️ Running the Monorepo

## Terminal 1 — Backend

```bash
cd backend
npm run dev
```

Production-style start:

```bash
npm start
```

## Terminal 2 — Mobile

```bash
cd mobile
npm start
```

Available Expo commands:

```bash
npm run android
npm run ios
npm run web
```

---

# 📦 Backend Scripts

The backend package currently provides:

```bash
npm run dev
npm start
npm test
npm run seed:ayurveda
npm run seed:yoga
```

| Command                 | Purpose                         |
| ----------------------- | ------------------------------- |
| `npm run dev`           | Development server with Nodemon |
| `npm start`             | Start backend normally          |
| `npm test`              | Test script placeholder         |
| `npm run seed:ayurveda` | Seed Ayurveda content           |
| `npm run seed:yoga`     | Seed Yoga content               |

---

# 📦 Mobile Scripts

The mobile package provides:

```bash
npm start
npm run android
npm run ios
npm run web
npm run lint
```

| Command           | Purpose                 |
| ----------------- | ----------------------- |
| `npm start`       | Start Expo              |
| `npm run android` | Start Expo Android flow |
| `npm run ios`     | Start Expo iOS flow     |
| `npm run web`     | Start Expo web          |
| `npm run lint`    | Run Expo linting        |

---

# 🛠️ Development Guidelines

## Backend

Keep the backend flow:

```text
Route
  ↓
Middleware
  ↓
Controller
  ↓
Service
  ↓
Model
```

Avoid placing large business-logic blocks directly inside routes.

## Frontend

Keep screen logic separated from API communication:

```text
Screen
  ↓
Service
  ↓
Axios
  ↓
Backend API
```

Reusable UI should go under:

```text
src/components/
```

Shared TypeScript types should go under:

```text
src/types/
```

API calls should go under:

```text
src/services/
```

---

# 🐛 Troubleshooting

## Backend does not start

Check:

```bash
cd backend
npm install
npm run dev
```

Then verify:

- `.env` exists
- MongoDB URI is valid
- JWT secrets are present
- Port `5000` is available

---

## Mobile cannot reach backend

Check:

```env
EXPO_PUBLIC_API_URL=http://YOUR_IPV4:5000/api/v1
```

Then verify:

1. Backend is running.
2. Phone and computer can communicate over the network.
3. Windows Firewall is not blocking port `5000`.
4. The API URL includes `/api/v1`.
5. The IP address is the computer's reachable IPv4 address.

---

## Expo does not pick up `.env` changes

Restart Expo after changing environment variables:

```bash
npm start
```

If needed, restart using Expo's cache-clearing option.

---

## Authentication fails

Check:

- MongoDB connection
- JWT access secret
- JWT refresh secret
- API URL
- Secure token storage
- Authentication middleware
- User account status

---

# 📊 Project Status

Current major application areas:

| Module                   | Status |
| ------------------------ | :----: |
| Authentication           |   ✅   |
| Onboarding               |   ✅   |
| Dashboard                |   ✅   |
| Goals                    |   ✅   |
| Progress                 |   ✅   |
| Explore                  |   ✅   |
| Ayurveda                 |   ✅   |
| Yoga                     |   ✅   |
| Search                   |   ✅   |
| Favorites                |   ✅   |
| Health Profile           |   ✅   |
| Consultation             |   ✅   |
| Notifications            |   ✅   |
| Profile                  |   ✅   |
| Settings                 |   ✅   |
| Password Management      |   ✅   |
| Account Deactivation     |   ✅   |
| Custom Drawer Navigation |   ✅   |

---

# 🚀 Future Enhancements

Potential future improvements include:

- Advanced recommendation algorithms
- More intelligent personalization
- Long-term progress analytics
- Progress charts and visualizations
- Personalized daily wellness plans
- Expanded Ayurveda knowledge/content
- Expanded Yoga library
- Richer consultation scheduling
- Online consultation/video support
- Push notifications
- Reminder scheduling
- Offline-first capabilities
- Automated unit/integration testing
- CI/CD
- Production deployment
- Admin/content management
- Accessibility improvements
- Better search/filtering
- More comprehensive wellness analytics

---

# 🎓 MCA Final Year Project

Niramaya demonstrates a broad range of software engineering concepts:

- Full-stack mobile development
- React Native application architecture
- Expo development
- Expo Router
- TypeScript
- NativeWind
- REST API design
- Node.js
- Express
- MongoDB
- Mongoose
- JWT authentication
- Password hashing
- Secure token storage
- Request validation
- Middleware architecture
- Layered backend design
- Reusable frontend components
- Context/state management
- Personalized recommendation architecture
- Modular service architecture
- Database seeding
- Mobile-to-backend integration

---

# 👨‍💻 Authors

**Satinder Singh Sall**  
**Soni Vaibhav Kumar**

**MCA Final Year Project**

---

# 📄 License

The mobile application contains the repository `LICENSE` file.

Refer to the project's license for applicable terms regarding use, modification and distribution.
