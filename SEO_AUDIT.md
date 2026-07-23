# SEO Audit

## Implemented Updates

- Set the production canonical domain to `https://evomortgagesolutions.co.za`.
- Updated the default site title, description, language, phone number, and email in `_config.yml`.
- Added page-specific meta descriptions for contact and calculator pages.
- Added canonical URLs, Open Graph metadata, Twitter card metadata, robots directives, and theme color in `_includes/head.html`.
- Added `FinancialService` JSON-LD structured data with address, email, phone, image, and social profile.
- Added `robots.txt` and `sitemap.xml`.
- Converted core content pages to pretty permalinks and updated internal links to match.
- Promoted the homepage hero text to a real `h1`.
- Fixed card heading markup so generated headings do not contain nested paragraphs.
- Improved external-link safety with `rel="noopener"` and checked image `alt` and iframe `title` coverage.

## Review Notes

High impact:

- Canonical/social URLs previously resolved to the wrong domain or localhost during inspection. They now resolve to the production domain after a clean build.
- The site title previously referenced Durban while the business address and content identify Pretoria. The default SEO title now aligns with Pretoria.
- The site email in config was malformed and is now `verna.vanheerden@evogroup.co.za`.
- Internal URLs now consistently use pretty permalink paths.

Medium impact:

- The sitemap is generated from Jekyll pages and excludes `robots.txt` and `sitemap.xml`.
- Social sharing images now use absolute URLs.
- Contact and calculator pages now have distinct descriptions instead of inheriting the homepage copy.

Remaining recommendations:

- Replace the placeholder Google Analytics ID `xxx` with the real measurement ID or disable analytics.
- Upgrade the Webpack 4 / Bootstrap 4 stack when practical to reduce Sass deprecation warnings and dependency vulnerabilities.
- Consider compressing or replacing large emitted SVG/font assets to reduce the `bundle.css` and asset payload.
