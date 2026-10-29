# SonarBangla BhorOS — ShokalPakhi

**Edition:** EdgeOne Edition  
**Project:** SonarBangla BhorOS  
**Codename:** ShokalPakhi (also known as Khela)

ShokalPakhi is the EdgeOne-hosted edition of SonarBangla BhorOS, a browser-based desktop/console-style environment created by SonarBangla. Its deployment target is a static website hosted through EdgeOne.

> ShokalPakhi is a SonarBangla project. It is not an official Nintendo product and is not affiliated with or endorsed by Nintendo.

## Features

The exact feature set depends on which BhorOS HTML build is deployed. Recent builds include:

- A browser-based BhorOS desktop and system settings.
- Local settings and game data storage, plus JSON export/import where available in the selected build.
- eDokan **More Games** entry that opens `https://sonarbangla-edokan.edgeone.dev/` in a separate browser window/tab.
- Mii avatar stage mode configured as `body_inv_depth_mask` in the current patched build.
- Local fallback behavior for game data when optional cloud services are unavailable.

## Deploy to EdgeOne

1. Choose the intended ShokalPakhi HTML build.
2. Make a backup of the current deployed `index.html` and any associated assets/functions before replacing files.
3. Put the selected BhorOS page at the deployment root as `index.html`.
4. Include any assets and Edge Functions required by that build. Do not upload only the HTML if the project depends on separate files.
5. Use the EdgeOne project's production deployment workflow to publish the update.
6. Open the live website in a fresh browser tab and test setup, settings persistence, game launching, mobile controls if applicable, and the More Games action.

The eDokan link is `https://sonarbangla-edokan.edgeone.dev/`.

## Why More Games opens separately

The external eDokan page may block being embedded in an iframe through security headers such as Content Security Policy `frame-ancestors` or `X-Frame-Options`. BhorOS cannot override those protections from its own page. Opening the eDokan website directly in a new tab/window avoids that iframe-specific problem; it does not guarantee that the external site itself will always be reachable.

## Optional Firebase services

EdgeOne is the web host, not a replacement for Firebase Authentication or Firestore. If the selected ShokalPakhi build connects to the `sonarbangla-bhoros` Firebase project, you must separately configure the Firebase services, publish secure Firestore rules, enable the required sign-in provider, and add the EdgeOne hostname under Firebase Authentication's authorized domains. Do not assume that deploying to EdgeOne automatically deploys Firebase rules or creates a database.

## Local data and persistence

Browser-local storage is tied to the browser profile and origin and can be cleared by the user or browser. Use the site's JSON export/import feature, when present, to back up supported user data before switching deployments or browsers. Cloud persistence only applies if the selected build is configured for a backend and that backend is correctly set up.

## Troubleshooting

- **The site did not update**: confirm that the production deployment finished and that the correct project and root `index.html` were uploaded. Hard-refresh the page or test in a private window.
- **More Games does not open**: allow pop-ups for the BhorOS site or use the direct eDokan website link.
- **An iframe shows a frame/CSP error**: use the separate-window approach. Only the eDokan site owner can change its framing policy.
- **Games or sounds fail to load**: check browser network requests and the remote asset URLs. Third-party asset failures can be caused by connectivity, service availability, or cross-origin restrictions.
- **Settings did not carry over**: browser storage does not automatically transfer between different domains. Export/import supported data before moving between origins.
- **Firebase reports permission errors**: publish the correct rules to the correct Firebase project and verify the signed-in user's access. EdgeOne hosting alone cannot repair Firestore permissions.

## Release checklist

- [ ] Correct ShokalPakhi HTML selected and backed up.
- [ ] `index.html` and required assets/functions included.
- [ ] Production deployment completed.
- [ ] Live URL opened and basic UI tested.
- [ ] More Games link tested.
- [ ] Local data exported before significant upgrades.
- [ ] Firebase services and rules checked separately if this build uses Firebase.

## Status

This README describes the EdgeOne deployment flow and known browser/hosting constraints. It does not claim that the live website, external eDokan service, or optional Firebase backend has been tested as part of this README creation.
