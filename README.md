# Zonemon Coming Soon Page

A clean, professional "Coming Soon" splash page for zonemon.com built to deploy on Cloudflare Pages.

## Overview

This is a single-page static site designed to be lightweight, fast, and professional. It features:

- Custom SVG shield logo with "ZM" branding
- Mantine v7-inspired design system (blues, clean typography)
- Responsive mobile-first design
- Subtle animations and interactions
- SEO-optimized meta tags for social sharing
- Accessibility features (WCAG compliance, keyboard navigation)
- Performance-optimized (no external dependencies)

## Project Structure

```
zm-splash/
├── .github/
│   └── workflows/
│       └── deploy.yml  # GitHub Actions deployment workflow
├── index.html          # Main HTML file
├── styles.css          # All styles (Mantine-inspired)
├── wrangler.toml       # Cloudflare Pages configuration
├── assets/
│   └── logo.svg        # Zonemon shield logo
└── README.md           # This file
```

## Design Features

### Color Palette (Mantine v7 Blues)
- Primary: `#228BE6` (blue.6)
- Light: `#339AF0` (blue.5)
- Dark: `#1971C2` (blue.7)
- Darker: `#1864AB` (blue.8)
- Grays: `#F8F9FA` to `#212529`

### Typography
- Font Family: System UI stack (San Francisco, Segoe UI, etc.)
- Responsive font sizes
- Clean, modern hierarchy

### Features
- Floating logo animation
- Parallax background effect on scroll
- Smooth entrance animations
- Hover effects on badges and CTA
- Blurred gradient background suggesting a dashboard

## Local Development

### Preview Locally

Simply open `index.html` in a web browser:

```bash
# Option 1: Direct file open
open index.html

# Option 2: Python HTTP server
python3 -m http.server 8000
# Then visit http://localhost:8000

# Option 3: Node.js HTTP server
npx serve .
# Then visit the provided URL
```

### Test with Wrangler (Cloudflare CLI)

```bash
# Install Wrangler if not already installed
npm install -g wrangler

# Login to Cloudflare
wrangler login

# Preview locally with Wrangler
wrangler pages dev .

# The page will be available at http://localhost:8788
```

## Deployment to Cloudflare Pages

### Method 1: Cloudflare Dashboard (Recommended)

1. Log in to [Cloudflare Dashboard](https://dash.cloudflare.com/)
2. Navigate to **Pages** in the left sidebar
3. Click **Create a project**
4. Choose **Direct Upload**
5. Upload the entire `zm-splash` directory
6. Set project name: `zonemon-splash`
7. Click **Save and Deploy**

### Method 2: Wrangler CLI

```bash
# From the zm-splash directory
wrangler pages deploy . --project-name=zonemon-splash

# Follow the prompts to complete deployment
```

### Method 3: GitHub Actions (Recommended - Automatic CI/CD)

This repo includes a GitHub Actions workflow for automatic deployment to Cloudflare Pages.

#### Initial Setup (One-time)

1. **Create the Cloudflare Pages project:**
   ```bash
   # Option A: Via Cloudflare Dashboard
   # Go to https://dash.cloudflare.com/ → Pages → Create project → Direct Upload
   # Upload the repo contents and name it "zonemon-splash"

   # Option B: Via Wrangler CLI (requires Node.js 20+)
   wrangler pages project create zonemon-splash
   ```

2. **Get your Cloudflare credentials:**
   - **Account ID**: Found in Cloudflare Dashboard → right sidebar → "Account ID"
   - **API Token**: Create at https://dash.cloudflare.com/profile/api-tokens
     - Use template "Edit Cloudflare Workers" OR create custom with:
       - Account → Cloudflare Pages → Edit
       - Account → Account Settings → Read
       - User → User Details → Read

3. **Add GitHub Secrets:**
   ```bash
   # Via GitHub CLI
   gh secret set CLOUDFLARE_API_TOKEN --repo infrabill/zm-splash
   gh secret set CLOUDFLARE_ACCOUNT_ID --repo infrabill/zm-splash

   # Or via GitHub web UI:
   # Settings → Secrets and variables → Actions → New repository secret
   ```

4. **Push to trigger deployment:**
   ```bash
   git push origin main
   ```

The workflow (`.github/workflows/deploy.yml`) will automatically deploy on every push to `main`.

### Method 4: Cloudflare Git Integration (Alternative)

1. In Cloudflare Pages, choose **Connect to Git**
2. Select the `infrabill/zm-splash` repository
3. Configure build settings:
   - **Build command**: Leave empty (static site)
   - **Build output directory**: `/`
   - **Root directory**: `/`
4. Click **Save and Deploy**

## Custom Domain Setup

After deployment, configure your custom domain:

1. In Cloudflare Pages project settings, go to **Custom domains**
2. Click **Set up a custom domain**
3. Enter `zonemon.com`
4. Add `www.zonemon.com` as well (optional)
5. Cloudflare will automatically configure DNS if the domain is managed by Cloudflare

Update `wrangler.toml` to include custom domain:

```toml
route = { pattern = "zonemon.com", custom_domain = true }
route = { pattern = "www.zonemon.com", custom_domain = true }
```

## Performance Optimizations

- No external dependencies (no CDN requests)
- Inline critical CSS (all styles in one file)
- SVG logo (scalable, small file size)
- Minimal JavaScript (only for animations)
- Preconnect hints for potential future resources
- Lazy background rendering with CSS filters

## Accessibility

- Semantic HTML5 structure
- ARIA labels where needed
- Keyboard navigation support
- Focus indicators for interactive elements
- Reduced motion support for accessibility preferences
- High contrast mode support
- Screen reader friendly

## Browser Support

- Modern browsers (Chrome, Firefox, Safari, Edge)
- iOS Safari 12+
- Android Chrome 70+
- IE11 not supported (uses modern CSS features)

## Customization

### Change Colors

Edit CSS variables in `styles.css`:

```css
:root {
    --primary-blue: #228BE6;
    --primary-blue-light: #339AF0;
    /* etc. */
}
```

### Update Content

Edit text directly in `index.html`:

- Main heading: `.heading-main` and `.heading-brand`
- Tagline: `.tagline`
- Description: `.description`
- CTA text: `.cta-text`
- Feature badges: `.feature-badge` elements

### Replace Logo

Replace `/assets/logo.svg` with your own logo. Recommended dimensions: 120x120px.

## SEO Considerations

The page includes:

- Descriptive title tag
- Meta description
- Open Graph tags (Facebook, LinkedIn)
- Twitter Card tags
- Canonical URL structure
- Semantic HTML for search engines

Remember to update the `og:image` and `twitter:image` URLs after deployment.

## Future Enhancements

Ideas for when you want to expand:

- Email signup form for launch notifications
- Countdown timer to launch date
- Social media links
- Blog or news section
- Demo video or screenshots
- More detailed feature descriptions

## License

Copyright 2026 Zonemon. All rights reserved.

## Support

For questions or issues, contact the Zonemon team.
