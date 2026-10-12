# Auldwyn Story Splitter

A small web tool for Auldwyn writers. Paste or upload a story and it gets cut into Discord-sized posts, broken at paragraph and sentence boundaries, ready to copy and post one at a time.

**Use it here:** https://ir0nwaffle.github.io/auldwyn-story-splitter/

## What it does

- Takes pasted text or an uploaded `.txt`, `.md`, `.docx` or `.html` file.
- Splits the story into posts that fit Discord's 2,000-character limit (4,000 for Nitro, or a custom limit). Every count includes formatting marks, part labels and break markers, so each post fits exactly as pasted.
- Breaks between paragraphs where possible, then between lines, then sentences, then words.
- Converts bold, italic, underline and strikethrough from Word, Google Docs or web pages into Discord marks (`**`, `*`, `__`, `~~`). Copy always hands over the raw marks, so Discord shows the formatting after pasting. If a post break lands inside formatted text, the marks are closed at the end of that post and reopened at the start of the next.
- Tracks which posts have been copied, with a **Copy post N** button that always copies the next one.

### Post formats

- **Formatted text** (default): plain Discord messages, so the formatting shows. The preview displays bold and italics the way Discord will.
- **Full page (edit the breaks)**: the whole story as one editable page, with a line holding just `…` wherever the app would break it. Move, add or delete those lines (a line of `...` also counts) to choose the breaks yourself. Each post gets a live character count and its own Copy button, and turns red if it's over the limit. Edits survive a reload; changing the source story offers a **Re-split** rather than overwriting them.
- **Code block**: each post wrapped in a code block. Formatting marks show as plain characters there.

### Other settings

- **Part labels**: optional "Title — Part 2/5" labels (default: none). Not available in Full page, where moving a break would make the numbers wrong.
- **Include … at the end of copied posts** (default: off): adds a `…` line to the bottom of each copied post except the last.

### Saving a copy

**Save a copy with the … breaks** saves the whole story, with a `…` line at every break, under a file name of your choice as Text (`.txt`), Word (`.docx`) or Markdown (`.md`). All three keep the Discord marks as plain text, because Discord ignores Word's own bold and italics when you paste. In Full page mode the file is the page exactly as edited.

Chrome and Edge open their Save window so you can pick the folder. Other browsers, and the tool when embedded on another site, save to the Downloads folder.

Everything runs in the visitor's browser. Stories are never sent to a server, and drafts are saved only in that visitor's browser (`localStorage`).

## Adding it to a website

### Recommended: embed the hosted version

Paste this into any page on your site:

```html
<iframe src="https://ir0nwaffle.github.io/auldwyn-story-splitter/"
        title="Auldwyn Story Splitter"
        allow="clipboard-write"
        style="width: 100%; height: 900px; border: 0;"></iframe>
```

The tool appears inside your page but loads from this repo's GitHub Pages site, so it **updates automatically**. Fixes and new features show up on your site about a minute after they're pushed here, with nothing for you to do. Keep `allow="clipboard-write"`, because the Copy buttons need it in some browsers.

Or just link to https://ir0nwaffle.github.io/auldwyn-story-splitter/, which also always shows the latest version.

### Alternative: host your own copy

The tool is `index.html` plus the `assets/` folder (logo and icons), with no build step and no server code. Copy both to your own web server or static host and link to it.

This gives you full control, and changes only reach your site when you choose. The trade-off is that your copy **won't update automatically**. To get updates, download `index.html` and `assets/` from this repo again and replace your copy.

### External files it loads

- Fonts from Google Fonts (Noto Serif, the typeface auldwyn.net uses, and JetBrains Mono for character counts and code block previews). If these are blocked, the page falls back to system fonts.
- [mammoth.js 1.6.0](https://github.com/mwilliamson/mammoth.js) from cdnjs, used only to read `.docx` uploads.
- [JSZip 3.10.1](https://stuk.github.io/jszip/) from cdnjs, loaded only when someone saves a Word file.

Everything else works without them.

If you host your own copy and your site has a Content Security Policy, allow `fonts.googleapis.com`, `fonts.gstatic.com` and `cdnjs.cloudflare.com`, or download those files and host them yourself. If you embed the hosted version and your site has a Content Security Policy, add `ir0nwaffle.github.io` to `frame-src`.

## Look and icons

The styling follows [auldwyn.net](https://www.auldwyn.net/) and matches the Auldwyn Library embed: the same colors, Noto Serif, gold uppercase labels and square gold-outlined buttons. The browser tab and home-screen icons use the gold "A" mark from the Auldwyn Story Picker, and the header uses the Auldwyn logo.

## Testing the character limit

`test/limit-test.txt` is a 2,099-character story used to confirm Discord's limit. Pasted into Discord, the counter reads **-99**. Removing the last paragraph and the blank line before it leaves exactly 1,999 characters, which sends.

## License

MIT. See [LICENSE](LICENSE). The Auldwyn team and anyone else may use, change and host it.
