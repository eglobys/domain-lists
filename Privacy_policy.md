# Privacy Policy — History Collector

**Effective date:** September 9, 2026

This policy explains what data the History Collector Chrome extension
("the extension," "we," "it") collects, how it's used, and who it's
shared with. It's written to match exactly what's declared in the
extension's Chrome Web Store listing and `manifest.json` — if the two
ever disagree, this document is out of date and should be updated before
resubmission.

## Summary

Everything the extension collects is stored **locally, in your own
browser** (`chrome.storage.local` / `chrome.storage.session`). We do not
operate a server, we do not receive your data, and we do not sell or
share it with advertisers or data brokers. The only outside destination
your data can go to is Anthropic's API — and only when you take an
explicit action (clicking "Analyze with AI" or "Check this page"), using
an API key you provide and control yourself.

## What data the extension collects

| Data | What it is | Where it's stored | Sent anywhere? |
|---|---|---|---|
| Browsing history | Page URL, title, domain, and visit timestamp | Locally (`chrome.storage.local`) | No |
| Time-on-page | How long each page was the focused, active tab | Locally, attached to the matching history entry | No |
| Domain lists | Your synced whitelist/blacklist and any temporary domains you add | Locally | No (the sync itself is a read-only fetch of a public JSON file — see "Domain list sync" below) |
| Anthropic API key | The key you enter to enable AI features | Locally only | No — sent only to `api.anthropic.com`, directly from your browser, when you use an AI feature |
| Page content (AI safety check) | Visible text, page title, meta description, form structure (action/method/whether a password field exists — never field *values*), and external link domains of the page you're currently on | Not stored — read at the moment you click "Check this page," used to build the request, then discarded | Yes, to Anthropic's API, only when you click that button |
| Browsing summary (AI Insights) | An aggregated summary — time per domain, visit counts, time-of-day patterns — for whichever date range you've selected | Not stored separately — derived from your local history at the moment you click "Analyze" | Yes, to Anthropic's API, only when you click that button |

We do not collect: personally identifiable information, health
information, financial or payment information, authentication
credentials (passwords, form values), personal communications, or
location data.

## How your data is used

- Browsing history and time-on-page data are used to power the
  extension's own stats page (charts, daily totals, domain breakdowns)
  and CSV/JSON export — features you use directly, for yourself.
- Domain lists are used to decide whether a page you navigate to should
  load normally, show a warning, or open as usual.
- The Anthropic API key and any data sent alongside it are used solely to
  generate the AI Insights summary or page-safety verdict you requested.

None of this data is used for advertising, analytics about you, or any
purpose other than the feature you're actively using.

## Who your data is shared with

- **Anthropic** (`api.anthropic.com`) — receives requests only when you
  click "Analyze with AI" or "Check this page," authenticated with your
  own API key. What's sent is described in the table above. Anthropic's
  own privacy policy and API terms govern how they handle that request;
  the extension has no visibility into or control over Anthropic's
  retention beyond what their API terms state.
- **GitHub** (`raw.githubusercontent.com`) — the extension periodically
  fetches a public JSON file listing whitelisted/blacklisted domains.
  This is a one-way, read-only request; no data about you or your
  browsing is sent as part of this fetch.
- **No one else.** We don't run a backend server, we don't have an
  analytics/telemetry pipeline, and we don't sell, rent, or otherwise
  transfer your data to third parties.

## Data retention and your controls

Because everything lives in your browser's own local storage, you're in
direct control of it:

- **Clear Data** (popup) — wipes all collected history/duration data.
- **Remove** (API key settings, stats page) — deletes your stored
  Anthropic API key.
- **Clear** (session bypasses, stats page) — clears any blacklist domains
  you've temporarily allowed.
- **Uninstalling the extension** removes all locally stored data
  (history, settings, API key, domain lists) along with it, since none of
  it exists anywhere else.

Session-only data (the currently-tracked tab's timer, temporary domain
overrides, blacklist bypasses) is stored in `chrome.storage.session` and
is automatically cleared when your browser restarts.

## Permissions this extension uses

A plain-English explanation of why each permission is requested is
maintained in the project repository
(`CHROME_WEB_STORE_PRIVACY_ANSWERS.md`) and in the Chrome Web Store
listing itself. In short: `history`, `tabs`, and `activeTab` let it read
and display your own browsing data back to you; `storage` and `alarms`
let it save your data and run periodic tasks locally;
`declarativeNetRequest` and `webNavigation` power the domain-blocking
feature; `scripting` and the content script power the optional
page-safety-check feature; and the host permissions allow the two
outbound connections described above (Anthropic's API and the public
domain-list file on GitHub).

## Children's privacy

This extension is not directed at children and does not knowingly
collect data from children.

## Security

Data stored locally is protected by Chrome's own extension storage
sandboxing (each extension's storage is isolated from other extensions
and from web pages). We recommend keeping your Anthropic API key private,
since anyone with local access to your browser profile could, in
principle, use it — the same as any other locally-stored credential.

## Changes to this policy

If what the extension collects or does changes, this document will be
updated to match, along with the corresponding Chrome Web Store listing
disclosures. Check the effective date above to see when it was last
revised.

## Contact

Questions about this policy or the extension's data practices can be
raised via an issue on the project's GitHub repository.
