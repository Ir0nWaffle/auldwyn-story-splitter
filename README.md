# Auldwyn Story Splitter

A small web tool for Auldwyn writers. Paste or upload a story and it gets cut into Discord-sized code blocks, broken at paragraph and sentence boundaries, ready to copy and post one at a time.

**Use it here:** https://ir0nwaffle.github.io/auldwyn-story-splitter/

## What it does

- Takes pasted text or an uploaded `.txt`, `.md`, `.docx` or `.html` file.
- Splits the story into posts that fit Discord's 2,000-character limit (4,000 for Nitro, or a custom limit). The count includes the code block fences and part labels, so each post fits exactly as pasted.
- Breaks between paragraphs where possible, then between lines, then sentences, then words.
- Converts bold, italic, underline and strikethrough from Word, Google Docs or web pages into Discord marks (`**`, `*`, `__`, `~~`), shown as plain text inside the code blocks so readers can copy them. If a post break lands inside formatted text, the marks are closed at the end of that post and reopened at the start of the next.
- Adds optional part labels ("Title — Part 2/5") above or inside each block.
- Tracks which posts have been copied, with a **Copy post N** button that always copies the next one.

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

The whole tool is the single file `index.html`, with no build step and no server code. Copy it to your own web server or static host and link to it.

This gives you full control, and changes only reach your site when you choose. The trade-off is that your copy **won't update automatically**. To get updates, download `index.html` from this repo again and replace your copy.

### External files it loads

- Fonts from Google Fonts (Cinzel, Source Sans 3, JetBrains Mono). If these are blocked, the page falls back to system fonts.
- [mammoth.js 1.6.0](https://github.com/mwilliamson/mammoth.js) from cdnjs, used only to read `.docx` uploads. Everything else works without it.

If you host your own copy and your site has a Content Security Policy, allow `fonts.googleapis.com`, `fonts.gstatic.com` and `cdnjs.cloudflare.com`, or download those files and host them yourself. If you embed the hosted version and your site has a Content Security Policy, add `ir0nwaffle.github.io` to `frame-src`.

## Testing the character limit

`test/limit-test.txt` is a 2,099-character story used to confirm Discord's limit. Pasted into Discord, the counter reads **-99**. Removing the last paragraph and the blank line before it leaves exactly 1,999 characters, which sends.

## License

MIT. See [LICENSE](LICENSE). The Auldwyn team and anyone else may use, change and host it.
