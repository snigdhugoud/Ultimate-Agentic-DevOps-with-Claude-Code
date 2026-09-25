# CLAUDE.md
# Claude Code Instructiond

## Project Overview

This repository contains a static portfolio website for the DevOps Micro Internship (DMI) Week 1 exercise. It is intended to be hosted on an Ubuntu VM with Nginx.

## Preferred Production Architecture

This project is a static HTML/CSS website, so the simplest deployment is an *AMS*S3-hosted static site behind *CloudeFront* for caching and HTTPS. If infrastructure is being provisioned as code, use *Terraform* to define the S3 bucket, CloudFront distribution, bucket policies, and any required IAM permissions. Keep the repo framework-free and avoid adding build steps or package management unless explicitly required.

## Project Structure

- `index.html` - Main portfolio page and primary site entry point.
- `privacy.html` - Privacy policy page.
- `terms.html` - Terms and conditions page.
- `style.css` - Shared stylesheet for the main page.
- `images/` - Logo, hero, signature, and other website assets.
- `README.md` - Internship context and deployment requirements.

## Development Guidelines

This is a plain HTML/CSS project. There is no package manager, build step, test suite, or lint configuration.

For local preview, serve the repository root with a static HTTP server:

```powershell
python -m http.server 8000
```

Then open `http://localhost:8000/` in a browser. Opening `index.html` directly also works, but an HTTP server more closely matches the intended deployment environment.

On Windows, Python may be unavailable. If `python -m http.server 8000` fails, use an existing Node.js static server or the VS Code Live Server extension for local preview. Do not add a runtime dependency to the project just to preview these files.

The intended production setup is an Ubuntu VM running Nginx with this repository served as the site root. After deployment, verify the site through the VM's public IP and keep it live for the required 24-hour submission period.

Before deployment, update the footer in `index.html` with the deployer's cohort, name, group, week, and date. Keep this ownership proof visible in the browser screenshot; do not remove or hide it.

- Keep the site framework-free and preserve the existing HTML/CSS structure.
- Preserve the existing inline JavaScript used for the mobile menu and section navigation unless the requested change requires it.
- Prefer small, focused changes and reuse the existing stylesheet and image assets.
- Do not add a package manager, build tool, framework, or dependency for a static-site change.
- Preserve working external links, section anchors, responsive behavior, and useful image alt text.
- Treat the missing DMI ownership-proof footer line as a deployment blocker and add the deployer details before release.
- Treat duplicate animation definitions, distorted hero media, and unsafe new-tab links as known issues to correct when touching those areas.

## Testing and Verification

Before considering a change complete:

1. Load the home page and confirm the layout works on desktop and mobile widths.
2. Check navigation links, section anchors, and the mobile menu.
3. Check that `privacy.html` and `terms.html` load correctly.
4. Confirm every image has a valid path and useful alt text.
5. Confirm the required ownership proof is visible in the footer before deployment.
6. Check the browser console for errors.
7. When editing the stylesheet, avoid retaining duplicate `@keyframes fadeUp` definitions.
8. Keep the hero image aspect ratio intact; do not use `object-fit: fill` unless distortion is intentional.
9. When adding external links with `target="_blank"`, include `rel="noopener noreferrer"`.

## Git and Commit Guidelines

- Keep commits focused on one website or documentation change.
- Review `git diff` before committing and do not include generated files or local server output.
- Never commit credentials, deployment secrets, or machine-specific configuration.
- Do not rewrite history or discard unrelated user changes.
