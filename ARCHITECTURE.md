# Frontend Architecture

This Jekyll site uses data-driven Liquid includes, Bootstrap 4, Webpack, and Sass. The current architecture preserves the existing visual design while making shared UI and design decisions easier to maintain.

## Assessment

High impact:

- Repeated service/calculator card markup existed in multiple includes. Use `_includes/icon-card-deck.html` for icon cards and `_includes/section-heading.html` for repeated section headings.
- Design values were scattered across partials. Use `_assets/abstracts/_tokens.scss` for colors, shadows, spacing, radii, type sizes, z-index values, transitions, breakpoints, and image paths.
- `node-sass` was deprecated and incompatible with modern Sass modules. The build now uses Dart Sass through the `sass` package.
- Inline template styles in the head/nav/footer reduced maintainability. Shared page spacing and footer background now live in Sass.
- Several semantics/accessibility issues were present: missing `lang`, missing main landmark, placeholder-only form fields, generic logo alt text, and malformed paragraph markup.

Medium impact:

- Navigation link logic was duplicated between home and inner-page navs. Shared link rendering now lives in `_includes/nav-links.html`.
- Bootstrap 4 emits Dart Sass deprecation warnings. A future Bootstrap upgrade should remove most vendor Sass warnings.
- The asset build still uses Webpack 4. It works on current Node through `node --openssl-legacy-provider`, but a Webpack 5/Vite migration would reduce maintenance risk.
- `_assets/**/dist` folders look like generated/dead CSS artifacts and are not imported by the source bundle. Confirm they are not used by deployment before removing.

Low impact:

- Some older or duplicate images appear unused, including old favicon/team image variants and Windows shortcut files in `assets`. Confirm with production references before deleting.
- Some page-specific iframe heights remain literal values because they are content-specific, but they could become data-driven if more calculator pages are added.

## Folder Roles

- `_assets/abstracts`: design tokens and Sass mixins/functions. No selectors should live here.
- `_assets/base`: global element styles, page defaults, and legacy compatibility shims.
- `_assets/components`: reusable UI primitives such as buttons, navigation, and client scrollers.
- `_assets/layout`: section-level styles for home/page sections.
- `_includes`: reusable Liquid components and section partials.
- `_layouts`: page shells and landmarks.
- `_data`: editable site content and navigation.

## Conventions

- Prefer data in `_data/sitetext.yml` or `_data/navigation.yml` over hardcoded section content.
- Prefer small includes for repeated Liquid patterns. Pass data through `include.*` parameters.
- Keep visual tokens in `_assets/abstracts/_tokens.scss`; avoid introducing new hex values, shadows, transitions, or breakpoints in component files.
- Use BEM-style class names for new custom components. Existing Bootstrap classes should remain where they provide layout or utility behavior.
- Use Sass `@use`/`@forward` for new local architecture. Bootstrap 4 still requires `@import` until the framework is upgraded.
- Avoid `!important` unless overriding Bootstrap states with no practical lower-specificity alternative.

## Verification

- `npm.cmd run bundle`
- `bundle exec jekyll build --trace`
