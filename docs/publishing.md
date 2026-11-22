# Publishing the portfolio

This guide prepares the project for sharing. **Nothing has been pushed or published.** Public release requires a full repository review and the PM's explicit approval.

## Why one README upload is not enough

The README's relative links point to other project files. If you upload only the README to Upwork, it will not upload or host those linked files. A repository keeps the artifacts together; GitHub Pages can serve the visual `index.html` as a public portfolio URL.

## Recommended setup

1. Create a GitHub account if you do not already have one.
2. Create a new repository for this project. For an initial review, keep it private.
3. Upload or push the complete project, including `index.html`, `README.md`, `docs/`, `data/synthetic_case_001/`, and `prototype/`. Do not upload `.env` or `.venv/`.
4. Review the repository contents and Git history for secrets, real patient information, employer material, and accidental outputs before changing visibility.
5. After approval to publish, make the repository public. GitHub Pages is available for public repositories on GitHub Free. In the repository, open Settings > Pages > Build and deployment, choose Deploy from a branch, select the `main` branch and `/(root)`, then save. The root `index.html` is the portfolio landing page.
6. Copy the Pages URL and add it to your Upwork portfolio entry. Also include the GitHub repository URL for readers who want the source artifacts.

GitHub Pages publishes the configured folder from the selected branch. Public Pages sites are visible on the internet, so treat publishing the site as public release of the files it serves. See [GitHub's official Pages publishing guide](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).

## Current setup status

- Visual landing page: prepared locally at [`../index.html`](../index.html).
- Repository remote: none configured.
- GitHub account/repository: not connected in this workspace.
- Public release: not approved or performed.
