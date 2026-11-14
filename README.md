# ShinyProtector companion downloads

This repository hosts distribution documentation only, not the project source repository.

**No companion download is published yet.** The Linux x86-64 archive has been built and tested locally, but its upload is pending. Windows/macOS installers are not available yet. Do not treat a GitHub draft release as an accessible download.

The Chrome Web Store extension remains an unpublished draft, configured for Unlisted distribution. Once approved and published, anyone with its store link can install without an invitation list. No Canvas test account or credentials are supplied.

The instructions below describe the prepared Linux review build and apply once its archive and checksum are available.

---

# ShinyProtector 0.0.5 — Linux companion review build

This is a development **connection-status-only** companion, not a course reader or offline archive. The browser extension is a separate Chrome Web Store draft and has not been submitted or published. This download does not install or publish that extension.

## Requirements

- Linux x86-64 with a graphical desktop, Electron-compatible system libraries and working Chromium sandbox support. No root access, Node.js or npm is needed to launch the included build. Do not run as root or disable the sandbox.
- A supported Chromium browser installed and launched at least once. Registration recognizes the usual Google Chrome, Chromium and Helium profile roots. This build is Linux-only; no Windows/macOS support is claimed.
- For the authenticated state, an account you are authorized to use on an HTTPS Canvas site under `*.instructure.com`. Custom institution domains are unsupported. No publisher/student credentials are provided. A separate supplied test account is not a universal Chrome Web Store requirement, but authenticated testing cannot be demonstrated without authorized access.

Validation covers isolated Linux Chromium/Electron tests and an owner-reported successful real Linux/Helium connection. This does not establish compatibility with every Linux distribution, institutional deployment or the final consumer store-install route.

## Download and launch

Download `ShinyProtector-0.0.5-linux-x64.tar.gz` and `SHA256SUMS` from the same release. In the download directory:

```sh
sha256sum --check SHA256SUMS
tar -xzf ShinyProtector-0.0.5-linux-x64.tar.gz
cd ShinyProtector-0.0.5-linux-x64
./ShinyProtector.sh
```

Extract somewhere you control and keep the directory in place: the native registration points to the extracted executable. This is a portable development archive, not a signed installer or automatic updater. Its Electron runtime and compiled application are included. The project source repository is not being published with this release; bundled JavaScript is necessarily inspectable application code.

Launching the companion creates its own native-host registration in detected existing browser profile roots and private connection metadata in the ShinyProtector OS application-data directory. It never overwrites an unknown or conflicting registration. If `REGISTRATION_CONFLICT` appears, stop and inspect the named app-owned registration; contact support rather than deleting unrelated files. Do not run a checkout-based development app at the same time as this build.

## Review walkthrough

1. Install the submitted extension in the review environment. Its ID must be `nmecinppodlgkibgkdbgfkmhcgjiebkh` and version 0.0.5. This download is only the companion; it does not provide a publicly available store installation while the extension remains a draft. The extension opens no setup tab or popup.
2. With the app closed, the extension waits for the app and must not discover Canvas sites or request its API.
3. Launch the companion. A fresh app-data directory shows **Connect Canvas**, a disclosure and Privacy policy. Before approval, no discovery, stored-origin reads, Canvas fetches or script injection are authorized.
4. Choose **Connect Canvas** in the app. There is no extension-side enable button or institution configuration. Browser-managed installation and site-access permissions still apply.
5. In that same browser/profile, sign in normally to a Canvas account you are authorized to use and visit its supported Canvas site. Never share a real student's login with the publisher or enter it into this app. Allow about a minute for native availability retries.
6. Expect **Checking Canvas connection…**, then **Canvas connected** with only the institution host and a simple check. The extension toolbar indicates `OK`. The only Canvas API endpoint is `GET /api/v1/users/self`. The browser validates and discards the profile JSON and account ID; only origin/status is transferred locally. There are no course, syllabus, grade, submission, assessment or messaging operations.
7. Normal identity checks repeat approximately every five minutes while the app is open; completed Canvas visits can trigger earlier login checks. HTTP 403 pauses until browser restart/permission change; HTTP 429 pauses for fifteen minutes. Browser alarms are not exact timers.
8. Close the app: authorization is revoked and checks stop. Reopen it: saved app consent avoids another enable prompt, but a fresh live native handshake is required. A browser restart needs an open Canvas tab/new visit to rediscover the institution.

Without authorized Canvas access, installation, onboarding, consent persistence, waiting states and stopping behavior can be checked, but the authenticated success state cannot be independently demonstrated. We do not claim an offline fixture is the actual Canvas service. Reviewers may request additional access; no approval guarantee is implied.

## Privacy and cleanup

No browser password, raw cookie or token is extracted/exported. The connector has no developer-operated data server, analytics or advertising. Canvas itself can record API access activity. Memory-backed retry origins/times end with the browser session; no permanent institution/profile/content data is saved by the extension.

Close the app before cleanup. Disable/uninstall the extension in the browser. On a standard Linux setup, the app's metadata is under `${XDG_CONFIG_HOME:-$HOME/.config}/ShinyProtector/`; saved approval is `connection-consent-v1.json`. Removing that receipt while closed makes the next launch ask again. Do not delete browser profiles or unrelated native hosts.

This portable build has no automatic uninstaller. Native registration files are named `com.shinyprotector.connector.json` under supported browsers' `NativeMessagingHosts` directories. Remove only registrations you have confirmed point to this build's app-owned launcher, plus the app-owned launcher when no other installation uses it; contact support if unsure. Back up conflicting registrations before intentionally switching installations. Keep the extracted directory until its registrations are removed. Browser/OS backups may retain files.

Privacy policy: https://gist.github.com/LyKhoris/f756307fca5e124c2068854b58e82073

Contact: shinobulaugh@gmail.com. Independent project; not affiliated with Instructure or an institution.

## Third-party notices

The archive includes Electron's `runtime/LICENSE` and `runtime/LICENSES.chromium.html`, Svelte's `licenses/Svelte-LICENSE.md`, and Figtree/Catppuccin notices in the renderer directory. These notices apply to their respective bundled third-party materials.
