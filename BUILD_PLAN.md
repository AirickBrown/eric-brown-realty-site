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
- WordPress
- Custom theme or child theme
- Custom page templates for seller-focused landing pages
- Custom plugin or mu-plugin for lead handling and integrations
- Advanced Custom Fields or native custom fields for editable content
- Gravity Forms or a custom WordPress form workflow for valuation intake

Why this stack:
- Easy for a real estate business to manage after launch
- Strong fit for content-heavy trust-building pages
- Mature ecosystem for forms, SEO, CRM, and IDX integrations
- Good admin experience for updating testimonials, page copy, and contact info
- Practical path for blending marketing pages with lead workflows

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
Suggested scaffold if building with WordPress:

```text
/
  wp-content/
    themes/
      eric-brown-realty/
        style.css
        functions.php
        front-page.php
        page-thank-you.php
        page-search.php
        header.php
        footer.php
        index.php
        template-parts/
          home/
            hero.php
            credibility-strip.php
            testimonials.php
            offer-highlights.php
          shared/
            sticky-contact-bar.php
        assets/
          css/
            main.css
          js/
            main.js
    plugins/
      eric-lead-workflows/
        eric-lead-workflows.php
        includes/
          class-lead-validator.php
          class-lead-submitter.php
          class-podio-integration.php
          class-email-integration.php
          class-sms-integration.php
          class-idx-placeholder.php
  docs/
    ux/
  README.md
```

## Files To Create In Phase 1
Core app scaffold:
- `wp-content/themes/eric-brown-realty/style.css`
- `wp-content/themes/eric-brown-realty/functions.php`
- `wp-content/themes/eric-brown-realty/index.php`
- `wp-content/themes/eric-brown-realty/header.php`
- `wp-content/themes/eric-brown-realty/footer.php`

App routes:
- `wp-content/themes/eric-brown-realty/front-page.php`
- `wp-content/themes/eric-brown-realty/page-thank-you.php`
- `wp-content/themes/eric-brown-realty/page-search.php`

Homepage and form components:
- `wp-content/themes/eric-brown-realty/template-parts/home/hero.php`
- `wp-content/themes/eric-brown-realty/template-parts/home/credibility-strip.php`
- `wp-content/themes/eric-brown-realty/template-parts/home/testimonials.php`
- `wp-content/themes/eric-brown-realty/template-parts/home/offer-highlights.php`
- `wp-content/themes/eric-brown-realty/template-parts/shared/sticky-contact-bar.php`

Content/config files:
- WordPress page content
- WordPress custom fields
- Theme options or plugin settings for contact details and seller offers

Logic and integration placeholders:
- `wp-content/plugins/eric-lead-workflows/eric-lead-workflows.php`
- `wp-content/plugins/eric-lead-workflows/includes/class-lead-validator.php`
- `wp-content/plugins/eric-lead-workflows/includes/class-lead-submitter.php`
- `wp-content/plugins/eric-lead-workflows/includes/class-podio-integration.php`
- `wp-content/plugins/eric-lead-workflows/includes/class-email-integration.php`
- `wp-content/plugins/eric-lead-workflows/includes/class-sms-integration.php`
- `wp-content/plugins/eric-lead-workflows/includes/class-idx-placeholder.php`

## Files Likely To Be Edited Later
As the build expands, these will likely be updated:
- `wp-content/themes/eric-brown-realty/front-page.php`
- `wp-content/themes/eric-brown-realty/functions.php`
- `wp-content/themes/eric-brown-realty/assets/css/main.css`
- `wp-content/plugins/eric-lead-workflows/includes/class-lead-submitter.php`
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
- Post form data through a WordPress form handler, AJAX endpoint, or plugin action
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
- Redirect to the WordPress thank-you page

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

In WordPress terms, these can be:
- Plugin classes
- Service functions
- Action-hooked handlers
- Form plugin feed integrations with custom extension points

## Phase 1 Implementation Sequence
Recommended build order:

1. Set up the WordPress theme and plugin structure
2. Create shared theme styles and layout partials
3. Build the homepage template and seller-focused sections
4. Build the valuation form and validation flow
5. Add the lead intake handler in the custom plugin
6. Add lead orchestration logic
7. Add integration placeholder classes
8. Add the thank-you page template
9. Add sticky mobile call/text bar
10. Configure editable content fields or page content areas
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
- Keep lead processing centralized in one plugin orchestration module
- Avoid wiring provider-specific logic directly into theme templates
- Add TODO comments at every external dependency boundary
- Prefer simple lead data structures over premature abstractions
- Keep theme responsibilities focused on rendering and UX
- Keep plugin responsibilities focused on forms, integrations, and workflow logic

## Suggested Lead Type
Suggested initial lead shape:

```php
$seller_lead = [
    'first_name' => '',
    'last_name' => '',
    'email' => '',
    'phone' => '',
    'property_address' => '',
    'notes' => '',
    'source' => '',
    'created_at' => '',
];
```

## Final Recommendation
Start with Phase 1 and do not broaden scope until the end-to-end valuation submission path works cleanly on mobile.

The most important early milestone is not visual polish. It is a reliable seller lead capture flow with obvious next integration points for email, SMS, Podio, and notifications.
