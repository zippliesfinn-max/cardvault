# CARDVAULT — Windows-only PWA

This build is a Progressive Web App (PWA). It does **not** need Xcode, a Mac, iTunes, an IPA, or Apple signing.

## What is included
- Dark CARDVAULT interface, responsive for iPhone and desktop.
- Camera capture using the phone's rear camera (browser permission required).
- OCR-assisted name suggestion using Tesseract.js loaded from its CDN.
- Search against the public Pokémon TCG API.
- Collection stored in IndexedDB, not cookies or session storage.
- Automatic save after adding a card; closing/reopening the app does not remove the collection.
- Service worker caches the app shell for repeat/offline opening.
- JSON export and import for backup/restore.
- Raw EUR Cardmarket and USD TCGplayer estimates when present in API responses.

## Important limits
- Camera access and PWA installation require HTTPS. `file://` will not work. Localhost is allowed for development.
- OCR is a name suggestion, not guaranteed card recognition. The user must verify the exact printing before saving.
- A 2–3 second scan is not guaranteed; OCR, device speed, lighting, and API latency vary.
- Graded PSA 10 / BGS 10 / CGC 10 prices are not included. Those require a legitimate licensed data source.
- No Gmail sign-in or cloud sync is implemented. Data stays in that browser's local IndexedDB. This is persistent across closing/reopening, but clearing browser/site data, uninstalling/resetting the browser, or changing devices can remove it. Export backups regularly.
- The Pokémon TCG API and Tesseract CDN need internet access for search/OCR. Previously cached app shell may open offline, but remote search will not.
- Public API availability and its data are not guaranteed. Review the provider's terms before commercial use.

## Fastest setup (recommended): GitHub Pages
1. On Windows, extract `CARDVAULT-WINDOWS-PWA.zip`.
2. Create a GitHub account if you do not have one, then create a **public** repository named `cardvault`.
3. Upload all files and folders from this extracted project to the repository root (not the ZIP itself).
4. In the repository, open **Settings → Pages**.
5. Under Build and deployment, choose **Deploy from a branch**, select `main` and `/ (root)`, then Save.
6. Wait for GitHub Pages to publish. Your site URL will look like `https://YOUR-USERNAME.github.io/cardvault/`.
7. Open that HTTPS URL on your iPhone in Safari. Tap Share → **Add to Home Screen** → Add.
8. Launch CARDVAULT from the new Home Screen icon. Allow camera permission when prompted.

## Alternative: test locally on Windows
1. Install Python 3 from python.org.
2. Open PowerShell in the extracted project folder.
3. Run `py -m http.server 8000`.
4. On the same PC, open `http://localhost:8000`.
   - This localhost test is suitable for desktop preview. To test iPhone camera from another device, use an HTTPS host such as GitHub Pages; ordinary LAN HTTP is not a secure camera context.

## Data persistence
The app uses IndexedDB in the browser's origin. It does not rely on cookies, so normal cookie cleanup is less likely to affect it. On first launch it also asks the browser for persistent storage permission where supported. This is still not a substitute for backups. Use **Vault → Export Backup** or Settings → Export Collection Backup. Import the JSON backup on another browser/device to restore.

## Updating
Upload the newer files to the same GitHub repository. The service worker cache version changes when the app is updated; close and reopen the installed PWA if an older cached screen remains.
