# Marketing Roadmap — Mini-CRM

## Objectives

1. Establish Mini-CRM as the go-to CRM solution for French artisans (plumbers, electricians, carpenters) in Normandie/Caen by Q3 2026
2. Drive organic and paid acquisition achieving 200 sign-ups by end of year one
3. Build brand recognition in the French artisan market with aided awareness >40% among target segment
4. Generate 50 qualified leads per month through combined digital channels by Q4 2026
5. Achieve 15% conversion rate from free trial to paid tier
6. Secure 5 partnership agreements with artisan suppliers or associations
7. Collect and publish 20 customer testimonials and 5 detailed case studies

## Subdomains

1. `mini-crm.fr` — Main product website (primary domain)
2. `blog.mini-crm.fr` — Content marketing hub
3. `app.mini-crm.fr` — SaaS application (login/dashboard)
4. `docs.mini-crm.fr` — Documentation and help center
5. `help.mini-crm.fr` — Support portal
6. `status.mini-crm.fr` — System status page
7. `caen.mini-crm.fr` — Localized landing page for Caen region
8. `normandie.mini-crm.fr` — Normandie regional hub

## Milestones

- **M1 (Month 1-2):** Brand foundation complete — logo, colors, voice, brand guidelines published
- **M2 (Month 2-3):** Website and landing page live with core pages (home, pricing, features, contact)
- **M3 (Month 3-4):** SEO foundation — keyword research, on-page SEO, Google Business Profile
- **M4 (Month 4-6):** Content engine running — 8 blog posts published, email sequences live
- **M5 (Month 5-7):** Paid acquisition launched — Google Ads and Meta campaigns active
- **M6 (Month 6-8):** First partnerships established, trade show attendance
- **M7 (Month 8-10):** First case studies published, testimonial collection at scale
- **M8 (Month 10-12):** Full funnel optimization, retargeting campaigns, referral program launch

## Task Categories

### Category: Brand Identity

#### Task: brand_name_finalization
- **title**: Finalize product name and register domain
- **description**: Confirm "Mini-CRM" as the product name, verify .fr domain availability, purchase and configure DNS for mini-crm.fr and all subdomains
- **inputs**: List of potential names, trademark search results
- **outputs**: Registered domain, DNS configuration document
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Domain resolves correctly, all subdomains accessible

#### Task: brand_logo_design_primary
- **title**: Design primary logo and icon
- **description**: Create a professional logo representing CRM for artisans. Design concepts combining tool/craft imagery with digital/software feel. Deliver SVG master file, PNG exports (512x512, 192x192, 64x64), favicon.ico
- **inputs**: Mood board of artisan/craft imagery, competitor logos for reference
- **outputs**: Logo files in multiple formats and sizes
- **dependencies**: brand_name_finalization
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Logo renders correctly at all sizes, works on light and dark backgrounds

#### Task: brand_color_palette_definition
- **title**: Define brand color palette
- **description**: Define primary, secondary, accent, and neutral colors with exact HEX, RGB, CMYK, and Pantone values. Create a 5-7 color palette that conveys trust, professionalism, and approachability for tradespeople
- **inputs**: Brand personality brief, competitor color analysis
- **outputs**: Color palette document with all color codes
- **dependencies**: brand_logo_design_primary
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Color palette documented with all formats, passes WCAG AA contrast

#### Task: brand_typography_selection
- **title**: Select primary and secondary typefaces
- **description**: Choose Google Fonts for headings and body text. Primary should feel professional yet approachable. Secondary for UI elements and data display. Document usage rules for each weight and style
- **inputs**: Font comparison research, web font licensing requirements
- **outputs**: Typography spec document with font family, weights, sizes, and line heights
- **dependencies**: brand_color_palette_definition
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: content
- **validation**: Fonts load correctly, render legibly on all devices

#### Task: brand_voice_guidelines
- **title**: Define brand voice and tone guidelines
- **description**: Document the brand voice characteristics (friendly, professional, no-jargon, empowering). Create tone guidelines for different contexts (marketing copy, support emails, blog posts, social media). Include do's and don'ts with examples
- **inputs**: Product positioning, target audience persona
- **outputs**: Voice and tone guide document
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Guidelines enable consistent copy across all channels

#### Task: brand_messaging_framework
- **title**: Create messaging framework (value proposition, tagline, key messages)
- **description**: Develop core messaging hierarchy: tagline, hero statement, three key value propositions, supporting benefits. Tailor messaging for each target persona (solo plumber vs. small team). Create elevator pitch and short description
- **inputs**: Product features, competitor positioning, customer pain points
- **outputs**: Messaging framework document with variations
- **dependencies**: brand_voice_guidelines
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Messaging tested with target audience, resonates with artisan personas

#### Task: brand_icon_library_design
- **title**: Design icon library for UI and marketing
- **description**: Create 30-50 custom icons for features, benefits, and UI elements. Style should match logo aesthetic. Include icons for: invoicing, scheduling, client management, quotes, payments, mobile, dashboard, notifications, calendar, map/location
- **inputs**: Required icon list, brand style guide
- **outputs**: Icon library in SVG and PNG formats
- **dependencies**: brand_logo_design_primary, brand_color_palette_definition
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: marketing
- **validation**: Icons consistent in style, render crisply at 16px to 512px

#### Task: brand_photography_style_guide
- **title**: Create photography style guide
- **description**: Define visual style for product screenshots, team photos, and hero imagery. Specify use of real artisan workplace photos vs. illustrations. Define lighting, composition, and color grading standards
- **inputs**: Reference photography styles, product UI screenshots
- **outputs**: Photography style guide document
- **dependencies**: brand_color_palette_definition
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Guide enables consistent visual production

#### Task: brand_social_media_templates
- **title**: Create social media templates
- **description**: Design branded templates for Facebook, Instagram, LinkedIn posts. Include quote cards, stat graphics, announcement templates, and story templates. Export in platform-specific dimensions
- **inputs**: Brand guidelines, social media strategy
- **outputs**: Figma/Canva template files, exported PNG/PDF templates
- **dependencies**: brand_logo_design_primary, brand_color_palette_definition, brand_typography_selection
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Templates match brand guidelines, easy to customize

#### Task: brand_email_template_design
- **title**: Design transactional and marketing email templates
- **description**: Create branded email templates for: welcome email, onboarding sequence, newsletter, promotional emails, invoice reminders, support responses. Include header, body, and footer designs
- **inputs**: Brand guidelines, email sequence plan
- **outputs**: HTML email templates compatible with email client
- **dependencies**: brand_logo_design_primary, brand_color_palette_definition, brand_typography_selection
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Emails render correctly in Gmail, Outlook, Apple Mail

#### Task: brand_print_material_templates
- **title**: Create print collateral templates
- **description**: Design templates for business cards, flyers, Rolodex cards, and trade show handouts. Include bleed and trim marks, proper color profiles for print
- **inputs**: Brand guidelines, print specifications
- **outputs**: Print-ready PDF files with proper color profiles
- **dependencies**: brand_logo_design_primary, brand_color_palette_definition
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Files meet print shop specifications

#### Task: brand_domain_ssl_setup
- **title**: Configure SSL certificates for all domains and subdomains
- **description**: Install SSL certificates for mini-crm.fr and all subdomains. Set up automatic renewal. Configure HTTPS redirect policies
- **inputs**: Domain registrar access, hosting accounts
- **outputs**: All domains serving HTTPS with valid certificates
- **dependencies**: brand_name_finalization
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: SSL Labs rating A+, no mixed content warnings

#### Task: brand_apple_app_icon
- **title**: Create Apple app icon assets
- **description**: Generate all required iOS app icon sizes (1024x1024 source, all device-specific sizes). Ensure icon works as app icon, notification icon, and settings icon
- **inputs**: Primary logo SVG
- **outputs**: All iOS icon sizes in PNG format
- **dependencies**: brand_logo_design_primary
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Icons pass Apple Human Interface Guidelines review

#### Task: brand_android_play_icon
- **title**: Create Android Play Store icon assets
- **description**: Generate adaptive icon assets for Android (512x512 source, all density versions). Create legacy icons for older Android versions
- **inputs**: Primary logo SVG
- **outputs**: All Android icon assets in PNG format
- **dependencies**: brand_logo_design_primary
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Icons meet Google Play Store requirements

#### Task: brand_url_structure_optimization
- **title**: Define URL structure for all pages
- **description**: Create SEO-friendly URL structure for main site, blog, documentation, and marketing pages. Define canonical URL patterns, redirect rules, and URL shortening strategy for social
- **inputs**: Site architecture plan, SEO keyword targets
- **outputs**: URL structure document with examples
- **dependencies**: brand_name_finalization
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: SEO
- **validation**: URLs are clean, readable, and consistent

### Category: Website & Landing Page

#### Task: site_hosting_ovh_vps_setup
- **title**: Set up hosting on OVH VPS
- **description**: Provision OVH VPS instance, install required software (nginx, Node.js, databases), configure server security (firewall, SSH keys, fail2ban), set up staging environment separate from production
- **inputs**: OVH account, server requirements document
- **outputs**: Running VPS with staging and production environments
- **dependencies**: brand_domain_ssl_setup
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: marketing
- **validation**: Site loads in under 3 seconds, staging accessible via password

#### Task: site_main_landing_page_build
- **title**: Build main landing page
- **description**: Create the primary conversion-focused landing page. Sections: hero with headline and CTA, pain point section, features overview, pricing preview, testimonials carousel, FAQ, final CTA. Mobile-first responsive design
- **inputs**: Brand guidelines, copywriting, product screenshots
- **outputs**: Fully functional landing page at mini-crm.fr
- **dependencies**: site_hosting_ovh_vps_setup, brand_messaging_framework, brand_logo_design_primary
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: marketing
- **validation**: Page passes Lighthouse audit (90+ performance), renders correctly on mobile

#### Task: site_pricing_page_build
- **title**: Build pricing page
- **description**: Create dedicated pricing page with three tiers (29/49/79EUR). Feature comparison table, FAQ section, testimonials per tier, money-back guarantee mention. Include annual discount callout (2 months free)
- **inputs**: Pricing strategy, feature matrix, competitor pricing
- **outputs**: Functional pricing page with tier comparison
- **dependencies**: site_main_landing_page_build
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Pricing displays correctly, CTAs link to checkout, annual pricing calculates correctly

#### Task: site_features_page_build
- **title**: Build features detail page
- **description**: Create comprehensive features page with dedicated sections for each major feature: client management, invoicing, scheduling, quotes, payments, reporting. Include demo videos or screenshots for each
- **inputs**: Product feature list, screen recordings
- **outputs**: Feature detail page with navigation anchors
- **dependencies**: site_main_landing_page_build
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: All features documented, links work, videos embed correctly

#### Task: site_contact_page_build
- **title**: Build contact page
- **description**: Create contact page with contact form (name, email, phone, message, business type), embedded map showing Caen office, direct email link, and social media links. Integrate with CRM to create leads from submissions
- **inputs**: Business address, social media links
- **outputs**: Functional contact page with lead capture
- **dependencies**: site_main_landing_page_build
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Form submissions received in CRM, map renders correctly

#### Task: site_about_page_build
- **title**: Build about us page
- **description**: Create about page with company story, mission statement, team photos and bios, company values, and photos of the office/workshop. Build trust with potential customers
- **inputs**: Team information, company story, photos
- **outputs**: About page with compelling narrative
- **dependencies**: site_main_landing_page_build, brand_photography_style_guide
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: content
- **validation**: Page renders correctly, photos optimized for web

#### Task: site_blog_setup
- **title**: Set up blog infrastructure
- **description**: Install and configure blog platform (Ghost or WordPress) on blog.mini-crm.fr. Set up categories, tags, author profiles, email subscription widget, and social sharing buttons
- **inputs**: Hosting environment, platform choice
- **outputs**: Functional blog with admin access configured
- **dependencies**: site_hosting_ovh_vps_setup
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Blog accessible, admin works, RSS feed generated

#### Task: site_docs_setup
- **title**: Set up documentation site
- **description**: Install documentation platform (GitBook or Docusaurus) on docs.mini-crm.fr. Create initial structure: Getting Started, Invoicing, Client Management, Scheduling, Billing, API, Troubleshooting
- **inputs**: Documentation content outline, product screenshots
- **outputs**: Functional documentation site
- **dependencies**: site_hosting_ovh_vps_setup
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Documentation searchable, renders correctly, links work

#### Task: site_caen_landing_page
- **title**: Build Caen-specific landing page
- **description**: Create localized landing page for Caen region. Include Caen-specific testimonials, mention of local support, Caen business statistics, and map of service area. Target Caen and Calvados keywords
- **inputs**: Local market research, testimonials from Caen customers
- **outputs**: Caen-specific landing page at caen.mini-crm.fr
- **dependencies**: site_main_landing_page_build, seo_local_caen_gmb_setup
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: SEO
- **validation**: Page indexed for Caen keywords, localized content renders correctly

#### Task: site_performance_optimization
- **title**: Optimize site performance
- **description**: Implement image optimization (WebP, lazy loading), minify CSS/JS, enable browser caching, set up CDN for static assets, optimize font loading, implement critical CSS
- **inputs**: Lighthouse audit results
- **outputs**: Optimized site with 90+ Lighthouse scores
- **dependencies**: site_main_landing_page_build
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: SEO
- **validation**: Lighthouse performance score 90+, page load under 2 seconds

#### Task: site_mobile_optimization
- **title**: Optimize for mobile experience
- **description**: Ensure all pages are fully responsive, touch-friendly, and fast on mobile. Test on iOS Safari and Android Chrome. Fix any horizontal scroll issues, small tap targets, or font sizing problems
- **inputs**: Mobile testing devices or emulators
- **outputs**: Fully mobile-optimized site
- **dependencies**: site_main_landing_page_build
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Google Mobile-Friendly Test passes, manual testing on iPhone and Android

#### Task: site_analytics_setup
- **title**: Set up Google Analytics 4
- **description**: Install GA4 tracking on all pages. Configure conversions for key actions: signup, trial start, pricing page view, contact form submit. Set up custom dashboards for traffic sources, user behavior, and conversion tracking
- **inputs**: GA4 property, tracking code
- **outputs**: GA4 fully configured with all events tracked
- **dependencies**: site_main_landing_page_build
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Data flowing into GA4, conversions tracking accurately

#### Task: site_heatmap_setup
- **title**: Set up heatmap and session recording
- **description**: Install Hotjar or Microsoft Clarity on main site. Configure heatmaps for landing page, pricing page, and blog. Set up conversion funnel tracking
- **inputs**: Hotjar/Clarity account
- **outputs**: Heatmaps and recordings available for analysis
- **dependencies**: site_main_landing_page_build
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Heatmaps generating data, sessions recording

#### Task: site_chat_widget_setup
- **title**: Install live chat widget
- **description**: Install Crisp or Tidio chat widget on site. Configure chatbot for common FAQ responses. Set up notification for new leads, offline message capture
- **inputs**: Chat service account
- **outputs**: Chat widget functional on all pages
- **dependencies**: site_main_landing_page_build
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Chat loads, messages received, chatbot responds to FAQ

#### Task: site_cookie_consent
- **title**: Implement cookie consent banner
- **description**: Install cookie consent banner compliant with CNIL (French data protection). Block tracking until consent given. Provide granular cookie preferences
- **inputs**: Cookie audit results, CNIL requirements
- **outputs**: Functional cookie consent with proper blocking
- **dependencies**: site_main_landing_page_build
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Banner displays, consent choices respected, CNIL compliant

#### Task: site_favicon_setup
- **title**: Create and install favicon
- **description**: Create multi-resolution favicon from logo (favicon.ico, apple-touch-icon.png, favicon-16x16.png, favicon-32x32.png, android-chrome-192x192.png, android-chrome-512x512.png)
- **inputs**: Logo SVG
- **outputs**: All favicon variants installed and linked
- **dependencies**: brand_logo_design_primary
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Favicon displays in browser tabs and bookmarks

#### Task: site_robots_txt
- **title**: Create robots.txt file
- **description**: Create robots.txt allowing crawlers to index main content while blocking admin, staging, and duplicate content paths. Include sitemap location
- **inputs**: Site structure, staging URLs to block
- **outputs**: robots.txt file at root
- **dependencies**: site_main_landing_page_build
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: SEO
- **validation**: robots.txt accessible, correct directives

#### Task: site_sitemap_generation
- **title**: Generate XML sitemap
- **description**: Create comprehensive XML sitemap including main site, blog posts, documentation pages. Submit to Google Search Console. Set up automatic sitemap regeneration on new content
- **inputs**: All page URLs
- **outputs**: Valid XML sitemap, Search Console submission
- **dependencies**: site_main_landing_page_build, site_blog_setup
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: SEO
- **validation**: Sitemap validates, Search Console accepts, all pages indexed

#### Task: site_404_page
- **title**: Create custom 404 error page
- **description**: Create branded 404 page with helpful navigation, search bar, and links to main pages. Include friendly message and suggestions
- **inputs**: Brand guidelines
- **outputs**: Custom 404 page functional
- **dependencies**: site_main_landing_page_build
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: 404 page displays for non-existent URLs

### Category: SEO

#### Task: seo_keyword_research_french
- **title**: Conduct French keyword research for artisan CRM
- **description**: Research French keywords for: CRM artisan, logiciel CRM plombier, gestion clients electricien, logiciel artisan, gestion chantier artisan. Include head terms and long-tail variations. Analyze search volume, competition, and keyword difficulty
- **inputs**: Competitor sites, seed keywords, French SEO tools
- **outputs**: Comprehensive keyword list with search volume and competition data
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: SEO
- **validation**: Keyword list with 200+ terms, prioritized by opportunity

#### Task: seo_local_caen_keywords
- **title**: Research Caen and Normandie specific keywords
- **description**: Research local keywords: CRM Caen, logiciel artisan Normandie, gestion clients Calvados. Identify geo-modified terms and local business intent keywords
- **inputs**: Local business list, geographic terms
- **outputs**: Local keyword list with search volume
- **dependencies**: seo_keyword_research_french
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: SEO
- **validation**: 50+ local keywords identified and documented

#### Task: seo_competitor_analysis
- **title**: Analyze competitor SEO strategies
- **description**: Analyze top 5 competitor websites for SEO: backlinks, on-page optimization, content strategy, keyword rankings, domain authority. Identify gaps and opportunities
- **inputs**: Competitor URL list
- **outputs**: Competitor analysis report with actionable insights
- **dependencies**: seo_keyword_research_french
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: SEO
- **validation**: Report with 10+ actionable recommendations

#### Task: seo_onpage_audit
- **title**: Conduct on-page SEO audit
- **description**: Audit all existing pages for title tags, meta descriptions, H1-H6 hierarchy, image alt text, internal linking, schema markup, and content optimization
- **inputs**: Site crawl data
- **outputs**: Audit report with prioritized fixes
- **dependencies**: site_main_landing_page_build
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: SEO
- **validation**: Audit complete, 100% of issues documented

#### Task: seo_title_tag_optimization
- **title**: Optimize title tags for all pages
- **description**: Write unique, keyword-rich title tags for each page (50-60 characters). Include primary keyword and brand name. Target different keywords per page based on keyword mapping
- **inputs**: Keyword list, page inventory
- **outputs**: Optimized title tags for all pages
- **dependencies**: seo_keyword_research_french, seo_onpage_audit
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: SEO
- **validation**: All titles unique, correct length, include target keywords

#### Task: seo_meta_description_optimization
- **title**: Optimize meta descriptions for all pages
- **description**: Write compelling meta descriptions with target keywords and CTAs (150-160 characters). Each page gets unique, action-oriented description
- **inputs**: Keyword list, page inventory
- **outputs**: Optimized meta descriptions for all pages
- **dependencies**: seo_keyword_research_french, seo_onpage_audit
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: SEO
- **validation**: All meta descriptions unique, correct length, include keywords

#### Task: seo_header_tag_structure
- **title**: Implement proper H1-H6 header structure
- **description**: Ensure each page has exactly one H1, logical H2-H6 hierarchy, and proper keyword distribution across headers. Fix any missing or duplicate H1 tags
- **inputs**: Page inventory, audit report
- **outputs**: Corrected header structure across all pages
- **dependencies**: seo_onpage_audit
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: SEO
- **validation**: Each page has single H1, logical hierarchy, keywords in headers

#### Task: seo_image_optimization
- **title**: Optimize all images with alt text and compression
- **description**: Add descriptive alt text to all images including target keywords where relevant. Compress images to WebP format, ensure proper dimensions. Remove unnecessary images
- **inputs**: Image inventory, keyword list
- **outputs**: All images optimized with proper alt text
- **dependencies**: seo_onpage_audit, site_performance_optimization
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: SEO
- **validation**: All images have descriptive alt text, compressed to WebP

#### Task: seo_schema_markup
- **title**: Implement structured data/schema markup
- **description**: Add Schema.org markup for: Organization, LocalBusiness, SoftwareApplication, FAQPage, BreadcrumbList, Organization with social links. Test with Rich Results Test
- **inputs**: Schema documentation, page inventory
- **outputs**: Schema markup implemented and validated
- **dependencies**: seo_onpage_audit
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: SEO
- **validation**: Schema passes Google Rich Results Test

#### Task: seo_internal_linking_strategy
- **title**: Develop and implement internal linking strategy
- **description**: Create internal linking map connecting related content. Implement contextual links in blog posts to product pages. Add related content sections. Fix any orphaned pages
- **inputs**: Page inventory, content map
- **outputs**: Internal linking implemented, link equity distributed
- **dependencies**: site_blog_setup
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: SEO
- **validation**: All pages have internal links, no orphaned pages

#### Task: seo_local_caen_gmb_setup
- **title**: Set up Google My Business profile
- **description**: Create and verify Google My Business listing for Mini-CRM office in Caen. Add complete business information, photos, hours, services, and posts. Enable messaging
- **inputs**: Business address, phone, hours, photos
- **outputs**: Verified GMB listing live
- **dependencies**: brand_logo_design_primary
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: SEO
- **validation**: GMB listing verified, appears in local search

#### Task: seo_local_directories_submission
- **title**: Submit to French business directories
- **description**: Submit business to French directories: PagesJaunes, Kompass, Verif, Societe.com, Mistersgoodpost, and local Caen/Normandie directories. Ensure NAP consistency
- **inputs**: Business information, directory list
- **outputs**: Listings on 20+ directories
- **dependencies**: seo_local_caen_gmb_setup
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: SEO
- **validation**: Listings appear on major directories, NAP consistent

#### Task: seo_backlink_acquisition
- **title**: Develop backlink acquisition strategy
- **description**: Identify link building opportunities: guest posts on artisan blogs, industry associations, local business partners, press mentions, resource page links. Create outreach list
- **inputs**: Competitor backlinks, industry contacts
- **outputs**: List of 50+ link opportunities with contact info
- **dependencies**: seo_competitor_analysis
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: SEO
- **validation**: Outreach list complete, 10+ active prospects

#### Task: seo_technical_audit
- **title**: Conduct technical SEO audit
- **description**: Audit site for: crawlability, indexability, page speed, mobile-friendliness, HTTPS, duplicate content, hreflang tags, canonical tags, XML sitemap issues, robots.txt blocking
- **inputs**: Site crawl, Search Console data
- **outputs**: Technical SEO report with prioritized fixes
- **dependencies**: site_hosting_ovh_vps_setup
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: SEO
- **validation**: All technical issues documented and prioritized

#### Task: seo_core_web_vitals_optimization
- **title**: Optimize Core Web Vitals
- **description**: Improve LCP (largest contentful paint), FID (first input delay), and CLS (cumulative layout shift). Optimize server response time, render-blocking resources, and layout stability
- **inputs**: PageSpeed Insights data
- **outputs**: Core Web Vitals scores in green range
- **dependencies**: site_performance_optimization
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: SEO
- **validation**: All Core Web Vitals pass Google's "Good" threshold

#### Task: seo_search_console_setup
- **title**: Set up Google Search Console
- **description**: Verify site ownership in Search Console, submit XML sitemap, configure URL parameters, set up email alerts for critical issues, claim viewport verification
- **inputs**: Search Console account
- **outputs**: Search Console configured with all properties
- **dependencies**: site_main_landing_page_build
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: SEO
- **validation**: Search Console shows site data, alerts configured

#### Task: seo_french_search_console
- **title**: Configure Search Console for French region
- **description**: Set international targeting to France in Search Console. Configure hreflang for fr-FR. Monitor French-specific search performance
- **inputs**: Search Console access
- **outputs**: Search Console shows French targeting
- **dependencies**: seo_search_console_setup
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: SEO
- **validation**: International targeting set to France

#### Task: seo_blog_seo_optimization
- **title**: Optimize blog for SEO
- **description**: Apply on-page SEO to all blog posts: optimize titles, meta descriptions, headers, images, internal links, and URL slugs. Implement category and tag SEO. Add related posts
- **inputs**: Blog post list, keyword targets
- **outputs**: All blog posts fully optimized
- **dependencies**: site_blog_setup
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: SEO
- **validation**: All posts have optimized on-page SEO

#### Task: seo_breadcrumb_implementation
- **title**: Implement breadcrumb navigation with schema
- **description**: Add breadcrumb navigation to all pages with proper schema markup. Ensure breadcrumbs show correct hierarchy and are consistent with URL structure
- **inputs**: Site structure
- **outputs**: Breadcrumbs implemented with schema
- **dependencies**: seo_schema_markup
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: SEO
- **validation**: Breadcrumbs display on pages, schema validates

#### Task: seo_faq_page_creation
- **title**: Create FAQ page with schema
- **description**: Create comprehensive FAQ page covering common questions about CRM for artisans, pricing, technical requirements, data security, onboarding. Implement FAQ schema for rich snippets
- **inputs**: Customer support common questions
- **outputs**: FAQ page with schema markup
- **dependencies**: seo_schema_markup
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: SEO
- **validation**: FAQ page live, schema validates, rich snippets appear

### Category: Content Marketing

#### Task: content_blog_content_calendar
- **title**: Create 6-month blog content calendar
- **description**: Plan 24 blog posts covering: invoicing tips for artisans, client management best practices, time tracking, scheduling, tax tips for French craftsmen, industry news. Include publishing frequency (2x/month), topics, keywords, and assign to writers
- **inputs**: Keyword research, audience persona, competitor blog analysis
- **outputs**: 6-month editorial calendar document
- **dependencies**: seo_keyword_research_french
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Calendar complete with all 24 posts planned

#### Task: content_invoicing_guide_artisans
- **title**: Write comprehensive guide: "Facturation pour Artisans en 2026"
- **description**: Write 2000+ word guide covering French invoicing requirements for artisans, mandatory fields, e-invoicing mandates (Chorus Pro), best practices, common mistakes, and software recommendations. Include templates and examples
- **inputs**: French invoicing regulations, artisan pain points
- **outputs**: Published blog post with downloadable template
- **dependencies**: content_blog_content_calendar
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Guide published, indexed by search engines

#### Task: content_client_management_guide
- **title**: Write guide: "Gestion Clients pour Artisans: Le Guide Complet"
- **description**: Write 1500+ word guide on client management for tradespeople. Topics: client database importance, communication tips, follow-up strategies, client segmentation, retaining clients for repeat business
- **inputs**: Best practices research, customer interviews
- **outputs**: Published blog post
- **dependencies**: content_blog_content_calendar
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Guide published with client management tips

#### Task: content_time_tracking_guide
- **title**: Write guide: "Suivi du Temps pour Artisans: Pourquoi et Comment"
- **description**: Write guide on time tracking importance for artisans. Topics: billing accuracy, productivity analysis, project profitability, tools and apps, simple methods for busy tradespeople
- **inputs**: Time tracking best practices, artisan workflow
- **outputs**: Published blog post
- **dependencies**: content_blog_content_calendar
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Guide published with actionable time tracking tips

#### Task: content_tax_tips_artisans
- **title**: Write guide: "Conseils Fiscaux pour Artisans en France"
- **description**: Write guide on tax obligations for French artisans. Topics: auto-entrepreneur vs. SAS, deductions, CFE, TVA rules, expense tracking, key dates and deadlines. Disclaimer to consult accountant
- **inputs**: French tax regulations for artisans, professional advice
- **outputs**: Published blog post with disclaimer
- **dependencies**: content_blog_content_calendar
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Guide published with proper tax disclaimer

#### Task: content_quote_creation_guide
- **title**: Write guide: "Comment Creer des Devis Professionnels"
- **description**: Write guide on creating effective quotes/proposals for artisan services. Topics: quote structure, pricing strategies, common mistakes, follow-up techniques, conversion optimization
- **inputs**: Sales best practices, artisan feedback
- **outputs**: Published blog post
- **dependencies**: content_blog_content_calendar
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**:Guide published with quote templates

#### Task: content_seasonal_maintenance_tips
- **title**: Write seasonal maintenance tips content
- **description**: Write blog post series on seasonal maintenance tips for homes (heating system check before winter, AC before summer). Target seasonal search intent
- **inputs**: Seasonal trends, common artisan services
- **outputs**: 4 seasonal blog posts (one per season)
- **dependencies**: content_blog_content_calendar
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: content
- **validation**: All 4 seasonal posts published

#### Task: content_industry_news_roundup
- **title**: Write monthly industry news roundup
- **description**: Create monthly "Actualites Artisanat" post summarizing relevant news: regulatory changes, industry trends, new technologies, trade shows. Position as a trusted industry news source
- **inputs**: Industry news sources, RSS feeds
- **outputs**: 6 monthly roundup posts
- **dependencies**: content_blog_content_calendar
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: content
- **validation**: 6 roundup posts published on schedule

#### Task: content_customer_interview_series
- **title**: Launch customer interview series
- **description**: Create a series of interview-style blog posts featuring Mini-CRM customers. Topics: how they use the product, challenges solved, productivity gains. Include photos of their work
- **inputs**: Willing customer participants, interview questions
- **outputs**: 6 customer interview posts
- **dependencies**: social_proof_testimonial_collection_initial
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: 6 interviews published with customer permission

#### Task: content_software_comparison_posts
- **title**: Write comparison posts vs competitors
- **description**: Write comparison posts: "Mini-CRM vs [competitor]" for 3 main competitors. Honest, feature-based comparisons highlighting Mini-CRM advantages. Target comparison search queries
- **inputs**: Competitor feature lists, pricing, Mini-CRM advantages
- **outputs**: 3 comparison blog posts
- **dependencies**: seo_competitor_analysis, content_blog_content_calendar
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Comparison posts indexed for target keywords

#### Task: content_howto_video_scripts
- **title**: Write video scripts for YouTube tutorials
- **description**: Write scripts for 10 YouTube tutorial videos: product demos, how-to guides, tips and tricks. Each script 5-10 minutes, include hook, content, and CTA
- **inputs**: Product features, common user questions
- **outputs**: 10 video scripts
- **dependencies**: site_features_page_build
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Scripts complete, approved, ready for filming

#### Task: content_downloadable_checklist_freelance
- **title**: Create downloadable checklist: "Checklist Demarrage Auto-Entrepreneur"
- **description**: Create a valuable lead magnet: checklist for starting as auto-entrepreneur artisan. Includes registration steps, insurance requirements, tools needed, first client checklist. Gate behind email signup
- **inputs**: Auto-entrepreneur requirements, design template
- **outputs**: Landing page, PDF checklist, email integration
- **dependencies**: site_main_landing_page_build, brand_design_assets
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Checklist downloadable, email capture working

#### Task: content_downloadable_invoice_template
- **title**: Create downloadable invoice template for artisans
- **description**: Create Excel/Google Sheets invoice template customized for French artisans with formula examples, mandatory fields highlighted, VAT calculations. Gate behind email signup
- **inputs**: French invoicing requirements, spreadsheet template
- **outputs**: Landing page, downloadable template, email integration
- **dependencies**: content_invoicing_guide_artisans
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Template downloadable, leads captured

#### Task: content_newsletter_setup
- **title**: Set up email newsletter
- **description**: Configure newsletter platform (Brevo/Sendinblue or Mailchimp). Create newsletter signup forms on blog and site. Set up welcome email, weekly digest template, and archive page
- **inputs**: Email platform account, brand guidelines
- **outputs**: Functional newsletter with signup forms
- **dependencies**: brand_email_template_design, site_blog_setup
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Newsletter signup functional, welcome email triggers

#### Task: content_newsletter_content_plan
- **title**: Plan 12-week newsletter content
- **description**: Plan newsletter content for 12 weeks: mix of new blog posts, curated content, exclusive tips, product updates, and community highlights. Create subject line variations
- **inputs**: Blog content calendar, product roadmap
- **outputs**: 12-week newsletter editorial plan
- **dependencies**: content_blog_content_calendar, content_newsletter_setup
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Newsletter plan complete with all 12 weeks

### Category: Referral Program Design

#### Task: referral_program_strategy
- **title**: Define referral program strategy and mechanics
- **description**: Design referral program structure: reward types (discount, free months, cash), threshold requirements, referral limits, program terms. Model customer lifetime value to set economics
- **inputs**: Customer LTV data, competitor referral programs
- **outputs**: Referral program design document
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Program economics validated, terms documented

#### Task: referral_program_landing_page
- **title**: Build referral program landing page
- **description**: Create dedicated page explaining the referral program: how it works, rewards, FAQ, and unique referral link dashboard. Include share buttons and social proof of past rewards
- **inputs**: Referral program design, brand guidelines
- **outputs**: Referral landing page live
- **dependencies**: referral_program_strategy, site_main_landing_page_build
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Page live with working referral links

#### Task: referral_program_technical_setup
- **title**: Implement referral tracking system
- **description**: Build or configure referral tracking in-app: unique referral codes per user, attribution tracking, reward calculation, and notification system. Integrate with billing for automatic discounts
- **inputs**: Technical requirements, billing system access
- **outputs**: Functional referral tracking
- **dependencies**: referral_program_strategy
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: marketing
- **validation**: Referrals tracked accurately, rewards calculated correctly

#### Task: referral_program_email_announcement
- **title**: Create referral program launch email
- **description**: Write and send announcement email to existing customers introducing the referral program. Include clear CTA, sharing buttons, and deadline for double-reward promotion
- **inputs**: Customer email list, referral program details
- **outputs**: Launch email sent, open and click rates tracked
- **dependencies**: referral_program_landing_page, email_welcome_sequence
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: content
- **validation**: Email sent, 25%+ open rate, referrals begin

#### Task: referral_social_media_campaign
- **title**: Launch referral social media campaign
- **description**: Create social media posts announcing referral program with shareable graphics, countdown for double-reward period, and testimonial from early referrer
- **inputs**: Social media templates, referral program details
- **outputs**: Posts published across all channels
- **dependencies**: referral_program_landing_page, brand_social_media_templates
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: content
- **validation**: Posts published with referral links

#### Task: referral_inapp_promotion
- **title**: Add in-app referral promotion
- **description**: Add referral CTA banners in the application: dashboard sidebar, post-login screen, settings menu. Target moments when user engagement is highest
- **inputs**: App UI screenshots, referral program details
- **outputs**: In-app referral prompts active
- **dependencies**: referral_program_technical_setup
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Prompts display to users, referral signups increase

### Category: Email Marketing

#### Task: email_welcome_sequence
- **title**: Create welcome email sequence for new signups
- **description**: Design 5-email welcome sequence: onboarding intro, feature highlights, success tips, case study spotlight, and trial conversion CTA. Space emails 2-3 days apart
- **inputs**: Brand guidelines, product tour content
- **outputs**: 5 automated welcome emails
- **dependencies**: brand_email_template_design, site_main_landing_page_build
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Sequence triggers on signup, all emails delivered

#### Task: email_onboarding_sequence
- **title**: Create onboarding drip campaign for trial users
- **description**: Design 8-email onboarding sequence guiding users through product setup: account configuration, import contacts, create first invoice, send first quote, schedule demo call. Trigger based on trial day
- **inputs**: Product walkthrough, onboarding milestones
- **outputs**: Automated onboarding sequence
- **dependencies**: email_welcome_sequence
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Trial users receive relevant emails based on day

#### Task: email_newsletter_template
- **title**: Create monthly newsletter template
- **description**: Design HTML newsletter template for monthly updates: company news, latest blog posts, tips of the month, upcoming features, community spotlight. Mobile-responsive
- **inputs**: Brand guidelines, newsletter content plan
- **outputs**: Newsletter template ready for use
- **dependencies**: brand_email_template_design
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Newsletter renders correctly on mobile and desktop

#### Task: email_newsletter_month_1
- **title**: Create and send Month 1 newsletter
- **description**: Write and design first newsletter edition. Include company update, top blog posts, tip of the month, upcoming events. Test across email clients
- **inputs**: Content plan, newsletter template
- **outputs**: Newsletter sent, analytics tracked
- **dependencies**: email_newsletter_template
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Newsletter delivered, 25%+ open rate

#### Task: email_reengagement_campaign
- **title**: Create re-engagement campaign for inactive users
- **description**: Design 3-email re-engagement sequence for users inactive 30+ days: "we miss you" message, new feature highlight, special offer to return. Include preference center link
- **inputs**: Inactive user list, product updates
- **outputs**: Automated re-engagement sequence
- **dependencies**: email_welcome_sequence
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Re-engagement emails sent, some users return

#### Task: email_customer_retention_sequence
- **title**: Create retention sequence for at-risk customers
- **description**: Design 4-email sequence for customers showing churn signals: usage drop, support tickets, non-renewal intent. Offer help, success stories, and retention discount
- **inputs**: Churn predictors, customer data
- **outputs**: Retention sequence with conditional triggers
- **dependencies**: email_onboarding_sequence
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: At-risk customers receive targeted retention emails

#### Task: email_pricing_upgrade_promotion
- **title**: Create upgrade promotion email sequence
- **description**: Design 3-email sequence promoting plan upgrades: feature comparison, case study of upgrade success, limited-time upgrade discount. Target users on lower tiers
- **inputs**: Tier feature matrix, upgrade incentives
- **outputs**: Upgrade promotion sequence
- **dependencies**: email_onboarding_sequence
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: content
- **validation**: Upgrade emails trigger, some upgrades occur

#### Task: email_invoice_reminder_templates
- **title**: Create invoice reminder email templates
- **description**: Design professional invoice reminder email sequence: payment due reminder (7 days before), payment due notice (day of), overdue notice (7 days after), final notice (14 days after)
- **inputs**: Brand guidelines, invoice workflow
- **outputs**: Invoice reminder email templates
- **dependencies**: brand_email_template_design
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: content
- **validation**: Reminders send automatically, payment rates improve

#### Task: email_list_hygiene_setup
- **title**: Set up email list hygiene processes
- **description**: Configure bounce handling, unsubscribe processing, spam complaint handling. Set up double opt-in for new subscribers. Configure list segmentation by engagement
- **inputs**: Email platform settings
- **outputs**: Clean email list with proper hygiene
- **dependencies**: email_newsletter_setup
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Bounces handled, list clean, deliverability high

#### Task: email_analytics_dashboard
- **title**: Create email analytics dashboard
- **description**: Set up email dashboard tracking: open rates, click rates, conversions, unsubscribes, bounces by campaign and segment. Create weekly email metrics report
- **inputs**: Email platform, analytics requirements
- **outputs**: Email dashboard with automated reports
- **dependencies**: email_welcome_sequence
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Dashboard live, reports sending weekly

### Category: Paid Acquisition

#### Task: paid_google_ads_account_setup
- **title**: Set up Google Ads account and campaigns
- **description**: Create Google Ads account, configure billing, install conversion tracking, set up shared budgets. Structure account for search and display campaigns
- **inputs**: Google Ads account, conversion tracking code
- **outputs**: Configured Google Ads account ready for campaigns
- **dependencies**: site_analytics_setup
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Account configured, conversion tracking verified

#### Task: paid_google_search_campaigns
- **title**: Launch Google Search campaigns
- **description**: Create search campaigns targeting French artisan keywords: CRM artisan, logiciel artisan, gestion clients plombier, etc. Write compelling ad copy with extensions. Set up ad groups by keyword theme
- **inputs**: Keyword list, competitor ad copy
- **outputs**: Search campaigns running
- **dependencies**: paid_google_ads_account_setup, seo_keyword_research_french
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: marketing
- **validation**: Campaigns running, clicks converting, CPA under target

#### Task: paid_google_display_campaigns
- **title**: Launch Google Display remarketing campaigns
- **description**: Create display remarketing campaigns targeting site visitors who didn't convert. Design banner ads in multiple sizes. Set up frequency capping and audience segmentation
- **inputs**: Banner designs, remarketing audience lists
- **outputs**: Display campaigns running
- **dependencies**: paid_google_ads_account_setup, site_analytics_setup
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Remarketing active, brand awareness increasing

#### Task: paid_meta_facebook_campaigns
- **title**: Launch Facebook/Instagram ad campaigns
- **description**: Create Facebook and Instagram campaigns: awareness ads with product benefits, retargeting ads for site visitors, lookalike audiences based on customers. Design ad creatives for each objective
- **inputs**: Ad creative designs, audience targeting criteria
- **outputs**: Meta campaigns running
- **dependencies**: brand_social_media_templates
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: marketing
- **validation**: Meta ads running, engagement metrics positive

#### Task: paid_linkedin_campaigns
- **title**: Launch LinkedIn campaigns for B2B targeting
- **description**: Create LinkedIn campaigns targeting small business owners in construction/trades. Use sponsored content and InMail. Target by job title, industry, company size
- **inputs**: LinkedIn ad account, audience criteria
- **outputs**: LinkedIn campaigns running
- **dependencies**: paid_google_ads_account_setup
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: LinkedIn ads running, B2B leads generated

#### Task: paid_retargeting_strategy
- **title**: Develop cross-platform retargeting strategy
- **description**: Map out retargeting funnel: site visitors -> email engaged -> trial started -> not converted. Define ad creative for each stage, frequency caps, and platform allocation
- **inputs**: Customer journey map, ad creative library
- **outputs**: Retargeting strategy document
- **dependencies**: paid_google_display_campaigns, paid_meta_facebook_campaigns
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Retargeting covering all funnel stages

#### Task: paid_ad_creative_variations
- **title**: Create multiple ad creative variations
- **description**: Design 20+ ad creative variations: different headlines, images, colors, CTAs. Test against each other to find winning combinations. Include video ads
- **inputs**: Brand guidelines, ad platform specs
- **outputs**: Ad creative library with 20+ variations
- **dependencies**: brand_social_media_templates
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Creative library complete, A/B testing configured

#### Task: paid_landing_page_optimization
- **title**: Optimize paid traffic landing pages
- **description**: Create dedicated landing pages for paid campaigns matching ad messaging. A/B test headlines, CTAs, and form lengths. Ensure fast load times for paid visitors
- **inputs**: Campaign keyword themes, analytics data
- **outputs**: High-converting landing pages
- **dependencies**: paid_google_search_campaigns, site_main_landing_page_build
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Landing page conversions 5%+ from paid traffic

#### Task: paid_budget_allocation
- **title**: Define paid media budget allocation
- **description**: Allocate monthly budget across platforms: Google Search (40%), Google Display (20%), Meta (30%), LinkedIn (10%). Define CPA targets per channel. Set up budget pacing
- **inputs**: Total marketing budget, channel performance data
- **outputs**: Budget allocation document
- **dependencies**: paid_google_search_campaigns, paid_meta_facebook_campaigns
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Budget allocated, spend on track, CPA targets set

#### Task: paid_conversion_tracking_verification
- **title**: Verify all conversion tracking
- **description**: Test all conversion actions across all paid platforms: form submits, trial starts, sign-ups. Ensure attribution is correct and cross-platform
- **inputs**: Google Ads, Meta Pixel, analytics
- **outputs**: All conversions tracked accurately
- **dependencies**: paid_google_ads_account_setup, site_analytics_setup
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: All conversions firing, attribution working

#### Task: paid_weekly_optimization_routine
- **title**: Establish weekly paid ads optimization routine
- **description**: Create SOP for weekly optimization: review CTR and CPC by ad, pause underperformers, adjust bids, check conversion rates, update negative keywords, review search terms
- **inputs**: Performance data templates
- **outputs**: Weekly optimization SOP document
- **dependencies**: paid_google_search_campaigns
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Weekly reviews happening, optimizations reducing CPA

#### Task: paid_monthly_reporting
- **title**: Create monthly paid media report
- **description**: Build monthly report template: spend by channel, impressions, clicks, CTR, CPC, conversions, CPA, ROAS. Include trend analysis and recommendations
- **inputs**: Ad platform data, analytics data
- **outputs**: Monthly report template and first report
- **dependencies**: paid_budget_allocation, paid_weekly_optimization_routine
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Report created, shared with stakeholders

### Category: Partnership Strategy

#### Task: partnership_supplier_research
- **title**: Research potential artisan tool and material suppliers
- **description**: Identify French suppliers of tools, materials, and equipment popular with plumbers, electricians, and carpenters. List potential co-marketing partners
- **inputs**: Industry directories, trade associations
- **outputs**: List of 30+ supplier prospects
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: List of 30+ qualified prospects with contact info

#### Task: partnership_supplier_outreach
- **title**: Execute outreach to supplier prospects
- **description**: Send partnership outreach emails to 30+ suppliers. Propose co-marketing: joint webinars, content collaborations, discount codes for shared customers
- **inputs**: Supplier list, outreach email templates
- **outputs**: Outreach sent, responses tracked
- **dependencies**: partnership_supplier_research
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: 30+ outreach emails sent, 10+ responses received

#### Task: partnership_association_research
- **title**: Research artisan trade associations
- **description**: Identify French artisan trade associations: Confederation of Artisans (CPA), regional artisan chambers, specific trades associations. List potential partnership opportunities
- **inputs**: Trade association directories
- **outputs**: List of 15+ association prospects
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: List of 15+ qualified association prospects

#### Task: partnership_association_outreach
- **title**: Execute outreach to trade associations
- **description**: Send partnership proposals to artisan associations. Propose member discounts, sponsored content, speaking opportunities at events, or membership benefits
- **inputs**: Association list, partnership proposals
- **outputs**: Partnership discussions initiated
- **dependencies**: partnership_association_research
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: 5+ partnership discussions active

#### Task: partnership_co_host_webinar
- **title**: Co-host webinar with partner
- **description**: Plan and execute joint webinar with partner (supplier or association). Topic relevant to both audiences. Promote to both customer bases. Include product demo
- **inputs**: Partner agreement, webinar platform
- **outputs**: Webinar executed with 50+ attendees
- **dependencies**: partnership_supplier_outreach, partnership_association_outreach
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: marketing
- **validation**: Webinar completed, leads generated

#### Task: partnership_discount_codes
- **title**: Create partner discount code program
- **description**: Design and implement discount code system for partners. Create unique codes per partner, track usage, set commission or revenue share structure
- **inputs**: Partner list, discount structure
- **outputs**: Partner discount program operational
- **dependencies**: partnership_supplier_outreach
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Partners using codes, sales tracked

#### Task: partnership_affiliate_tracking
- **title**: Set up affiliate tracking for partners
- **description**: Configure affiliate tracking system for partner referrals. Set up commission structure, payout thresholds, and reporting dashboard for partners
- **inputs**: Affiliate platform, partner terms
- **outputs**: Affiliate program live with 5+ partners
- **dependencies**: partnership_discount_codes
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Partners referring customers, commissions tracked

### Category: Trade Show & Event Strategy

#### Task: events_trade_show_calendar
- **title**: Research French trade shows for artisans
- **description**: Identify relevant trade shows: BATIMAT (Paris), EQUIPBAIE, artisaNantes, regional artisan fairs. Research dates, costs, attendee demographics, and past attendance
- **inputs**: Trade show directories, industry calendars
- **outputs**: Calendar of 10+ relevant events
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Calendar complete with all relevant events

#### Task: events_batimat_2026_planning
- **title**: Plan BATIMAT 2026 attendance
- **description**: Plan participation at BATIMAT (Paris, November 2026). Book booth, design booth space, plan staff schedule, prepare marketing materials, set show goals
- **inputs**: BATIMAT details, budget, goals
- **outputs**: BATIMAT participation plan
- **dependencies**: events_trade_show_calendar
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: marketing
- **validation**: Booth booked, materials in production

#### Task: events_booth_design
- **title**: Design trade show booth and materials
- **description**: Design booth graphics, banner stands, product demo station, branded giveaways, and lead capture forms. Create memorable booth experience
- **inputs**: Brand guidelines, booth specifications
- **outputs**: Booth design files ready for production
- **dependencies**: events_batimat_2026_planning, brand_design_assets
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: marketing
- **validation**: Booth materials produced, booth setup ready

#### Task: events_local_caen_fairs
- **title**: Attend local Caen/Normandie fairs
- **description**: Identify and attend 3 local fairs or artisan events in Caen/Normandie region. Set up booth, distribute materials, collect leads, build local awareness
- **inputs**: Local event list, event requirements
- **outputs**: 3 local events attended, 100+ leads collected
- **dependencies**: events_trade_show_calendar
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Events attended, leads followed up

#### Task: events_product_demos
- **title**: Prepare product demo for trade shows
- **description**: Create polished product demo specifically for trade show settings. Highlight key features, keep demo under 5 minutes, have backup internet connection plan
- **inputs**: Demo script, trade show laptop
- **outputs**: Demo ready, rehearsed
- **dependencies**: events_batimat_2026_planning
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Demo polished, staff can deliver consistently

#### Task: events_lead_capture_system
- **title**: Set up trade show lead capture system
- **description**: Configure mobile lead capture (tablet form or business card scanner). Create follow-up workflow for leads. Set up instant email to leads after show
- **inputs**: Lead capture tools, email templates
- **outputs**: Lead capture system operational
- **dependencies**: events_batimat_2026_planning
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Leads captured digitally, follow-up workflow active

#### Task: events_staff_training
- **title**: Train staff for trade show presence
- **description**: Train team on booth etiquette, product pitch, competitor handling, lead qualification, and demo delivery. Create FAQ card for common questions
- **inputs**: Product knowledge, booth staff
- **outputs**: Staff trained, FAQ cards created
- **dependencies**: events_product_demos
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Staff confident, delivering consistent message

#### Task: events_followup_campaign
- **title**: Execute post-show follow-up campaign
- **description**: Send personalized follow-up emails to all trade show leads within 48 hours. Segment by interest level, trigger appropriate nurture sequences
- **inputs**: Lead list from events, email templates
- **outputs**: All leads contacted within 48 hours
- **dependencies**: events_lead_capture_system
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: 100% leads emailed, some converting

#### Task: events_virtual_webinar_series
- **title**: Host virtual webinar series for remote reach
- **description**: Plan and execute 6-part webinar series on topics relevant to artisans: invoicing, client management, productivity, business growth. Promote via email and social
- **inputs**: Webinar topics, registration landing pages
- **outputs**: 6 webinars completed with 30+ attendees each
- **dependencies**: content_blog_content_calendar
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: marketing
- **validation**: Webinars scheduled, registrations meeting targets

### Category: PR & Press

#### Task: pr_press_kit_creation
- **title**: Create digital press kit
- **description**: Create comprehensive press kit PDF: company overview, founder bios, product screenshots, logo, key statistics, customer testimonials, contact info
- **inputs**: Company information, design assets
- **outputs**: Press kit PDF and online page
- **dependencies**: brand_logo_design_primary, site_about_page_build
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Press kit complete and accessible online

#### Task: pr_french_business_press_list
- **title**: Build list of French business press contacts
- **description**: Identify French business journalists and publications: Les Echos, Le Figaro Entreprise, Capital, FrenchWeb, Maddyness. Find appropriate reporters for tech/startup stories
- **inputs**: Press databases, Twitter lists
- **outputs**: List of 50+ journalist contacts with beats
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Journalist list complete with 50+ contacts

#### Task: pr_trade_publication_list
- **title**: Build list of artisan trade publications
- **description**: Identify French trade publications for construction and crafts: Le Moniteur, QualiBTP, Practitioners journals, regional artisan newsletters. Research editorial contacts
- **inputs**: Trade publication directories
- **outputs**: List of 20+ trade publication contacts
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Trade press list complete with 20+ contacts

#### Task: pr_pitch_story_angles
- **title**: Develop compelling story angles for press
- **description**: Identify 5 unique story angles: founder story (artisan-turned-tech), market gap story, customer success stories, industry innovation story, local tech hub story
- **inputs**: Company backstory, customer stories
- **outputs**: Press story angles document
- **dependencies**: pr_press_kit_creation
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: 5 story angles ready for pitch

#### Task: pr_personalized_outreach
- **title**: Execute personalized press outreach
- **description**: Send personalized pitches to 30+ journalists. Reference their recent articles, tailor angle to their beat. Follow up once if no response
- **inputs**: Journalist list, pitch templates
- **outputs**: Press mentions or interviews booked
- **dependencies**: pr_french_business_press_list, pr_pitch_story_angles
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: 30+ pitches sent, 5+ responses

#### Task: pr_press_release_product_launch
- **title**: Write and distribute press release for product launch
- **description**: Write press release announcing Mini-CRM launch. Target tech and business press. Distribute via PR wire (BNP Networks, Business Wire France). Include quotes, key features, availability
- **inputs**: Product launch details, press kit
- **outputs**: Press release distributed, press coverage tracked
- **dependencies**: pr_press_kit_creation
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Press release distributed, coverage achieved

#### Task: pr_press_release_major_update
- **title**: Write press release for major product update
- **description**: Write press release announcing significant product update. Highlight new features and customer benefits. Target trade publications
- **inputs**: Product update details, customer quotes
- **outputs**: Press release distributed
- **dependencies**: pr_press_kit_creation
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Press release sent, coverage generated

#### Task: pr_thought_leadership_articles
- **title**: Place thought leadership articles
- **description**: Write and pitch 3 thought leadership articles on artisan business trends, CRM adoption, or digital transformation in trades. Target op-ed sections of business publications
- **inputs**: Article outlines, publication guidelines
- **outputs**: 3 articles published
- **dependencies**: pr_french_business_press_list
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Articles published with byline

#### Task: pr_customer_story_press
- **title**: Pitch customer stories to press
- **description**: Work with willing customers to pitch their success story to press. Write press release featuring customer quote and results achieved with Mini-CRM
- **inputs**: Customer stories, customer permission
- **outputs**: Customer stories covered in press
- **dependencies**: social_proof_testimonial_collection_initial
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Customer stories published externally

#### Task: pr_crisis_communications_plan
- **title**: Develop crisis communications plan
- **description**: Create crisis communications plan: potential scenarios, response protocols, spokesperson designated, pre-written holding statements, escalation procedures
- **inputs**: Risk assessment, legal input
- **outputs**: Crisis communications plan
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Plan documented, team trained

#### Task: pr_press_monitoring_setup
- **title**: Set up press and media monitoring
- **description**: Set up Google Alerts for brand name, competitors, and industry terms. Monitor French tech press and trade publications. Track all mentions
- **inputs**: Brand name, keywords
- **outputs**: Monitoring alerts active
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: All brand mentions captured

#### Task: pr_reporter_relationship_building
- **title**: Build ongoing reporter relationships
- **description**: Engage with journalists on social media, share their relevant articles, offer exclusives on breaking news. Build genuine relationships for future coverage
- **inputs**: Journalist contacts from list
- **outputs**: Relationships with 10+ reporters
- **dependencies**: pr_french_business_press_list
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Ongoing rapport with key journalists

### Category: Social Proof

#### Task: social_proof_strategy
- **title**: Define social proof strategy
- **description**: Map out social proof types needed: testimonials (audio, video, written), case studies, reviews on external platforms, trust badges, usage statistics. Define collection and deployment plan
- **inputs**: Buyer journey stages, social proof types
- **outputs**: Social proof strategy document
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Strategy complete with all social proof types planned

#### Task: social_proof_testimonial_collection_initial
- **title**: Collect initial testimonials from early customers
- **description**: Reach out to first 20 customers for testimonials. Offer incentives (free month, discount). Collect video (Zoom), audio, and written formats. Get permission for various uses
- **inputs**: Customer list, testimonial request template
- **outputs**: 20 testimonials collected with permissions
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agentCRM users. Target: 10 video, 10 written testimonials
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: 20 testimonials collected with permissions

#### Task: social_proof_review_site_setup
- **title**: Set up profile on French review platforms
- **description**: Create profiles on French review sites: Trustpilot France, Google Reviews, Facebook Reviews. Encourage satisfied customers to leave reviews. Respond to all reviews
- **inputs**: Business profiles, review platform requirements
- **outputs**: Active review profiles with 20+ reviews
- **dependencies**: social_proof_testimonial_collection_initial
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: 4.5+ star rating across platforms

#### Task: social_proof_trust_badges
- **title**: Design and display trust badges
- **description**: Create trust badges: "French Company", "Secure Data Hosting", "Satisfied Artisans", "GDPR Compliant". Display on landing page, pricing page, checkout
- **inputs**: Trust claims, brand guidelines
- **outputs**: Trust badges designed and implemented
- **dependencies**: brand_logo_design_primary
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Trust badges visible on site

#### Task: social_proof_user_count_claims
- **title**: Display user count and usage statistics
- **description**: Create badge showing: number of artisans using Mini-CRM, number of invoices created, number of clients managed. Update periodically. Display prominently
- **inputs**: Product usage data, badge design
- **outputs**: Usage statistics badge on site
- **dependencies**: site_main_landing_page_build
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Statistics displayed accurately

#### Task: social_proof_logo_wall
- **title**: Create customer logo wall
- **description**: With permission, display logos of artisan businesses using Mini-CRM. Create recognizable customer logo wall for homepage. Target 10 logos
- **inputs**: Customer logos, permission forms
- **outputs**: Logo wall implemented
- **dependencies**: social_proof_testimonial_collection_initial
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: 10+ customer logos displayed

#### Task: social_proof_media_mentions
- **title**: Display media mention badges
- **description**: Create badge showing "As Seen In" with logos of publications that have covered Mini-CRM. Display on homepage and press page
- **inputs**: Media coverage, publication logos
- **outputs**: Media badges displayed
- **dependencies**: pr_personalized_outreach
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Media badges displayed if coverage received

### Category: Customer Testimonials & Case Studies

#### Task: case_study_template_design
- **title**: Design case study template
- **description**: Create professional case study template: challenge, solution, implementation, results structure. Include space for metrics, quotes, screenshots. Brand consistently
- **inputs**: Case study outline, brand guidelines
- **outputs**: Case study template in multiple formats
- **dependencies**: brand_design_assets
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Template ready for use by content team

#### Task: case_study_plumber_caen
- **title**: Create case study: Plomberie Dupont, Caen
- **description**: Write detailed case study featuring a plumber in Caen. Document challenges (manual invoicing, lost client info), implementation of Mini-CRM, results (time saved, invoices increased). Include metrics and quotes
- **inputs**: Customer interview, usage data, photos
- **outputs**: Published case study with permission
- **dependencies**: case_study_template_design, social_proof_testimonial_collection_initial
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Case study published, customer approved

#### Task: case_study_electrician_rouen
- **title**: Create case study: Electricien Martin, Rouen
- **description**: Write detailed case study featuring an electrician in Rouen. Focus on scheduling challenges solved, client communication improvements, quote-to-job conversion increase
- **inputs**: Customer interview, usage data
- **outputs**: Published case study with permission
- **dependencies**: case_study_template_design, social_proof_testimonial_collection_initial
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Case study published

#### Task: case_study_carpenter_honfleur
- **title**: Create case study: Menuiserie Leroy, Honfleur
- **description**: Write detailed case study featuring a carpenter in Honfleur. Document project management challenges, customer relationship improvements, and business growth metrics
- **inputs**: Customer interview, project photos
- **outputs**: Published case study with permission
- **dependencies**: case_study_template_design, social_proof_testimonial_collection_initial
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Case study published

#### Task: case_study_time_savings_metric
- **title**: Create aggregated time savings case study
- **description**: Analyze usage data across customers to document average time savings: hours per week saved, invoices processed faster, etc. Create aggregate case study with anonymized data
- **inputs**: Product usage analytics
- **outputs**: Time savings infographic and case study
- **dependencies**: case_study_template_design
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Time savings data verified, published

#### Task: case_study_small_team_invoicing
- **title**: Create case study: Small team handling 50+ clients
- **description**: Write case study featuring a small team (2-3 people) successfully using Mini-CRM to manage 50+ clients. Document team collaboration features, shared inbox, role-based access
- **inputs**: Customer interview, team usage data
- **outputs**: Published case study
- **dependencies**: case_study_template_design
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Case study published with team metrics

#### Task: case_study_video_testimonial_setup
- **title**: Set up video testimonial production
- **description**: Set up process for recording video testimonials: Zoom recording setup, lighting guidelines, consent forms, editing workflow. Create reusable setup kit
- **inputs**: Video recording tools, consent template
- **outputs**: Video testimonial workflow ready
- **dependencies**: social_proof_testimonial_collection_initial
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Video testimonials being produced

#### Task: case_study_promotion
- **title**: Promote case studies across channels
- **description**: Promote each case study via: email to customers, social media posts, LinkedIn article, blog mention, paid ads targeting similar profiles. Track traffic and conversions
- **inputs**: Case study content, promotion channels
- **outputs**: Case studies reaching target audience
- **dependencies**: case_study_plumber_caen, case_study_electrician_rouen
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Traffic to case studies, leads generated

### Category: Competitive Battle Cards

#### Task: battle_card_competitor_research
- **title**: Research top 5 CRM competitors
- **description**: Deep dive into 5 competitors: HubSpot, Salesforce, Pipedrive, Zoho CRM, and a French-specific competitor. Document pricing, features, positioning, strengths, weaknesses
- **inputs**: Competitor websites, G2 reviews, user interviews
- **outputs**: Competitor profiles with detailed analysis
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: marketing
- **validation**: 5 competitor profiles complete

#### Task: battle_card_hubspot_analysis
- **title**: Create HubSpot battle card
- **description**: Create detailed battle card comparing Mini-CRM to HubSpot. Focus on: pricing (HubSpot expensive for artisans), complexity (Mini-CRM simpler), French market support, local hosting option
- **inputs**: HubSpot pricing, features, customer complaints
- **outputs**: HubSpot battle card
- **dependencies**: battle_card_competitor_research
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Battle card ready for sales team

#### Task: battle_card_salesforce_analysis
- **title**: Create Salesforce battle card
- **description**: Create detailed battle card comparing Mini-CRM to Salesforce. Focus on: pricing (Salesforce too expensive), complexity (Mini-CRM designed for non-tech users), implementation time
- **inputs**: Salesforce pricing, features, complexity complaints
- **outputs**: Salesforce battle card
- **dependencies**: battle_card_competitor_research
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Battle card ready for sales team

#### Task: battle_card_pipedrive_analysis
- **title**: Create Pipedrive battle card
- **description**: Create detailed battle card comparing Mini-CRM to Pipedrive. Focus on: invoicing features (Mini-CRM has built-in), French market support, pricing transparency, local data hosting
- **inputs**: Pipedrive features, pricing, reviews
- **outputs**: Pipedrive battle card
- **dependencies**: battle_card_competitor_research
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Battle card ready for sales team

#### Task: battle_card_zoho_analysis
- **title**: Create Zoho CRM battle card
- **description**: Create detailed battle card comparing Mini-CRM to Zoho CRM. Focus on: user interface (Mini-CRM cleaner), French language support, local support, industry-specific features for artisans
- **inputs**: Zoho CRM features, pricing, reviews
- **outputs**: Zoho battle card
- **dependencies**: battle_card_competitor_research
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Battle card ready for sales team

#### Task: battle_card_french_competitor_analysis
- **title**: Create French CRM competitor battle card
- **description**: Create detailed battle card comparing Mini-CRM to French-specific CRM solution (e.g., Holded, Indy). Focus on: self-hosted option, artisan-specific features, local support, pricing
- **inputs**: French competitor analysis
- **outputs**: French competitor battle card
- **dependencies**: battle_card_competitor_research
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Battle card ready for sales team

#### Task: battle_card_win_themes
- **title**: Document competitive win themes
- **description**: Synthesize battle card analysis into common win themes: "Mini-CRM wins on pricing under 100EUR/month", "Mini-CRM wins on simplicity", "Mini-CRM wins on French support". Create talking points
- **inputs**: All battle cards
- **outputs**: Win themes document for sales
- **dependencies**: battle_card_hubspot_analysis, battle_card_salesforce_analysis
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Sales team using win themes

#### Task: battle_card_objection_handling
- **title**: Create objection handling guide
- **description**: Create objection handling matrix: common objections ("too expensive", "already have Excel", "not needed") with responses, proof points, and resources. Train sales team
- **inputs**: Sales call recordings, common questions
- **outputs**: Objection handling guide
- **dependencies**: battle_card_win_themes
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Sales team trained on objections

### Category: Sales Collateral

#### Task: collateral_pitch_deck_design
- **title**: Design investor/partnership pitch deck
- **description**: Create pitch deck for investors and potential partners: problem, solution, product, market size, business model, team, traction, ask. 12-15 slides max
- **inputs**: Company metrics, investor requirements
- **outputs**: Pitch deck in PDF and PPTX
- **dependencies**: brand_design_assets, brand_messaging_framework
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: content
- **validation**: Pitch deck ready for presentations

#### Task: collateral_one_pager_product
- **title**: Create product one-pager
- **description**: Create single-page product overview: key features, benefits, pricing tiers, target customer, and CTA. For sales use at trade shows and meetings. Print-ready PDF
- **inputs**: Product features, pricing, brand guidelines
- **outputs**: Product one-pager PDF
- **dependencies**: brand_design_assets
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: content
- **validation**: One-pager used by sales team

#### Task: collateral_one_pager_pricing
- **title**: Create pricing one-pager
- **description**: Create single-page pricing summary: tier comparison, FAQ, testimonials, and CTA. Highlight annual discount. For sales and pre-sales
- **inputs**: Pricing tiers, feature matrix
- **outputs**: Pricing one-pager PDF
- **dependencies**: collateral_one_pager_product
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: content
- **validation**: Pricing one-pager ready

#### Task: collateral_product_demo_video
- **title**: Create 3-minute product demo video
- **description**: Record professional product demo video: walk through key features, show real use case, include customer testimonial snippet. Host on YouTube/Vimeo
- **inputs**: Demo script, screen recording setup
- **outputs**: Demo video published
- **dependencies**: site_features_page_build
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Video created, used in sales

#### Task: collateral_customer_successDeck
- **title**: Create customer success deck
- **description**: Create presentation of customer success stories: testimonials, metrics, before/after comparisons. For sales to show social proof
- **inputs**: Case studies, testimonials, metrics
- **outputs**: Success deck PDF
- **dependencies**: case_study_plumber_caen, case_study_electrician_rouen
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Success deck used in sales

#### Task: collateral_comparison_sheet
- **title**: Create feature comparison sheet
- **description**: Create detailed comparison table: Mini-CRM vs 3 competitors across 20+ features. Highlight where Mini-CRM wins. PDF format for sales use
- **inputs**: Battle cards, feature matrix
- **outputs**: Comparison sheet PDF
- **dependencies**: battle_card_competitor_research
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Comparison sheet used in sales

#### Task: collateralROI_calculator
- **title**: Build ROI calculator for prospects
- **description**: Create interactive ROI calculator: time saved on invoicing, reduction in lost clients, efficiency gains. Show payback period and annual savings. For sales conversations
- **inputs**: Customer usage data, industry benchmarks
- **outputs**: ROI calculator (web-based or PDF)
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Calculator used in sales calls

#### Task: collateral_sales_playbook
- **title**: Create sales playbook
- **description**: Create comprehensive sales playbook: prospecting scripts, discovery questions, demo guidelines, proposal process, objection handling, close techniques, post-sale handoff
- **inputs**: Sales process documentation
- **outputs**: Sales playbook document
- **dependencies**: collateral_pitch_deck_design, battle_card_objection_handling
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: marketing
- **validation**: Sales team using playbook

#### Task: collateral_email_templates_sales
- **title**: Create sales email templates
- **description**: Create library of sales email templates: cold outreach, follow-up, discovery, demo scheduling, proposal follow-up, close, referral request. Include subject line variations
- **inputs**: Sales process, email best practices
- **outputs**: Email template library
- **dependencies**: collateral_sales_playbook
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Sales team using templates

#### Task: collateral_proposal_template
- **title**: Create proposal template
- **description**: Create proposal template for custom deals: executive summary, solution description, pricing, timeline, terms, case study snippet, signature block
- **inputs**: Proposal structure, legal terms
- **outputs**: Proposal template
- **dependencies**: collateral_sales_playbook
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Proposal template in use

### Category: Analytics & Attribution

#### Task: analytics_dashboard_setup
- **title**: Set up marketing analytics dashboard
- **description**: Create comprehensive marketing dashboard using Google Data Studio or similar: traffic sources, conversions, revenue, CAC, LTV, funnel performance. Connect all data sources
- **inputs**: GA4, Google Ads, Meta Ads, billing data
- **outputs**: Live marketing dashboard
- **dependencies**: site_analytics_setup, paid_google_ads_account_setup
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: marketing
- **validation**: Dashboard live, updates daily

#### Task: analytics_conversion_tracking_full
- **title**: Implement full conversion tracking
- **description**: Track all micro and macro conversions: page views, CTA clicks, form submits, trial starts, onboarding steps, upgrades, churn. Map to customer journey stages
- **inputs**: Customer journey map, analytics setup
- **outputs**: All conversions tracked in GA4 and ad platforms
- **dependencies**: site_analytics_setup
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: All conversions firing correctly

#### Task: analytics_attribution_model
- **title**: Define attribution model
- **description**: Choose attribution model: first-touch, last-touch, linear, time-decay, or data-driven. Document which interactions contribute to conversions. Set up in analytics
- **inputs**: Customer journey data, conversion data
- **outputs**: Attribution model implemented
- **dependencies**: analytics_conversion_tracking_full
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Attribution data available for optimization

#### Task: analytics_cac_calculation
- **title**: Calculate and track customer acquisition cost
- **description**: Calculate CAC by channel: paid search, paid social, organic, referral, direct. Track monthly trends. Set up automated CAC report
- **inputs**: Marketing spend data, customer data
- **outputs**: CAC by channel updated monthly
- **dependencies**: analytics_dashboard_setup
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: CAC metrics tracked, report automated

#### Task: analytics_ltv_calculation
- **title**: Calculate customer lifetime value
- **description**: Calculate LTV by customer segment: solo artisan vs team, by trade type, by pricing tier. Include churn rate. Set up LTV report
- **inputs**: Customer billing data, usage data
- **outputs**: LTV by segment calculated
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: LTV metrics available for business decisions

#### Task: analytics_roi_reporting
- **title**: Create marketing ROI reporting
- **description**: Build monthly ROI report: revenue attributed to marketing, marketing spend, net ROI. Compare channels. Identify best and worst performing
- **inputs**: Revenue data, marketing spend
- **outputs**: Monthly ROI report
- **dependencies**: analytics_cac_calculation, analytics_ltv_calculation
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: ROI report shared monthly

#### Task: analytics_cohort_analysis
- **title**: Set up cohort analysis
- **description**: Create cohort analysis: customer retention by signup month, revenue by cohort, feature usage by cohort. Track cohort health over time
- **inputs**: Customer signup data, usage data
- **outputs**: Cohort dashboard
- **dependencies**: analytics_dashboard_setup
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Cohort data visible in dashboard

#### Task: analytics_content_performance
- **title**: Track content performance metrics
- **description**: Track blog and content performance: page views, time on page, shares, leads generated per piece. Identify top content. Create content ROI report
- **inputs**: GA4 data, content inventory
- **outputs**: Content performance dashboard
- **dependencies**: site_blog_setup, content_blog_content_calendar
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Content metrics tracked, top content identified

#### Task: analytics_weekly_review_process
- **title**: Establish weekly analytics review process
- **description**: Create SOP for weekly marketing review: metrics to check, questions to answer, actions to take. Automate data pulls where possible. Schedule recurring meeting
- **inputs**: Analytics dashboard
- **outputs**: Weekly review SOP
- **dependencies**: analytics_dashboard_setup
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Weekly reviews happening consistently

#### Task: analytics_ab_testing_framework
- **title**: Create A/B testing framework
- **description**: Define A/B testing process: hypothesis creation, test design, statistical significance requirements, implementation, analysis, documentation. Set up testing tool
- **inputs**: Testing tools, statistical methods
- **outputs**: A/B testing framework and first tests
- **dependencies**: site_analytics_setup
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Tests running with proper methodology

### Category: Brand Guidelines Document

#### Task: brand_guidelines_document
- **title**: Compile comprehensive brand guidelines document
- **description**: Compile all brand elements into single brand guidelines document: logo usage, color palette, typography, voice and tone, photography style, iconography, and examples of correct/incorrect usage
- **inputs**: All brand deliverables from previous tasks
- **outputs**: Complete brand guidelines PDF
- **dependencies**: brand_color_palette_definition, brand_typography_selection, brand_voice_guidelines, brand_logo_design_primary
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Brand guidelines complete and distributed

#### Task: brand_logo_usage_rules
- **title**: Document logo usage rules
- **description**: Create detailed logo usage guide: minimum sizes, clear space requirements, approved backgrounds, incorrect uses, file formats, and version variations (color, black, white)
- **inputs**: Logo files, brand principles
- **outputs**: Logo usage section of brand guidelines
- **dependencies**: brand_logo_design_primary
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Logo rules documented

#### Task: brand_color_application_guide
- **title**: Create color application guide
- **description**: Document proper color usage: primary color usage, secondary color usage, accent colors, neutral colors, background color rules, text color contrast requirements
- **inputs**: Color palette
- **outputs**: Color application section of brand guidelines
- **dependencies**: brand_color_palette_definition
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Color rules documented

#### Task: brand_typography_rules
- **title**: Document typography rules
- **description**: Create detailed typography guide: font families, font weights, type scales, line heights, letter spacing, paragraph rules, and do's and don'ts
- **inputs**: Selected fonts, brand principles
- **outputs**: Typography section of brand guidelines
- **dependencies**: brand_typography_selection
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: content
- **validation**: Typography rules documented

#### Task: brand_photography_guidelines
- **title**: Document photography guidelines
- **description**: Create photography guidelines: preferred subjects (real artisans in real work environments), style (natural light, candid, professional), composition rules, and approved image sources
- **inputs**: Photography style guide
- **outputs**: Photography section of brand guidelines
- **dependencies**: brand_photography_style_guide
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: content
- **validation**: Photography rules documented

#### Task: brand_digital_usage_examples
- **title**: Create digital usage examples
- **description**: Document correct brand usage in digital contexts: website, email, social media, ads. Include examples of correct and incorrect usage
- **inputs**: Brand guidelines
- **outputs**: Digital usage section with examples
- **dependencies**: brand_logo_usage_rules, brand_color_application_guide, brand_typography_rules
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Digital examples complete

#### Task: brand_print_usage_examples
- **title**: Create print usage examples
- **description**: Document correct brand usage in print contexts: business cards, brochures, trade show materials, merchandise. Include production specifications
- **inputs**: Brand guidelines
- **outputs**: Print usage section with specifications
- **dependencies**: brand_logo_usage_rules, brand_color_application_guide
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Print examples complete

#### Task: brand_do_dont_examples
- **title**: Create do's and don'ts visual guide
- **description**: Create visual guide showing correct and incorrect brand usage: logo placements, color combinations, typography mistakes, spacing errors. Make it memorable
- **inputs**: Brand elements
- **outputs**: Do's and don'ts visual guide
- **dependencies**: brand_logo_usage_rules, brand_color_application_guide, brand_typography_rules
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Do's and don'ts guide complete

#### Task: brand_asset_distribution
- **title**: Set up brand asset distribution system
- **description**: Create shared brand asset library (Google Drive or similar): logo files in all formats, color codes, font files, template files. Set up access controls and version control
- **inputs**: All brand assets
- **outputs**: Brand asset library operational
- **dependencies**: brand_logo_design_primary, brand_color_palette_definition, brand_typography_selection
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Team accessing and using correct assets

#### Task: brand_training_material
- **title**: Create brand training material
- **description**: Create training presentation for new team members: brand overview, key principles, how to use brand assets, where to find resources. Include quiz to verify understanding
- **inputs**: Brand guidelines
- **outputs**: Brand training presentation
- **dependencies**: brand_guidelines_document
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: New team members trained

#### Task: brand_compliance_review
- **title**: Conduct brand compliance review
- **description**: Review all existing marketing materials for brand compliance. Identify and fix any deviations. Create checklist for future material review
- **inputs**: All marketing materials
- **outputs**: Compliance report, remediation plan
- **dependencies**: brand_guidelines_document
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: All materials compliant

#### Task: brand_guidelines_distribution
- **title**: Distribute brand guidelines to all stakeholders
- **description**: Share brand guidelines with all team members, contractors, agencies, and partners who create on behalf of Mini-CRM. Track acknowledgment
- **inputs**: Brand guidelines PDF, stakeholder list
- **outputs**: All stakeholders received and acknowledged guidelines
- **dependencies**: brand_guidelines_document
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: All stakeholders have guidelines, usage consistent
