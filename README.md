# CodeCursor (Revival)

> **This is a maintained fork of [Helixform/CodeCursor](https://github.com/Helixform/CodeCursor).**
> The original project was archived on October 2024 with 17 open issues and no maintainer activity. We picked it up, fixed what was broken, and shipped it.

<p>
  <img src="https://img.shields.io/badge/original-archived-critical.svg" alt="Original Status">
  <img src="https://img.shields.io/badge/open%20issues%20(original)-17-red.svg" alt="Original Issues">
  <img src="https://img.shields.io/badge/last%20original%20commit-2024--10-lightgrey.svg" alt="Last Original Commit">
  <img src="https://img.shields.io/badge/stars-1.8k-blue.svg" alt="Stars">
  <img src="https://img.shields.io/badge/revival-active-brightgreen.svg" alt="Revival Status">
</p>

**CodeCursor** brings [Cursor](https://www.cursor.so) AI capabilities directly into VS Code — code generation, editing, chat, and project scaffolding — without leaving your editor.

---

## What Changed

The original extension wouldn't build or run on modern toolchains. These fixes get it working again:

| # | Fix | Original Issue |
|---|-----|----------------|
| 1 | Updated `wasm-bindgen` to 0.2.88+ (Rust WASM wouldn't compile on Rust 1.73+) | [#59](https://github.com/Helixform/CodeCursor/issues/59), [#60](https://github.com/Helixform/CodeCursor/issues/60) |
| 2 | Aligned `wasm-bindgen-futures` and `js-sys` versions to fix module resolution errors | — *(build breakage, no report)* |
| 3 | Fixed TypeScript `ProgressOptions` type mismatch blocking extension compilation | [#56](https://github.com/Helixform/CodeCursor/issues/56), [#50](https://github.com/Helixform/CodeCursor/issues/50) |
| 4 | Fixed build pipeline so the extension can be packaged into a working .vsix | [#51](https://github.com/Helixform/CodeCursor/issues/51), [#62](https://github.com/Helixform/CodeCursor/issues/62) |

## Still Broken

These are known issues we haven't gotten to yet. PRs welcome.

- [ ] Authentication flow may fail — Cursor OAuth endpoint behavior has changed since the extension was last maintained ([#52](https://github.com/Helixform/CodeCursor/issues/52))
- [ ] Custom API base URL not configurable — users behind proxies or using Azure OpenAI can't set their endpoint ([#55](https://github.com/Helixform/CodeCursor/issues/55))
- [ ] Azure OpenAI integration needs guidance ([#47](https://github.com/Helixform/CodeCursor/issues/47))
- [ ] Sidebar/chat panel may not appear in some VS Code versions ([#53](https://github.com/Helixform/CodeCursor/issues/53))
- [ ] Long code continuation unavailable (upstream Cursor API limitation)
- [ ] Multiple simultaneous `Generate Project` invocations cause undefined behavior

*If you hit something not listed here, [open an issue](https://github.com/AttacktheDPoint-com/CodeCursor-revival/issues).*

---

## Install

**From .vsix (recommended for now):**

1. Download `aicursor-0.5.3.vsix` from the [Releases](https://github.com/AttacktheDPoint-com/CodeCursor-revival/releases) page
2. In VS Code: `Ctrl+Shift+P` > `Extensions: Install from VSIX...` > select the file
3. Sign into your Cursor account or configure an OpenAI API key in settings

**Build from source:**

```bash
# Requires: Node.js 19+, Rust, wasm-pack
npm install
npm run package
npx @vscode/vsce package
# Install the generated .vsix file in VS Code
```

## Usage

- **Generate Code**: `Ctrl+Shift+P` > `CodeCursor: Generate Code` (or right-click in editor)
- **Chat**: Click the CodeCursor icon in the Activity Bar sidebar
- **Generate Project**: `Ctrl+Shift+P` > `CodeCursor: Generate Project` (experimental)
- **API Key**: `Ctrl+Shift+P` > `CodeCursor: Configure API Key`

Select code before generating to edit/replace existing code. Generated changes appear as a live-streamed diff — click "Accept" or "Reject".

---

## Support This Project

This project was revived by **[Attack the D Point](https://github.com/AttacktheDPoint-com)** — we find abandoned open-source projects, fix them, and ship them.

If this fix saved you time, consider supporting the work:

<a href="https://github.com/sponsors/AttacktheDPoint-com"><img src="https://img.shields.io/badge/Sponsor_on_GitHub-%E2%9D%A4-ea4aaa.svg" alt="GitHub Sponsors"></a>
<a href="https://ko-fi.com/atdpt"><img src="https://img.shields.io/badge/Buy_a_Coffee-ko--fi-ff5e5b.svg" alt="Ko-fi"></a>

Your support helps us keep reviving projects like this one. See what else we're working on at [AttacktheDPoint-com](https://github.com/AttacktheDPoint-com).

---

## Credits

All credit for the original project goes to **[Helixform](https://github.com/Helixform)** and its contributors. This fork exists because the original was too good to let die.

*Licensed under MIT — same as the original.*

---

<details>
<summary><strong>Original README</strong></summary>

# CodeCursor (Cursor for Visual Studio Code)

**Use Cursor right in the editor you love!**

First of all, we would like to thank **Cursor Team** for their brilliant works. Please give their [app](https://www.cursor.so) a try!

## What's Cursor? And Why This Extension?

Cursor is an AI code editor based on OpenAI GPT models. You can write, edit, and chat about your code with it. At this time, Cursor is only provided as a dedicated app, and the team currently has no plans to develop extensions for other editors or IDEs.

We believe there are more developers actively using Visual Studio Code as their main tool for serious work. This is why we built **CodeCursor**. It's not going to replace the Cursor app, but it provides another way to use Cursor.

## Getting Started

You must sign into your Cursor account or configure you own API keys to use this extension. Please refer to the Custom API Keys section for details.

### Code Generation

Just open a document and type `CodeCursor` in Command Palette. You will see the command below.

Type your prompt and the code generation will just begin. To edit some existing code, you can also select something before performing this command. When accepting the change, the selected code will be replaced with the generated one.

While code generation is in progress, a status bar item will be displayed. Click on it to cancel the request. Upon completion of code generation, the status bar item will change to a "check mark". You can click it to reopen the generated result at any time.

The generated contents will be live streamed, and shown as a text diff. You can simply apply the changes by clicking the "Accept" button in the notification.

### Chat

You can chat with your code just like using ChatGPT. To open the chat panel, click "CodeCursor" icon on the Activity Bar. You can ask questions about the currently opened document or a selected piece of text.

## Custom API Keys

The Cursor server may become unstable when it's under heavy traffic. You can provide your own OpenAI API keys to have a smoother user experience. You can also choose the model you want to use when a key is set. For details, please refer to the extension configuration.

> **Note:**
> Your API key will be sent to Cursor server.

## Known Issues

- Due to limitations in the new version of the Cursor API, the automatic continuation ability for long code is currently unavailable.
- If you trigger `Generate Project` command multiple times simultaneously, undefined behavior may occur.

## Security Consideration

The extension **DOES NOT** collect your code, environment data, or any information that could be used to track you. Additionally, we ensure that the Cursor server will not receive that data either. Only the document you perform code generation against will be uploaded to the Cursor server, and they are responsible for preventing any leaks of your code.

## License

MIT

</details>
