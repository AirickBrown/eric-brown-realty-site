# Eric Website Build Plan

## Purpose
This document turns the planning notes in this repo into a concrete implementation roadmap for a seller-focused real estate website for Eric.

The build should optimize for:
- Seller lead capture first
- Fast follow-up workflows
- Clear trust-building messaging
- Mobile-first conversion UX
- IDX as a secondary feature

## Current Repo State
This repository currently contains planning documents only. There is no existing frontend app, backend service, package manifest, or deployment configuration yet.

Because of that, this plan includes a recommended implementation stack and a proposed file structure for the first working version.

## Recommended Stack
Recommended default stack for this project:
- Next.js
- TypeScript
- App Router
- React
- Tailwind CSS
- Server actions or route handlers for form submission
- Simple provider wrapper modules for Podio, email, SMS, and IDX integration points

Why this stack:
- Fast to scaffold and iterate
- Strong fit for mobile-first marketing pages
- Easy to separate UI, content, and integrations
- Supports lightweight server-side form handling without a separate API project
- Good path for future SEO, analytics, and landing page expansion

## Major Unknowns To Keep As TODOs
These should remain TODO placeholders until real values or vendor choices are provided:
- Podio credentials and field mapping
- Email delivery provider and sender domain
- SMS provider and launch decision
- Eric notification destination and method
- IDX vendor or embed/API strategy
- Brokerage compliance copy and required disclosures
- Testimonials, headshot, and finalized brand copy
- Eric's final phone number, text number, and contact email
- Market/service area copy

## Phase 1 Goal
Build the smallest working seller-focused MVP with:
- Homepage
- Home valuation form
- Thank-you state
- Placeholders for Podio, email, SMS, and IDX integrations
- Mobile-first sticky call/text buttons

Phase 1 is successful when:
- A user can land on the homepage on mobile
- A user can submit the valuation form
- The app shows a confirmation state
- The submission path is structured to later call Podio, email, and SMS services
- Eric contact actions are visible and usable on mobile

## Recommended Initial File Structure
Suggested scaffold if building with Next.js App Router:

```text
/
  app/
    layout.tsx
    page.tsx
    thank-you/
      page.tsx
    search/
      page.tsx
    api/
      leads/
        route.ts
  components/
    home/
      Hero.tsx
      CredibilityStrip.tsx
      Testimonials.tsx
      OfferHighlights.tsx
      SellerCta.tsx
    lead-form/
      HomeValuationForm.tsx
      ThankYouCard.tsx
    shared/
      StickyContactBar.tsx
      Section.tsx
      Button.tsx
      Input.tsx
      Textarea.tsx
  content/
    site.ts
    testimonials.ts
    seller-offer.ts
  lib/
    validation/
      lead.ts
    integrations/
      podio.ts
      email.ts
      sms.ts
      idx.ts
    leads/
      submitLead.ts
  public/
    images/
  styles/
    globals.css
  .env.example
  README.md
```

## Files To Create In Phase 1
Core app scaffold:
- `package.json`
- `tsconfig.json`
- `next.config.js` or `next.config.ts`
- `tailwind.config.ts`
- `postcss.config.js`
- `.env.example`

App routes:
- `app/layout.tsx`
- `app/page.tsx`
- `app/thank-you/page.tsx`
- `app/search/page.tsx`
- `app/api/leads/route.ts`

Homepage and form components:
- `components/home/Hero.tsx`
- `components/home/CredibilityStrip.tsx`
- `components/home/Testimonials.tsx`
- `components/home/OfferHighlights.tsx`
- `components/lead-form/HomeValuationForm.tsx`
- `components/lead-form/ThankYouCard.tsx`
- `components/shared/StickyContactBar.tsx`

Content/config files:
- `content/site.ts`
- `content/testimonials.ts`
- `content/seller-offer.ts`

Logic and integration placeholders:
- `lib/validation/lead.ts`
- `lib/leads/submitLead.ts`
- `lib/integrations/podio.ts`
- `lib/integrations/email.ts`
- `lib/integrations/sms.ts`
- `lib/integrations/idx.ts`

## Files Likely To Be Edited Later
As the build expands, these will likely be updated:
- `app/page.tsx`
- `content/site.ts`
- `content/testimonials.ts`
- `lib/leads/submitLead.ts`
- `.env.example`
- `README.md`

## Phase 1 Detailed Scope

### 1. Homepage
The homepage should be conversion-oriented and seller-first.

Recommended homepage sections:
- Hero with strong seller headline
- Short supporting message about valuation or pre-listing help
- Primary CTA to request home value
- Embedded valuation form or a prominent jump link to the form
- Short credibility section
- Seller offer highlights
- Testimonials
- Contact/footer block

Important behavior:
- Above-the-fold CTA must focus on seller conversion
- Buyer search should be present only as a secondary navigation path

### 2. Home Valuation Form
Required fields:
- First name
- Last name
- Email
- Phone
- Property address
- Optional notes

Recommended validation:
- Require all non-optional fields
- Validate email format
- Validate phone as a plain string initially
- Keep validation messages simple and mobile-friendly

Submission behavior:
- Post form data to a single lead intake function
- Log the submission for development visibility
- Call integration placeholder methods in a predictable order

Recommended lead processing order:
1. Validate payload
2. Save or log intake event
3. Trigger placeholder email workflow
4. Trigger placeholder SMS workflow if enabled
5. Trigger placeholder Podio sync
6. Trigger Eric notification placeholder

### 3. Thank-You State
The thank-you state can be:
- A redirect to `/thank-you`, or
- An inline success state inside the form

Recommended default:
- Redirect to `/thank-you`

Why:
- Easier to measure conversions later
- Cleaner UX on mobile
- Better path for analytics and future follow-up content

The thank-you page should:
- Confirm submission clearly
- Set expectation for follow-up
- Offer call/text contact action
- Optionally link to buyer search as a secondary path

### 4. Sticky Call/Text Buttons
These should remain visible on mobile throughout the homepage.

Recommended behavior:
- Sticky bottom bar on small screens
- `Call Eric` button using `tel:`
- `Text Eric` button using `sms:`
- Clear tap targets and high contrast

### 5. Integration Placeholders
Phase 1 should not fake real external integrations. Instead, it should establish clear interfaces with TODO comments.

Required placeholder modules:
- Podio
- Email
- SMS
- IDX

Each module should:
- Export a clearly named function
- Accept a typed lead payload where relevant
- Return a mocked or no-op result in development
- Include TODO comments for credentials, provider setup, and field mapping

## Phase 1 Implementation Sequence
Recommended build order:

1. Scaffold the Next.js app with TypeScript and Tailwind
2. Create shared design primitives and global styles
3. Build the homepage layout and sections
4. Build the valuation form UI and validation
5. Add lead intake route or server action
6. Add `submitLead` orchestration logic
7. Add integration placeholder modules
8. Add thank-you route
9. Add sticky mobile call/text bar
10. Add content/config files for easy copy updates
11. Smoke test the complete form flow

## Phase 2
Real lead automation and follow-up.

Scope:
- Connect real email provider
- Add Eric notification delivery
- Add real Podio sync
- Add optional SMS workflow
- Add source tracking and timestamps
- Add spam prevention and basic analytics

Definition of done:
- Lead submissions trigger real operational workflows
- Error states are handled gracefully
- Env vars and provider setup are documented

## Phase 3
Seller trust and brand expansion.

Scope:
- Build Sellers page
- Build About Eric page
- Build Contact page
- Expand testimonials and educational content
- Add stronger SEO/local content blocks

Definition of done:
- Trust-building pages support the main homepage funnel without distracting from conversion

## Phase 4
IDX as a secondary feature.

Scope:
- Add Search Homes page
- Integrate chosen IDX provider or embed
- Keep seller-first navigation hierarchy

Definition of done:
- Buyer search is available, but seller conversion remains primary throughout the site

## Phase 5
Production hardening and launch prep.

Scope:
- Accessibility review
- Performance improvements
- Analytics and event tracking
- Error monitoring
- Compliance review
- QA on mobile devices

Definition of done:
- The site is stable, measurable, responsive, and launch-ready

## Technical Notes
- Keep content separate from presentation where possible
- Keep lead processing centralized in one orchestration module
- Avoid wiring provider-specific logic directly into UI components
- Add TODO comments at every external dependency boundary
- Prefer simple typed payloads over premature abstractions

## Suggested Lead Type
Suggested initial lead shape:

```ts
type SellerLead = {
  firstName: string;
  lastName: string;
  email: string;
  phone: string;
  propertyAddress: string;
  notes?: string;
  source: string;
  createdAt: string;
};
```

## Final Recommendation
Start with Phase 1 and do not broaden scope until the end-to-end valuation submission path works cleanly on mobile.

The most important early milestone is not visual polish. It is a reliable seller lead capture flow with obvious next integration points for email, SMS, Podio, and notifications.
