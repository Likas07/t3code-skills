---
name: website-audit
description: Comprehensive website auditing with deep SEO, technical SEO, schema markup (JSON-LD structured data), performance, security, accessibility, content quality, E-E-A-T assessment, Core Web Vitals, crawlability, indexation, on-page optimization, and 15+ other audit categories using 230+ rules via the squirrelscan CLI. Use when the user wants to audit a website, diagnose SEO or technical issues, review structured data, check site health, fix ranking problems, or generate audit reports.
license: See LICENSE file in repository root
compatibility: Requires squirrel CLI installed and accessible in PATH
metadata:
  author: squirrelscan
  version: "1.18"
allowed-tools: Bash(squirrel:*)
---

# Website Audit Skill

Audit websites for SEO, technical, content, performance, security, schema markup, and more using the squirrelscan CLI. This skill also provides deep SEO audit knowledge, E-E-A-T assessment, and structured data (JSON-LD) implementation guidance.

squirrelscan provides a cli tool squirrel - available for macos, windows and linux. It carries out extensive website auditing
by emulating a browser, search crawler, and analyzing the website's structure and content against over 230+ rules.

It will provide you a list of issues as well as suggestions on how to fix them.

## Links

* squirrelscan website is at [https://squirrelscan.com](https://squirrelscan.com)
* documentation (including rule references) are at [docs.squirrelscan.com](https://docs.squirrelscan.com)

You can look up the docs for any rule with this template:

https://docs.squirrelscan.com/rules/{rule_category}/{rule_id}

example:

https://docs.squirrelscan.com/rules/links/external-links

## What This Skill Does

This skill enables AI agents to audit websites for over 230 rules in 21 categories, including:

- **SEO issues**: Meta tags, titles, descriptions, canonical URLs, Open Graph tags
- **Technical problems**: Broken links, redirect chains, page speed, mobile-friendliness
- **Performance**: Page load time, resource usage, caching, Core Web Vitals
- **Content quality**: Heading structure, image alt text, content analysis, E-E-A-T
- **Security**: Leaked secrets, HTTPS usage, security headers, mixed content
- **Accessibility**: Alt text, color contrast, keyboard navigation
- **Usability**: Form validation, error handling, user flow
- **Links**: Checks for broken internal and external links
- **E-E-A-T**: Expertise, Experience, Authority, Trustworthiness
- **User Experience**: User flow, error handling, form validation
- **Mobile**: Checks for mobile-friendliness, responsive design, touch-friendly elements
- **Crawlability**: Checks for crawlability, robots.txt, sitemap.xml and more
- **Schema**: Schema.org markup, structured data, JSON-LD, rich snippets
- **Legal**: Compliance with legal requirements, privacy policies, terms of service
- **Social**: Open graph, twitter cards and validating schemas, snippets etc.
- **Url Structure**: Length, hyphens, keywords
- **Keywords**: Keyword stuffing
- **Content**: Content structure, headings
- **Images**: Alt text, color contrast, image size, image format
- **Local SEO**: NAP consistency, geo metadata
- **Video**: VideoObject schema, accessibility

and more

The audit crawls the website, analyzes each page against audit rules, and returns a comprehensive report with:
- Overall health score (0-100)
- Category breakdowns (core SEO, technical SEO, content, security)
- Specific issues with affected URLs
- Broken link detection
- Actionable recommendations
- Rules have levels of error, warning and notice and also have a rank between 1 and 10

## When to Use

Use this skill when you need to:

- Analyze a website's health
- Debug technical SEO issues
- Audit on-page SEO (titles, meta descriptions, headings, keyword targeting)
- Assess E-E-A-T signals and content quality
- Fix all of the issues mentioned above
- Check for broken links
- Validate meta tags and structured data
- Add, fix, or optimize schema markup and JSON-LD structured data
- Implement rich snippets (FAQ, Product, Article, HowTo, etc.)
- Generate site audit reports
- Compare site health before/after changes
- Improve website performance, accessibility, SEO, security and more
- Diagnose why a site is not ranking ("why am I not ranking")
- Review technical SEO, crawlability, and indexation issues
- Audit Core Web Vitals and page speed

You should re-audit as often as possible to ensure your website remains healthy and performs well.

## Prerequisites

This skill requires the squirrel CLI to be installed and available in your PATH.

### Installation

If squirrel is not already installed, you can install it using:

```bash
curl -fsSL https://squirrelscan.com/install | bash
```

This will:
- Download the latest release binary
- Install to `~/.local/share/squirrel/releases/{version}/`
- Create a symlink at `~/.local/bin/squirrel`
- Initialize settings at `~/.squirrel/settings.json`

If `~/.local/bin` is not in your PATH, add it to your shell configuration:

```bash
export PATH="$HOME/.local/bin:$PATH"
```

### Windows Installation

Install using PowerShell:

```powershell
irm https://squirrelscan.com/install.ps1 | iex
```

This will:
- Download the latest release binary
- Install to `%LOCALAPPDATA%\squirrel\`
- Add squirrel to your PATH

If using Command Prompt, you may need to restart your terminal for PATH changes to take effect.

### Verify Installation

Check that squirrel is installed and accessible:

```bash
squirrel --version
```

## Setup

Running `squirrel init` will setup a squirrel.toml file for configuration in the current directory.

Each project should have a squirrel project name for the database - by default this is the name of the
website you audit - but you can set it yourself so that you can place all audits for a project in one database

You do this either on init with:

```bash
squirrel init --project-name my-project
# or with aliases
squirrel init -n my-project
# overwrite existing config
squirrel init -n my-project --force
```

or config:

```bash
squirrel config set project.name my-project
```

If there is no squirrel.toml in the directory you're running from CREATE ONE with `squirrel init` and specify the '-n'
parameter for a project name (infer this)

The project name is used to identify the project in the database and is used to generate the database name.

It is stored in ~/.squirrel/projects/<project-name>

## Usage

### Intro

There are three processes that you can run and they're all cached in the local project database:

- crawl - subcommand to run a crawl or refresh, continue a crawl
- analyze - subcommand to analyze the crawl results
- report - subcommand to generate a report in desired format (llm, text, console, html etc.)

the 'audit' command is a wrapper around these three processes and runs them sequentially:

```bash
squirrel audit https://example.com --format llm
```

YOU SHOULD always prefer format option llm - it was made for you and provides an exhaustive and compact output format.

FIRST SCAN should be a surface scan, which is a quick and shallow scan of the website to gather basic information about the website, such as its structure, content, and technology stack. This scan can be done quickly and without impacting the website's performance.

SECOND SCAN should be a deep scan, which is a thorough and detailed scan of the website to gather more information about the website, such as its security, performance, and accessibility. This scan can take longer and may impact the website's performance.

If the user doesn't provide a website to audit - extrapolate the possibilities in the local directory and checking environment variables (ie. linked vercel projects, references in memory or the code).

If the directory you're running for provides for a method to run or restart a local dev server - run the audit against that.

If you have more than one option on a website to audit that you discover - prompt the user to choose which one to audit.

If there is no website - either local, or on the web to discover to audit, then ask the user which URL they would like to audit.

You should PREFER to audit live websites - only there do we get a TRUE representation of the website and performance or rendering issuers.

If you have both local and live websites to audit, prompt the user to choose which one to audit and SUGGEST they choose live.

You can apply fixes from an audit on the live site against the local code.

When planning scope tasks so they can run concurrently as sub-agents to speed up fixes.

When implementing fixes take advantage of subagents to speed up implementation of fixes.

Run typechecking and formatting against generated code when you finish if available in the environment (ruff for python,
biome and tsc for typescript etc.)

### Initial SEO Assessment

**Check for product marketing context first:**
If `.claude/product-marketing-context.md` exists, read it before asking questions. Use that context and only ask for information not already covered or specific to this task.

Before performing a deep SEO audit, understand:

1. **Site Context**
   - What type of site? (SaaS, e-commerce, blog, etc.)
   - What's the primary business goal for SEO?
   - What keywords/topics are priorities?

2. **Current State**
   - Any known issues or concerns?
   - Current organic traffic level?
   - Recent changes or migrations?

3. **Scope**
   - Full site audit or specific pages?
   - Technical + on-page, or one focus area?
   - Access to Search Console / analytics?

### Basic Workflow

The audit process is two steps:

1. **Run the audit** (saves to database, shows console output)
2. **Export report** in desired format

```bash
# Step 1: Run audit (default: console output)
squirrel audit https://example.com

# Step 2: Export as LLM format
squirrel report <audit-id> --format llm
```

### Regression Diffs

When you need to detect regressions between audits, use diff mode:

```bash
# Compare current report against a baseline audit ID
squirrel report --diff <audit-id> --format llm

# Compare latest domain report against a baseline domain
squirrel report --regression-since example.com --format llm
```

Diff mode supports `console`, `text`, `json`, `llm`, and `markdown`. `html` and `xml` are not supported.

### Running Audits

When running an audit:

1. **Fix ALL issues** - critical, high, medium, and low priority
2. **Don't stop early** - continue until score target is reached (see Score Targets below)
3. **Parallelize fixes** - use subagents for bulk content edits (alt text, headings, descriptions)
4. **Iterate** - fix batch -> re-audit -> fix remaining -> re-audit -> until done
5. **Only pause for human judgment** - broken links may need manual review; everything else should be fixed automatically
6. **Show before/after** - present score comparison only AFTER all fixes are complete

**IMPORTANT: Fix ALL issues, don't stop early.**

- **Iteration Loop**: After fixing a batch of issues, re-audit and continue fixing until:
  - Score reaches target (typically 85+), OR
  - Only issues requiring human judgment remain (e.g., "should this link be removed?")

- **Treat all fixes equally**: Code changes (`*.tsx`, `*.ts`) and content changes (`*.md`, `*.mdx`, `*.html`) are equally important. Don't stop after code fixes.

- **Parallelize content fixes**: For issues affecting multiple files:
  - Spawn subagents to fix in parallel
  - Example: 7 files need alt text -> spawn 1-2 agents to fix all
  - Example: 30 files have heading issues -> spawn agents to batch edit

- **Don't ask, act**: Don't pause to ask "should I continue?" - proceed autonomously until complete.

- **Completion criteria**:
  - All errors fixed
  - All warnings fixed (or documented as requiring human review)
  - Re-audit confirms improvements
  - Before/after comparison shown to user
  - Site is complete and fixed (scores above 95 with full coverage)

Run multiple audits to ensure completeness and fix quality. Prompt the user to deploy fixes if auditing a live production, preview, staging or test environment.

### Score Targets

| Starting Score | Target Score | Expected Work |
|----------------|--------------|---------------|
| < 50 (Grade F) | 75+ (Grade C) | Major fixes |
| 50-70 (Grade D) | 85+ (Grade B) | Moderate fixes |
| 70-85 (Grade C) | 90+ (Grade A) | Polish |
| > 85 (Grade B+) | 95+ | Fine-tuning |

A site is only considered COMPLETE and FIXED when scores are above 95 (Grade A) with coverage set to FULL (--coverage full).

**Don't stop until target is reached.**

### Issue Categories

| Category | Fix Approach | Parallelizable |
|----------|--------------|----------------|
| Meta tags/titles | Edit page components or metadata.ts | No |
| Structured data | Add JSON-LD to page templates | No |
| Missing H1/headings | Edit page components + content files | Yes (content) |
| Image alt text | Edit content files | Yes |
| Heading hierarchy | Edit content files | Yes |
| Short descriptions | Edit content frontmatter | Yes |
| HTTP->HTTPS links | Bulk sed/replace in content | Yes |
| Broken links | Manual review (flag for user) | No |

**For parallelizable fixes**: Spawn subagents with specific file assignments.

### Content File Fixes

Many issues require editing content files (`*.md`, `*.mdx`). These are equally important as code fixes:

- **Image alt text**: Edit markdown image tags to add descriptions
- **Heading hierarchy**: Change `###` to `##` where H2 is skipped
- **Meta descriptions**: Extend `excerpt` in frontmatter to 120+ chars
- **HTTP links**: Replace `http://` with `https://` in all links

For 5+ files needing the same fix type, spawn a subagent:
```
Task: Fix missing alt text in 6 posts
Files: [list of files]
Pattern: Find `![](` or `<img src=` without alt, add descriptive text
```

### Parallelizing Fixes with Subagents

Use the **Task tool** to spawn subagents for parallel fixes. Critical rules:

1. **Multiple Task calls in ONE message** = parallel execution
2. **Sequential Task calls** = slower, only when fixes have dependencies
3. **Each subagent gets a focused scope** - don't overload with too many files

**When to parallelize:**
- 5+ files need same fix type (alt text, headings, meta descriptions)
- Fixes have no dependencies on each other
- Files are independent (not importing from each other)

**Subagent prompt structure:**
```
Fix [issue type] in the following files:
- path/to/file1.md
- path/to/file2.md
- path/to/file3.md

Pattern: [what to find]
Fix: [what to change]

Do not ask for confirmation. Make all changes and report what was fixed.
```

**Example - parallel alt text fixes:**

When audit shows 12 files missing alt text, spawn 2-3 subagents in a SINGLE message:

```
[Task tool call 1]
subagent_type: "general-purpose"
prompt: |
  Fix missing image alt text in these files:
  - content/blog/post-1.md
  - content/blog/post-2.md
  - content/blog/post-3.md
  - content/blog/post-4.md

  Find images without alt text (![](path) or <img without alt=).
  Add descriptive alt text based on image filename and context.
  Do not ask for confirmation.

[Task tool call 2]
subagent_type: "general-purpose"
prompt: |
  Fix missing image alt text in these files:
  - content/blog/post-5.md
  - content/blog/post-6.md
  - content/blog/post-7.md
  - content/blog/post-8.md

  [same instructions...]

[Task tool call 3]
subagent_type: "general-purpose"
prompt: |
  Fix missing image alt text in these files:
  - content/blog/post-9.md
  - content/blog/post-10.md
  - content/blog/post-11.md
  - content/blog/post-12.md

  [same instructions...]
```

**Example - parallel heading fixes:**

```
[Task tool call 1]
Fix H1/H2 heading hierarchy in: docs/guide-1.md, docs/guide-2.md, docs/guide-3.md
Change ### to ## where H2 is skipped. Ensure single H1 per page.

[Task tool call 2]
Fix H1/H2 heading hierarchy in: docs/guide-4.md, docs/guide-5.md, docs/guide-6.md
[same instructions...]
```

**Batch sizing:**
- 3-5 files per subagent (optimal)
- Max 10 files per subagent
- Spawn 2-4 subagents for parallel work

**DO NOT parallelize:**
- Shared component edits (layout.tsx, metadata.ts)
- JSON-LD schema changes (single source of truth)
- Config file edits (may conflict)

### Advanced Options

Audit more pages:

```bash
squirrel audit https://example.com --max-pages 200
```

Force fresh crawl (ignore cache):

```bash
squirrel audit https://example.com --refresh
```

Resume interrupted crawl:

```bash
squirrel audit https://example.com --resume
```

Verbose output for debugging:

```bash
squirrel audit https://example.com --verbose
```

## Common Options

### Audit Command Options

| Option | Alias | Description | Default |
|--------|-------|-------------|---------|
| `--format <fmt>` | `-f <fmt>` | Output format: console, text, json, html, markdown, llm | console |
| `--coverage <mode>` | `-C <mode>` | Coverage mode: quick, surface, full | surface |
| `--max-pages <n>` | `-m <n>` | Maximum pages to crawl (max 5000) | varies by coverage |
| `--output <path>` | `-o <path>` | Output file path | - |
| `--refresh` | `-r` | Ignore cache, fetch all pages fresh | false |
| `--resume` | - | Resume interrupted crawl | false |
| `--verbose` | `-v` | Verbose output | false |
| `--debug` | - | Debug logging | false |
| `--trace` | - | Enable performance tracing | false |
| `--project-name <name>` | `-n <name>` | Override project name | from config |

### Coverage Modes

Choose a coverage mode based on your audit needs:

| Mode | Default Pages | Behavior | Use Case |
|------|---------------|----------|----------|
| `quick` | 25 | Seed + sitemaps only, no link discovery | CI checks, fast health check |
| `surface` | 100 | One sample per URL pattern | General audits (default) |
| `full` | 500 | Crawl everything up to limit | Deep analysis |

**Surface mode is smart** - it detects URL patterns like `/blog/{slug}` or `/products/{id}` and only crawls one sample per pattern. This makes it efficient for sites with many similar pages (blogs, e-commerce).

```bash
# Quick health check (25 pages, no link discovery)
squirrel audit https://example.com -C quick --format llm

# Default surface audit (100 pages, pattern sampling)
squirrel audit https://example.com --format llm

# Full comprehensive audit (500 pages)
squirrel audit https://example.com -C full --format llm

# Override page limit for any mode
squirrel audit https://example.com -C surface -m 200 --format llm
```

**When to use each mode:**
- `quick`: CI pipelines, daily health checks, monitoring
- `surface`: Most audits - covers unique templates efficiently
- `full`: Before launches, comprehensive analysis, deep dives

### Report Command Options

| Option | Alias | Description |
|--------|-------|-------------|
| `--list` | `-l` | List recent audits |
| `--severity <level>` | - | Filter by severity: error, warning, all |
| `--category <cats>` | - | Filter by categories (comma-separated) |
| `--format <fmt>` | `-f <fmt>` | Output format: console, text, json, html, markdown, xml, llm |
| `--output <path>` | `-o <path>` | Output file path |
| `--input <path>` | `-i <path>` | Load from JSON file (fallback mode) |

### Config Subcommands

| Command | Description |
|---------|-------------|
| `config show` | Show current config |
| `config set <key> <value>` | Set config value |
| `config path` | Show config file path |
| `config validate` | Validate config file |

### Other Commands

| Command | Description |
|---------|-------------|
| `squirrel feedback` | Send feedback to squirrelscan team |
| `squirrel skills install` | Install Claude Code skill |
| `squirrel skills update` | Update Claude Code skill |

### Self Commands

Self-management commands under `squirrel self`:

| Command | Description |
|---------|-------------|
| `self install` | Bootstrap local installation |
| `self update` | Check and apply updates |
| `self completion` | Generate shell completions |
| `self doctor` | Run health checks |
| `self version` | Show version information |
| `self settings` | Manage CLI settings |
| `self uninstall` | Remove squirrel from the system |

## Output Formats

### Console Output (default)

The `audit` command shows human-readable console output by default with colored output and progress indicators.

### LLM Format

To get LLM-optimized output, use the `report` command with `--format llm`:

```bash
squirrel report <audit-id> --format llm
```

The LLM format is a compact XML/text hybrid optimized for token efficiency (40% smaller than verbose XML):

- **Summary**: Overall health score and key metrics
- **Issues by Category**: Grouped by audit rule category (core SEO, technical, content, security)
- **Broken Links**: List of broken external and internal links
- **Recommendations**: Prioritized action items with fix suggestions

See [OUTPUT-FORMAT.md](references/OUTPUT-FORMAT.md) for detailed format specification.

## Deep SEO Audit Guide

When performing a thorough SEO audit (beyond the automated squirrelscan checks), follow this priority-ordered framework:

### SEO Audit Priority Order

1. **Crawlability & Indexation** (can Google find and index it?)
2. **Technical Foundations** (is the site fast and functional?)
3. **On-Page Optimization** (is content optimized?)
4. **Content Quality** (does it deserve to rank?)
5. **Authority & Links** (does it have credibility?)

### Crawlability Deep Dive

**Robots.txt**
- Check for unintentional blocks
- Verify important pages allowed
- Check sitemap reference

**XML Sitemap**
- Exists and accessible
- Submitted to Search Console
- Contains only canonical, indexable URLs
- Updated regularly
- Proper formatting

**Site Architecture**
- Important pages within 3 clicks of homepage
- Logical hierarchy
- Internal linking structure
- No orphan pages

**Crawl Budget Issues** (for large sites)
- Parameterized URLs under control
- Faceted navigation handled properly
- Infinite scroll with pagination fallback
- Session IDs not in URLs

### Indexation Audit

**Index Status**
- site:domain.com check
- Search Console coverage report
- Compare indexed vs. expected

**Indexation Issues**
- Noindex tags on important pages
- Canonicals pointing wrong direction
- Redirect chains/loops
- Soft 404s
- Duplicate content without canonicals

**Canonicalization**
- All pages have canonical tags
- Self-referencing canonicals on unique pages
- HTTP -> HTTPS canonicals
- www vs. non-www consistency
- Trailing slash consistency

### Core Web Vitals & Site Speed

**Core Web Vitals Thresholds**
- LCP (Largest Contentful Paint): < 2.5s
- INP (Interaction to Next Paint): < 200ms
- CLS (Cumulative Layout Shift): < 0.1

**Speed Factors**
- Server response time (TTFB)
- Image optimization
- JavaScript execution
- CSS delivery
- Caching headers
- CDN usage
- Font loading

**Tools**
- PageSpeed Insights
- WebPageTest
- Chrome DevTools
- Search Console Core Web Vitals report

### Mobile-Friendliness

- Responsive design (not separate m. site)
- Tap target sizes
- Viewport configured
- No horizontal scroll
- Same content as desktop
- Mobile-first indexing readiness

### Security & HTTPS

- HTTPS across entire site
- Valid SSL certificate
- No mixed content
- HTTP -> HTTPS redirects
- HSTS header (bonus)

### On-Page SEO Deep Audit

#### Title Tags

**Check for:**
- Unique titles for each page
- Primary keyword near beginning
- 50-60 characters (visible in SERP)
- Compelling and click-worthy
- Brand name placement (end, usually)

**Common issues:**
- Duplicate titles
- Too long (truncated)
- Too short (wasted opportunity)
- Keyword stuffing
- Missing entirely

#### Meta Descriptions

**Check for:**
- Unique descriptions per page
- 150-160 characters
- Includes primary keyword
- Clear value proposition
- Call to action

**Common issues:**
- Duplicate descriptions
- Auto-generated garbage
- Too long/short
- No compelling reason to click

#### Heading Structure

**Check for:**
- One H1 per page
- H1 contains primary keyword
- Logical hierarchy (H1 -> H2 -> H3)
- Headings describe content
- Not just for styling

**Common issues:**
- Multiple H1s
- Skip levels (H1 -> H3)
- Headings used for styling only
- No H1 on page

#### Content Optimization

**Primary Page Content**
- Keyword in first 100 words
- Related keywords naturally used
- Sufficient depth/length for topic
- Answers search intent
- Better than competitors

**Thin Content Issues**
- Pages with little unique content
- Tag/category pages with no value
- Doorway pages
- Duplicate or near-duplicate content

#### Image Optimization

**Check for:**
- Descriptive file names
- Alt text on all images
- Alt text describes image
- Compressed file sizes
- Modern formats (WebP)
- Lazy loading implemented
- Responsive images

#### Internal Linking

**Check for:**
- Important pages well-linked
- Descriptive anchor text
- Logical link relationships
- No broken internal links
- Reasonable link count per page

**Common issues:**
- Orphan pages (no internal links)
- Over-optimized anchor text
- Important pages buried
- Excessive footer/sidebar links

#### Keyword Targeting

**Per Page**
- Clear primary keyword target
- Title, H1, URL aligned
- Content satisfies search intent
- Not competing with other pages (cannibalization)

**Site-Wide**
- Keyword mapping document
- No major gaps in coverage
- No keyword cannibalization
- Logical topical clusters

#### URL Structure

- Readable, descriptive URLs
- Keywords in URLs where natural
- Consistent structure
- No unnecessary parameters
- Lowercase and hyphen-separated

### E-E-A-T Assessment

**Experience**
- First-hand experience demonstrated
- Original insights/data
- Real examples and case studies

**Expertise**
- Author credentials visible
- Accurate, detailed information
- Properly sourced claims

**Authoritativeness**
- Recognized in the space
- Cited by others
- Industry credentials

**Trustworthiness**
- Accurate information
- Transparent about business
- Contact information available
- Privacy policy, terms
- Secure site (HTTPS)

### Content Quality Assessment

**Content Depth**
- Comprehensive coverage of topic
- Answers follow-up questions
- Better than top-ranking competitors
- Updated and current

**User Engagement Signals**
- Time on page
- Bounce rate in context
- Pages per session
- Return visits

### Common SEO Issues by Site Type

#### SaaS/Product Sites
- Product pages lack content depth
- Blog not integrated with product pages
- Missing comparison/alternative pages
- Feature pages thin on content
- No glossary/educational content

#### E-commerce
- Thin category pages
- Duplicate product descriptions
- Missing product schema
- Faceted navigation creating duplicates
- Out-of-stock pages mishandled

#### Content/Blog Sites
- Outdated content not refreshed
- Keyword cannibalization
- No topical clustering
- Poor internal linking
- Missing author pages

#### Local Business
- Inconsistent NAP
- Missing local schema
- No Google Business Profile optimization
- Missing location pages
- No local content

### SEO Audit Report Structure

When presenting SEO findings, use this structure:

**Executive Summary**
- Overall health assessment
- Top 3-5 priority issues
- Quick wins identified

**Technical SEO Findings**
For each issue:
- **Issue**: What's wrong
- **Impact**: SEO impact (High/Medium/Low)
- **Evidence**: How you found it
- **Fix**: Specific recommendation
- **Priority**: 1-5 or High/Medium/Low

**On-Page SEO Findings**
Same format as above

**Content Findings**
Same format as above

**Prioritized Action Plan**
1. Critical fixes (blocking indexation/ranking)
2. High-impact improvements
3. Quick wins (easy, immediate benefit)
4. Long-term recommendations

## Schema Markup & Structured Data Guide

When fixing schema-related issues from the audit or implementing new structured data, follow this guide.

### Schema Core Principles

1. **Accuracy First** - Schema must accurately represent page content. Don't markup content that doesn't exist. Keep updated when content changes.
2. **Use JSON-LD** - Google recommends JSON-LD format. Easier to implement and maintain. Place in `<head>` or end of `<body>`.
3. **Follow Google's Guidelines** - Only use markup Google supports. Avoid spam tactics. Review eligibility requirements.
4. **Validate Everything** - Test before deploying. Monitor Search Console. Fix errors promptly.

### Common Schema Types Reference

| Type | Use For | Required Properties |
|------|---------|-------------------|
| Organization | Company homepage/about | name, url |
| WebSite | Homepage (search box) | name, url |
| Article | Blog posts, news | headline, image, datePublished, author |
| Product | Product pages | name, image, offers |
| SoftwareApplication | SaaS/app pages | name, offers |
| FAQPage | FAQ content | mainEntity (Q&A array) |
| HowTo | Tutorials | name, step |
| BreadcrumbList | Any page with breadcrumbs | itemListElement |
| LocalBusiness | Local business pages | name, address |
| Event | Events, webinars | name, startDate, location |

### Schema Quick Reference

**Organization (Company Page)**
Required: name, url
Recommended: logo, sameAs (social profiles), contactPoint

**Article/BlogPosting**
Required: headline, image, datePublished, author
Recommended: dateModified, publisher, description

**Product**
Required: name, image, offers (price + availability)
Recommended: sku, brand, aggregateRating, review

**FAQPage**
Required: mainEntity (array of Question/Answer pairs)

**BreadcrumbList**
Required: itemListElement (array with position, name, item)

### Multiple Schema Types on One Page

Combine multiple schema types using `@graph`:

```json
{
  "@context": "https://schema.org",
  "@graph": [
    { "@type": "Organization", "..." : "..." },
    { "@type": "WebSite", "..." : "..." },
    { "@type": "BreadcrumbList", "..." : "..." }
  ]
}
```

### Schema Validation and Testing

**Tools**
- **Google Rich Results Test**: https://search.google.com/test/rich-results
- **Schema.org Validator**: https://validator.schema.org/
- **Search Console**: Enhancements reports

**Common Errors**
- **Missing required properties** - Check Google's documentation for required fields
- **Invalid values** - Dates must be ISO 8601, URLs fully qualified, enumerations exact
- **Mismatch with page content** - Schema doesn't match visible content

### Schema Implementation Patterns

**Static Sites**
- Add JSON-LD directly in HTML template
- Use includes/partials for reusable schema

**Dynamic Sites (React, Next.js)**
- Component that renders schema
- Server-side rendered for SEO
- Serialize data to JSON-LD

**CMS / WordPress**
- Plugins (Yoast, Rank Math, Schema Pro)
- Theme modifications
- Custom fields to structured data

### Schema Testing Checklist

- [ ] Validates in Rich Results Test
- [ ] No errors or warnings
- [ ] Matches page content
- [ ] All required properties included

**For complete JSON-LD examples**: See [schema-examples.md](references/schema-examples.md)

## Examples

### Example 1: Quick Site Audit with LLM Output

```bash
# User asks: "Check squirrelscan.com for SEO issues"
squirrel audit https://squirrelscan.com --format llm
```

### Example 2: Deep Audit for Large Site

```bash
# User asks: "Do a thorough audit of my blog with up to 500 pages"
squirrel audit https://myblog.com --max-pages 500 --format llm
```

### Example 3: Fresh Audit After Changes

```bash
# User asks: "Re-audit the site and ignore cached results"
squirrel audit https://example.com --refresh --format llm
```

### Example 4: Two-Step Workflow (Reuse Previous Audit)

```bash
# First run an audit
squirrel audit https://example.com
# Note the audit ID from output (e.g., "a1b2c3d4")

# Later, export in different format
squirrel report a1b2c3d4 --format llm
```

## Output

On completion give the user a summary of all of the changes you made.

## SEO Tools Reference

**Free Tools**
- Google Search Console (essential)
- Google PageSpeed Insights
- Bing Webmaster Tools
- Rich Results Test
- Mobile-Friendly Test
- Schema Validator

**Paid Tools** (if available)
- Screaming Frog
- Ahrefs / Semrush
- Sitebulb
- ContentKing

## References

- **Output Format Reference**: [OUTPUT-FORMAT.md](references/OUTPUT-FORMAT.md)
- **Schema Markup Examples**: [schema-examples.md](references/schema-examples.md) - Complete JSON-LD examples for Organization, Article, Product, FAQ, HowTo, BreadcrumbList, LocalBusiness, Event, and more
- **AI Writing Detection**: [ai-writing-detection.md](references/ai-writing-detection.md) - Common AI writing patterns to avoid (em dashes, overused phrases, filler words)
- **AEO & GEO Patterns**: [aeo-geo-patterns.md](references/aeo-geo-patterns.md) - Content patterns optimized for answer engines and AI citation
- **squirrelscan Documentation**: https://docs.squirrelscan.com
- **CLI Help**: `squirrel audit --help`

## Troubleshooting

### squirrel command not found

If you see this error, squirrel is not installed or not in your PATH.

**Solution:**
1. Install squirrel: `curl -fsSL https://squirrelscan.com/install | bash`
2. Add to PATH: `export PATH="$HOME/.local/bin:$PATH"`
3. Verify: `squirrel --version`

### Permission denied

If squirrel is not executable:

```bash
chmod +x ~/.local/bin/squirrel
```

### Crawl timeout or slow performance

For very large sites, the audit may take several minutes. Use `--verbose` to see progress:

```bash
squirrel audit https://example.com --format llm --verbose
```

### Invalid URL

Ensure the URL includes the protocol (http:// or https://):

```bash
# Wrong
squirrel audit example.com

# Correct
squirrel audit https://example.com
```

## How It Works

1. **Crawl**: Discovers and fetches pages starting from the base URL
2. **Analyze**: Runs audit rules on each page
3. **External Links**: Checks external links for availability
4. **Report**: Generates LLM-optimized report with findings

The audit is stored in a local database and can be retrieved later with `squirrel report` commands.
