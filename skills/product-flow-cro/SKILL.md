---
name: product-flow-cro
version: 1.0.0
description: When the user wants to optimize any part of the in-product user journey — signup/registration flow, post-signup onboarding and activation, or in-app paywalls and upgrade screens. Also use when the user mentions "signup conversions," "registration friction," "signup form optimization," "free trial signup," "reduce signup dropoff," "account creation flow," "onboarding flow," "activation rate," "user activation," "first-run experience," "empty states," "onboarding checklist," "aha moment," "new user experience," "paywall," "upgrade screen," "upgrade modal," "upsell," "feature gate," "convert free to paid," "freemium conversion," "trial expiration screen," "limit reached screen," "plan upgrade prompt," "in-app pricing," "user journey conversion," or "product flow optimization." Covers the full conversion funnel from account creation through activation to monetization. For lead capture forms (not account creation), see form-cro. For public pricing pages, see page-cro. For ongoing email sequences, see email-sequence.
---

# Product Flow CRO

You are an expert in optimizing the full in-product user journey: **signup to activation to upgrade**. These three stages are deeply interconnected — poor signup hurts onboarding, poor onboarding hurts upgrade conversion. Your goal is to reduce friction at every stage, accelerate time-to-value, and convert free users into paying customers.

## Initial Assessment

**Check for product marketing context first:**
If `.claude/product-marketing-context.md` exists, read it before asking questions. Use that context and only ask for information not already covered or specific to this task.

Before providing recommendations, understand:

1. **Product Context** - What type of product? B2B or B2C? Core value proposition? Freemium, free trial, or paid-only?
2. **Current Journey** - What happens at each stage? Where do users drop off?
3. **Activation Definition** - What's the "aha moment"? What action indicates a user "gets it"?
4. **Monetization Model** - What's free vs. paid? What triggers upgrade prompts? Current conversion rates?
5. **Business Constraints** - Compliance requirements? Data needed at signup? What's behind the paywall?

---

## Shared CRO Methodology

These principles apply across all three journey phases.

### Analytics & Measurement Framework

**Funnel tracking** — Track drop-off at every transition:
```
Visit → Signup Start → Signup Complete → Activation → Retained → Upgrade → Retained Paid
100%      60%             45%              25%          15%        5%         4%
```

Identify the biggest drops and focus there.

**What to track at every stage:**
- Conversion rate (stage entry to stage completion)
- Time through stage
- Drop-off points within stage
- Mobile vs. desktop completion
- Cohort analysis (by source, segment, time period)

**Event instrumentation:**
- Each field/step interaction (focus, blur, error, completion)
- Session recordings for qualitative insight
- Funnel visualization with segment breakdowns

### A/B Testing Principles

- Test one variable at a time per experiment
- Define primary metric and guardrail metrics before launching
- Run tests to statistical significance (not just a few days)
- Segment results by device, source, and user type
- Document learnings regardless of outcome

**For comprehensive experiment ideas across all phases**: See [references/experiments.md](references/experiments.md)

### Output Format

For any audit or recommendation across phases:

**Audit findings** — For each issue:
- **Issue**: What's wrong
- **Impact**: Why it matters (with estimated impact if possible)
- **Fix**: Specific recommendation
- **Priority**: High / Medium / Low

**Recommended changes** — Organized by:
1. Quick wins (same-day fixes)
2. High-impact changes (week-level effort)
3. Test hypotheses (things to A/B test)

---

## Phase 1: Signup & Registration

Reduce friction, increase completion rates, and set users up for successful activation.

### Core Principles

1. **Minimize Required Fields** — Every field reduces conversion. For each field, ask: Do we need this before they can use the product? Can we collect it later? Can we infer it?
2. **Show Value Before Asking for Commitment** — What can you show/give before requiring signup? Can they experience the product first?
3. **Reduce Perceived Effort** — Show progress if multi-step, group related fields, use smart defaults, pre-fill when possible.
4. **Remove Uncertainty** — Clear expectations ("Takes 30 seconds"), show what happens after signup, no surprises.

### Field-by-Field Optimization

**Email Field**
- Single field (no email confirmation)
- Inline validation for format
- Check for common typos (gmial.com -> gmail.com)
- Clear error messages

**Password Field**
- Show/hide toggle (eye icon)
- Show requirements upfront, not after failure
- Strength meter instead of rigid rules
- Allow paste (don't disable)
- Consider passwordless options

**Name Field**
- Single "Full name" field vs. First/Last split (test this)
- Only require if immediately used (personalization)
- Consider making optional

**Social Auth Options**
- Place prominently (often higher conversion than email)
- Show most relevant options for your audience
  - B2C: Google, Apple, Facebook
  - B2B: Google, Microsoft, SSO
- Clear visual separation from email signup
- Consider "Sign up with Google" as primary

**Phone Number** — Defer unless essential. If required, explain why. Use proper input type with country code.

**Company/Organization** — Defer if possible. Auto-suggest as they type. Infer from email domain.

**Use Case / Role Questions** — Defer to onboarding if possible. If needed at signup, keep to one question.

### Single-Step vs. Multi-Step

**Single-step works when:** 3 or fewer fields, simple B2C products, high-intent visitors.

**Multi-step works when:** More than 3-4 fields, complex B2B needing segmentation, different types of info needed.

**Multi-step best practices:**
- Show progress indicator
- Lead with easy questions (name, email)
- Put harder questions later (after psychological commitment)
- Each step should feel completable in seconds
- Allow back navigation
- Save progress (don't lose data on refresh)

**Progressive commitment pattern:**
1. Email only (lowest barrier)
2. Password + name
3. Customization questions (optional)

### Trust and Friction Reduction

**At the form level:**
- "No credit card required" (if true)
- "Free forever" or "14-day free trial"
- Privacy note: "We'll never share your email"
- Security badges if relevant
- Testimonial near signup form

**Error handling:**
- Inline validation (not just on submit)
- Specific error messages ("Email already registered" + recovery path)
- Don't clear the form on error
- Focus on the problem field

**Microcopy:**
- Placeholder text: Use for examples, not labels
- Labels: Always visible (not just placeholders)
- Help text: Only when needed, placed close to field

### Mobile Signup Optimization

- Larger touch targets (44px+ height)
- Appropriate keyboard types (email, tel, etc.)
- Autofill support
- Reduce typing (social auth, pre-fill)
- Single column layout
- Sticky CTA button
- Test with actual devices

### Post-Submit Experience

**Success state:**
- Clear confirmation
- Immediate next step
- If email verification required: explain what to do, easy resend, check spam reminder, option to change email

**Verification flows:**
- Consider delaying verification until necessary
- Magic link as alternative to password
- Let users explore while awaiting verification
- Clear re-engagement if verification stalls

### Common Signup Patterns

| Type | Pattern |
|------|---------|
| B2B SaaS Trial | Email + Password (or Google auth) -> Name + Company -> Onboarding flow |
| B2C App | Google/Apple auth OR Email -> Product experience -> Profile completion later |
| Waitlist/Early Access | Email only -> Optional role/use case -> Waitlist confirmation |
| E-commerce | Guest checkout default -> Account creation optional post-purchase |

### Signup Metrics

- Form start rate (landed -> started filling)
- Form completion rate (started -> submitted)
- Field-level drop-off (which fields lose people)
- Time to complete
- Error rate by field
- Social auth vs. email signup ratio

---

## Phase 2: Onboarding & Activation

Help users reach their "aha moment" as quickly as possible and establish habits that lead to long-term retention.

### Core Principles

1. **Time-to-Value Is Everything** — Remove every step between signup and experiencing core value.
2. **One Goal Per Session** — Focus first session on one successful outcome. Save advanced features for later.
3. **Do, Don't Show** — Interactive > Tutorial. Doing the thing > Learning about the thing.
4. **Progress Creates Motivation** — Show advancement. Celebrate completions. Make the path visible.

### Defining Activation

**Find your aha moment** — The action that correlates most strongly with retention:
- What do retained users do that churned users don't?
- What's the earliest indicator of future engagement?

**Examples by product type:**
- Project management: Create first project + add team member
- Analytics: Install tracking + see first report
- Design tool: Create first design + export/share
- Marketplace: Complete first transaction

**Activation metrics:**
- % of signups who reach activation
- Time to activation
- Steps to activation
- Activation by cohort/source

### Onboarding Flow Design

**Immediate post-signup (first 30 seconds):**

| Approach | Best For | Risk |
|----------|----------|------|
| Product-first | Simple products, B2C, mobile | Blank slate overwhelm |
| Guided setup | Products needing personalization | Adds friction before value |
| Value-first | Products with demo data | May not feel "real" |

Whatever you choose: clear single next action, no dead ends, progress indication if multi-step.

### Onboarding Checklist Pattern

**When to use:** Multiple setup steps, several features to discover, self-serve B2B products.

**Best practices:**
- 3-7 items (not overwhelming)
- Order by value (most impactful first)
- Start with quick wins
- Progress bar / completion %
- Celebration on completion
- Dismiss option (don't trap users)

### Empty States

Empty states are onboarding opportunities, not dead ends.

**Good empty state:**
- Explains what this area is for
- Shows what it looks like with data
- Clear primary action to add first item
- Optional: Pre-populate with example data

### Tooltips and Guided Tours

**When to use:** Complex UI, features that aren't self-evident, power features users might miss.

**Best practices:**
- Max 3-5 steps per tour
- Dismissable at any time
- Don't repeat for returning users

### Multi-Channel Onboarding

**Trigger-based emails:**
- Welcome email (immediate)
- Incomplete onboarding (24h, 72h)
- Activation achieved (celebration + next step)
- Feature discovery (days 3, 7, 14)

**Email should:** Reinforce in-app actions (not duplicate them), drive back to product with specific CTA, be personalized based on actions taken.

### Handling Stalled Users

**Detection:** Define "stalled" criteria (X days inactive, incomplete setup).

**Re-engagement tactics:**
1. **Email sequence** — Reminder of value, address blockers, offer help
2. **In-app recovery** — Welcome back message, pick up where left off
3. **Human touch** — For high-value accounts, personal outreach

### Common Patterns by Product Type

| Product Type | Key Steps |
|--------------|-----------|
| B2B SaaS | Setup wizard -> First value action -> Team invite -> Deep setup |
| Marketplace | Complete profile -> Browse -> First transaction -> Repeat loop |
| Mobile App | Permissions -> Quick win -> Push setup -> Habit loop |
| Content Platform | Follow/customize -> Consume -> Create -> Engage |

### Onboarding Metrics

| Metric | Description |
|--------|-------------|
| Activation rate | % reaching activation event |
| Time to activation | How long to first value |
| Onboarding completion | % completing setup |
| Day 1/7/30 retention | Return rate by timeframe |

---

## Phase 3: Upgrade & Monetization

Convert free users to paid, or upgrade users to higher tiers, at moments when they've experienced enough value to justify the commitment.

### Core Principles

1. **Value Before Ask** — User should have experienced real value first. Upgrade should feel like natural next step. Timing: after "aha moment," not before.
2. **Show, Don't Just Tell** — Demonstrate the value of paid features. Preview what they're missing. Make the upgrade feel tangible.
3. **Friction-Free Path** — Easy to upgrade when ready. Don't make them hunt for pricing.
4. **Respect the No** — Don't trap or pressure. Make it easy to continue free. Maintain trust for future conversion.

### Paywall Trigger Points

**Feature gates** — When user clicks a paid-only feature:
- Clear explanation of why it's paid
- Show what the feature does
- Quick path to unlock
- Option to continue without

**Usage limits** — When user hits a limit:
- Clear indication of limit reached
- Show what upgrading provides
- Don't block abruptly

**Trial expiration** — When trial is ending:
- Early warnings (7, 3, 1 day)
- Clear "what happens" on expiration
- Summarize value received

**Time-based prompts** — After X days of free use:
- Gentle upgrade reminder
- Highlight unused paid features
- Easy to dismiss

### Paywall Screen Components

1. **Headline** — Focus on what they get: "Unlock [Feature] to [Benefit]"
2. **Value Demonstration** — Preview, before/after, "With Pro you could..."
3. **Feature Comparison** — Highlight key differences, current plan marked
4. **Pricing** — Clear, simple, annual vs. monthly options
5. **Social Proof** — Customer quotes, "X teams use this"
6. **CTA** — Specific and value-oriented: "Start Getting [Benefit]"
7. **Escape Hatch** — Clear "Not now" or "Continue with Free"

### Specific Paywall Types

**Feature Lock Paywall:**
```
[Lock Icon]
This feature is available on Pro

[Feature preview/screenshot]

[Feature name] helps you [benefit]:
- [Capability]
- [Capability]

[Upgrade to Pro - $X/mo]
[Maybe Later]
```

**Usage Limit Paywall:**
```
You've reached your free limit

[Progress bar at 100%]

Free: 3 projects | Pro: Unlimited

[Upgrade to Pro]  [Delete a project]
```

**Trial Expiration Paywall:**
```
Your trial ends in 3 days

What you'll lose:
- [Feature used]
- [Data created]

What you've accomplished:
- Created X projects

[Continue with Pro]
[Remind me later]  [Downgrade]
```

### Timing and Frequency Rules

**When to show:**
- After value moment, before frustration
- After activation / aha moment
- When hitting genuine limits

**When NOT to show:**
- During onboarding (too early)
- When they're in a flow
- Repeatedly after dismissal

**Frequency rules:**
- Limit per session
- Cool-down after dismiss (days, not hours)
- Track annoyance signals

### Upgrade Flow Optimization

**From paywall to payment:**
- Minimize steps
- Keep in-context if possible
- Pre-fill known information

**Post-upgrade:**
- Immediate access to features
- Confirmation and receipt
- Guide to new features

### Anti-Patterns to Avoid

**Dark patterns:**
- Hiding the close button
- Confusing plan selection
- Guilt-trip copy

**Conversion killers:**
- Asking before value delivered
- Too frequent prompts
- Blocking critical flows
- Complicated upgrade process

### Upgrade Metrics

- Paywall impression rate
- Click-through to upgrade
- Upgrade completion rate
- Revenue per user
- Churn rate post-upgrade
- Free -> paid conversion rate

---

## Cross-Phase Journey Diagnostics

When analyzing a full product flow, look for these cross-phase issues:

### Signup -> Onboarding Handoff
- Does signup collect info that onboarding asks again? (Eliminate redundancy)
- Is there a clear transition from signup completion to first onboarding step?
- Do signup segmentation answers actually personalize onboarding?

### Onboarding -> Upgrade Handoff
- Does onboarding successfully deliver the aha moment before upgrade prompts appear?
- Are upgrade triggers based on activation signals or arbitrary timers?
- Do stalled onboarding users get re-engagement before paywall exposure?

### Full-Journey Red Flags
- High signup completion but low activation = onboarding problem
- High activation but low upgrade = monetization timing or value problem
- Low signup completion = too much friction or unclear value prop
- High upgrade but high post-upgrade churn = expectation mismatch

---

## Task-Specific Questions

### For Signup Work
1. What's your current signup completion rate?
2. Do you have field-level analytics on drop-off?
3. What data is absolutely required before they can use the product?
4. Are there compliance or verification requirements?

### For Onboarding Work
1. What action most correlates with retention?
2. What happens immediately after signup?
3. Where do users currently drop off in onboarding?
4. What's your activation rate target?
5. Do you have cohort analysis on successful vs. churned users?

### For Upgrade Work
1. What's your current free -> paid conversion rate?
2. What triggers upgrade prompts today?
3. What features are behind the paywall?
4. What pricing model? (per seat, usage, flat)
5. Mobile app, web app, or both?

---

## Related Skills

- **form-cro**: For non-signup forms (lead capture, contact)
- **page-cro**: For landing pages leading to signup, or public pricing pages
- **email-sequence**: For onboarding email series and lifecycle emails
- **ab-test-setup**: For testing changes across any phase
