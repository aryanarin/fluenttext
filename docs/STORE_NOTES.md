# Store submission notes

Reusable text for the Chrome Web Store and addons.mozilla.org (AMO). Version 1.2.1.

The product is called **FluentText**. Groq is named only as a supported API provider; the extension is independent and is not affiliated with or endorsed by Groq, Inc.

## Listing

**Name:** FluentText

**Short description (132 characters max):**
Proofread as you type, then rewrite and translate selected text with the AI provider you choose.

**Category:** Productivity

**Long description:**
FluentText - Your AI Writing Assistant, Everywhere

Write better, communicate clearly, and work across languages with FluentText.

FluentText is a writing assistant that works directly inside your browser. It helps you fix spelling and grammar mistakes, improve clarity, rewrite sentences, and translate text without switching tabs or leaving the website you are working on.

Whether you are writing emails, preparing documents, replying to messages, or filling out forms, FluentText helps you communicate with more confidence.

Key features

1. Smart proofreading
- Detects spelling and grammar mistakes as you type.
- Flags punctuation, clarity and style issues.
- Shows suggestions directly in the text field.
- Accept or dismiss each suggestion.
- Fix all detected issues with one click.
- Add your own words to a personal dictionary.

2. Rewriting
Choose one of two focused actions:
- Improve Writing - fixes spelling, grammar and awkward wording while preserving the original tone and meaning.
- More polite - makes the text more polite and courteous without changing its meaning.

3. Translation
- Translate selected text into other languages.
- Detect the source language automatically.
- The star menu lists only the languages you add in Settings. German is the default.
- Choose a formal or neutral register.
- Replace the selected text in place.

4. Language detection
Identify the language of selected text with a single action. You do not need to guess the source language before translating.

5. Works across websites
FluentText works in:
- Text fields and text areas.
- Email composition windows.
- Web forms.
- Rich-text editors.
- Other editable fields.
Use the floating menu, the right-click menu, or keyboard shortcuts to open its tools.

6. Quick actions and keyboard shortcuts
- Quick rewrite: Alt + Shift + F
- Quick translate: Alt + Shift + G
- Open the rewrite menu: Alt + Shift + E
- Turn FluentText on or off: Alt + Shift + K
Choose the rewrite style and target language used by the quick actions.

7. Your choice of AI provider
FluentText is not tied to a single AI service. Connect a hosted provider, a local model server, or a proxy you run yourself. Enter the endpoint, choose the authentication header, and select the models you want. The extension sends requests only to the service you configure.

8. Personalization and customization
- Personal dictionary for words you commonly use.
- Spelling and grammar preferences.
- English variant: US, UK, Canadian, Australian and Indian English.
- Translation languages and writing styles.
- Disable FluentText on specific websites.
- Adjust checking delays and other preferences.

Privacy first
Your writing belongs to you.
FluentText has no developer-operated backend, no user accounts, no analytics and no tracking.
- API credentials are stored locally in your browser and are never synced.
- Text is sent only to the AI service you configure, for features that require AI processing.
- No text is sent to a developer-operated server.
- Custom endpoints and proxy connections are configured by you.
- You remain in control of your provider and data.
Text processed by AI is transmitted to your selected provider. Its privacy and data-retention policies apply.

Browser compatibility
- Chrome and other Chromium-based browsers
- Firefox

Get started
1. Install FluentText.
2. Open Settings and choose your AI provider.
3. Add your API key or custom endpoint.
4. Start writing on any supported website.

FluentText takes care of proofreading, rewriting and translation while you focus on what matters: your message.

FluentText - Write better. Communicate clearly.

Project: https://github.com/aryanarin/fluenttext

**Metadata rule:** do not list provider brands in the store title, short description, long description, or manifest description. Chrome treats provider-name lists as keyword spam (Yellow Argon). Provider names belong only in the extension's settings screen, where they identify a working option. Use generic wording such as "the AI provider you choose" everywhere in store metadata.

**Links:**
- Homepage and source: https://github.com/aryanarin/fluenttext
- Privacy policy: https://github.com/aryanarin/fluenttext/blob/main/docs/privacy.html (or the GitHub Pages URL if you enable Pages on `/docs`)
- Support: contact@davagni.eu.org, https://ko-fi.com/ysaryan

## Single purpose

Help the user write better text: proofread, rewrite, translate and identify the language of text they type or select on web pages.

## Permission justifications

| Permission | Why |
| ---------- | --- |
| `storage` | Saves settings, the personal dictionary, disabled sites, API keys, and the Worker URL and proxy token locally. |
| `contextMenus` | Adds FluentText entries (Rewrite, Translate to, Detect language, Settings, Support) to the right-click menu. |
| `activeTab` | Lets the toolbar popup read the current tab's address to offer the per-site on/off switch. |
| `https://api.groq.com/*` | Sends text to the Groq API for checking, rewriting and translating when Groq is the selected provider. |
| `optional_host_permissions` (`https://*/*`, `http://*/*`) | Only used when the user chooses a custom OpenAI-compatible endpoint or a Cloudflare Worker / proxy. The origin is requested at runtime with `permissions.request()` from a button click, and can be revoked. A single broad optional pattern is needed because the user supplies the endpoint or Worker URL. |
| Content script on `http://*/*` and `https://*/*` | Detects editable fields on any page to show suggestions. The script never reads or sends text from fields it skips (password, email, code editors, `spellcheck="false"`). |

No remote code is loaded. The extension has no analytics and no servers of its own. Requests go to the selected provider or to the user's own proxy.

## Data disclosure

- **Collected:** website content (the text of the field being checked or the selection being rewritten or translated) and authentication information (the API key or proxy token the user enters for their provider or Worker).
- **Purpose:** only to provide the proofreading, rewriting, translation and language-detection features, and to authenticate requests to the provider or Worker the user chose.
- **Recipient:** the configured provider (Groq, Inc. at `api.groq.com` by default), the custom endpoint the user enters, or the Cloudflare Worker / proxy the user runs.
- **Not collected:** browsing history, identifiers, location, analytics, or anything else.
- **Retention:** the extension stores nothing on a server. Keys, proxy URL/token and settings stay in the browser profile. The provider's or proxy operator's own policy applies to text and authentication information it receives.
- **Sale and sharing:** no sale, no sharing beyond transmitting the request to the provider the user configured.
- **Chrome Web Store privacy practices:** select **Website content** and **Authentication information**; both are used for the single purpose above and transferred to the user-selected provider.

AMO: `data_collection_permissions.required = ["websiteContent", "authenticationInfo"]`.

## Reviewer notes

- A provider key, custom endpoint, or Worker URL is required to see suggestions. Reviewers can create a free Groq key at https://console.groq.com/keys, or a test key can be provided in the reviewer notes field.
- Test steps (Groq): open the extension's settings, paste a Groq key under **Connection**, click **Save connection**, then **Test connection**. Open any page with a textarea, type `Teh quick brwon fox jump over teh lazy dog`, wait about a second, and click an underline. Select text and click the blue star for rewrite and translate.
- Test steps (custom endpoint): under **Provider** choose **Custom / other**, enter an OpenAI-compatible base URL, choose the authentication header, enter the key, save, accept the browser's host-permission prompt, and test.
- Test steps (Worker proxy): under **Provider** choose **Cloudflare Worker / proxy**, enter the Worker URL exactly as deployed, enter the optional **Proxy token** if the Worker sets `PROXY_TOKEN`, click **Test connection**, then **Save connection**. The test sends one short chat request; there is no model list to load.
- Settings > **Quick actions and shortcuts** shows the current key bindings and opens the browser's shortcut manager. Browsers, not extensions, assign shortcut keys.
- Support is reachable from the popup, the settings header, the in-page badge panel, the star menu, result cards, and the right-click menu.

## Store assets

Ready in `docs/store-assets/`:

| File | Use |
| ---- | --- |
| `screenshot-1-proofreading.png` | 1280x800 — underlines and the suggestion panel |
| `screenshot-2-rewrite.png` | 1280x800 — rewrite and translate menu |
| `screenshot-3-translation.png` | 1280x800 — translated result card |
| `screenshot-4-connection.png` | 1280x800 — the new settings layout, provider connected |
| `screenshot-5-proxy.png` | 1280x800 — Cloudflare Worker / proxy settings, saved |
| `store-icon-128.png` | 128x128 store icon: 96x96 artwork with 16px transparent padding |
| `promo-440x280.png` | 440x280 small promo tile, 24-bit PNG with no alpha |
| `marquee-1400x560.png` | 1400x560 marquee promo tile, 24-bit PNG with no alpha |

The screenshots were captured from the running 1.2.0 build against a local demo page and a local proxy endpoint; 1.2.1 changes only the sidebar selection logic and store metadata, so the visible UI is unchanged. The API key and proxy token shown are masked test values. The extension icons (16, 48, 128) live in `chrome/icons/` and are generated by `tools/make-icons.ps1`. The promo and marquee tiles are generated by `tools/make-promo.ps1` and `tools/make-marquee.ps1`; both draw the shared artwork from `tools/icon-art.ps1`.
