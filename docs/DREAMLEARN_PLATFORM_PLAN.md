# Dreamlearn Education Pvt Ltd – AI Platform Master Plan

## 1) Vision
Dreamlearn Education should be built as a **secure, scalable, bilingual (Tamil + English) learning platform** with AI-first features for students and easy management for admins.

---

## 2) Final Product Modules

### Public Website
- Home page with branding, tagline, feature highlights, and CTA buttons.
- About page with mission, vision, and founder profile.
- Pricing page with monthly/yearly plans.
- Contact/help page.

### User Authentication
- Register
- Login
- Forgot password (email link)
- Optional OTP login (phase 2)

### Student Dashboard
- Welcome card with user name
- Subscription details
- Payment status (`Paid`, `Pending`, `Expired`)
- Remaining days and expiry date
- Quick launch cards for AI tools

### AI Tools
1. **AI Chatbot**
   - Doubt-solving assistant
   - Tamil + English
   - Context-safe responses for school use
2. **AI Story Generator**
   - Topic-to-story generation
   - Tone/age mode: Kids, School
3. **AI Quiz Generator**
   - Subject + difficulty + number of questions
   - MCQ output with options and answer key

### Admin Panel
- Admin login
- Users list (search + filter)
- Manual payment updates
- Expiry tracking and reminder list
- Add/remove/disable users
- Dashboard analytics (active/pending/expired counts)

---

## 3) Suggested Tech Stack (Production-friendly)

### Frontend
- React + Vite
- Tailwind CSS (or Material UI)
- i18n support for Tamil/English

### Backend API
- Node.js (Express or NestJS)
- JWT auth + refresh tokens
- Role-based access (`admin`, `student`)

### AI Service Layer
- Python (FastAPI) microservice
- OpenAI API integration
- Prompt templates for chatbot, story, and quiz

### Database
- PostgreSQL (recommended) or MySQL
- Redis for sessions/cache/rate limits

### Payments
- Razorpay (India-friendly UPI/Card/NetBanking)
- Webhook verification for payment status updates

### Deployment
- Frontend: Vercel / Netlify
- Backend + AI service: Render / Railway / AWS
- DB: managed PostgreSQL
- Observability: Sentry + uptime monitor

---

## 4) Core Data Model (Minimum)

### `users`
- id
- full_name
- email
- mobile
- password_hash
- role (`student` / `admin`)
- language_pref
- created_at

### `subscriptions`
- id
- user_id
- plan_type (`monthly` / `yearly`)
- start_date
- expiry_date
- status (`active` / `pending` / `expired`)
- amount

### `payments`
- id
- user_id
- provider
- provider_payment_id
- amount
- currency
- status (`created` / `paid` / `failed`)
- paid_at

### `ai_usage_logs`
- id
- user_id
- tool_type (`chatbot` / `story` / `quiz`)
- prompt_tokens
- completion_tokens
- created_at

---

## 5) Status & Remaining Days Logic

```text
remaining_days = expiry_date - today

if remaining_days > 0: Active ✅
if remaining_days == 0: Expiring Today ⚠️
if remaining_days < 0: Expired ❌
```

Run this calculation:
- At login/dashboard load
- In daily scheduled cron job
- After every successful payment webhook

---

## 6) Recommended API Endpoints

### Auth
- `POST /api/auth/register`
- `POST /api/auth/login`
- `POST /api/auth/forgot-password`
- `POST /api/auth/reset-password`

### User
- `GET /api/user/me`
- `GET /api/user/subscription`
- `GET /api/user/payment-history`

### AI
- `POST /api/ai/chat`
- `POST /api/ai/story`
- `POST /api/ai/quiz`

### Payment
- `POST /api/payment/create-order`
- `POST /api/payment/webhook`
- `GET /api/payment/status/:paymentId`

### Admin
- `GET /api/admin/users`
- `PATCH /api/admin/users/:id/subscription`
- `PATCH /api/admin/users/:id/payment-status`
- `GET /api/admin/expiry-report`

---

## 7) Security Checklist
- Password hashing with bcrypt/argon2
- JWT expiration and refresh flow
- CSRF/CORS hardening
- Input validation (Zod/Joi/Pydantic)
- Rate limiting on auth + AI endpoints
- Payment webhook signature validation
- Audit log for admin actions

---

## 8) UI/UX Direction
- Blue + white theme
- Clean card-based dashboard
- Mobile-first responsive layout
- AI-themed icons and subtle gradients
- Accessibility: readable contrast, large tap targets

---

## 9) Domain Suggestions
Preferred:
- `dreamlearneducation.com`
- `dreamlearnedu.in`

Avoid invalid formatting (spaces or broken domain pattern).

---

## 10) Delivery Roadmap (8 Weeks)

### Phase 1 (Week 1-2): Foundation
- Finalize Figma design system
- Setup React + Node + DB projects
- Implement auth flow

### Phase 2 (Week 3-4): Dashboard + Subscription
- Student dashboard
- Payment integration (Razorpay)
- Subscription logic + expiry calculation

### Phase 3 (Week 5-6): AI Features
- Build Python AI service
- Integrate chatbot/story/quiz
- Add bilingual prompts

### Phase 4 (Week 7): Admin Panel
- User/payment/expiry controls
- Manual updates and status corrections

### Phase 5 (Week 8): QA + Launch
- Functional testing
- Security and performance checks
- Production deployment + monitoring

---

## 11) Nice-to-Have (Phase 2+)
- OTP login
- Email/SMS expiry reminders
- Student progress tracking
- Parent dashboard
- Certificate generation

---

## 12) Immediate Next Actions
1. Lock domain and hosting.
2. Create Figma wireframes for Home, Dashboard, AI pages, Admin.
3. Build MVP with auth + subscription + one AI feature first.
4. Add payment + full AI suite.
5. Run pilot with 20-50 students before public launch.
