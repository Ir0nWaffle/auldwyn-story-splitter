# Auldwyn Story Splitter

A small web tool for Auldwyn writers. Paste or upload a story and it gets cut into Discord-sized code blocks, broken at paragraph and sentence boundaries, ready to copy and post one at a time.

**Live version:** https://claude.ai/artifact/1JiSZA4HLNs5EhP9tppbEZ

## What it does

- Takes pasted text or an uploaded `.txt`, `.md`, `.docx` or `.html` file.
- Splits the story into posts that fit Discord's 2,000-character limit (4,000 for Nitro, or a custom limit). The count includes the code block fences and part labels, so each post fits exactly as pasted.
- Breaks between paragraphs where possible, then between lines, then sentences, then words.
- Converts bold, italic, underline and strikethrough from Word, Google Docs or web pages into Discord marks (`**`, `*`, `__`, `~~`), shown as plain text inside the code blocks so readers can copy them. If a post break lands inside formatted text, the marks are closed at the end of that post and reopened at the start of the next.
- Adds optional part labels ("Title — Part 2/5") above or inside each block.
- Tracks which posts have been copied, with a **Copy post N** button that always copies the next one.

Everything runs in the visitor's browser. Stories are never sent to a server, and drafts are saved only in that visitor's browser (`localStorage`).

## Adding it to a website

The whole tool is the single file `index.html`. There is no build step and no server code.

**Option 1: host the file.** Copy `index.html` to any static host (your web server, GitHub Pages, Netlify, Cloudflare Pages) and link to it, for example at `https://your-site/story-splitter/`.

**Option 2: embed it in an existing page.** Host the file as above, then add:

```html
<iframe src="/story-splitter/" title="Auldwyn Story Splitter"
        style="width: 100%; height: 900px; border: 0;"></iframe>
```

Copy buttons inside an iframe need clipboard permission on some browsers. If copying fails in the embed, add `allow="clipboard-write"` to the iframe.

### External files it loads

- Fonts from Google Fonts (Cinzel, Source Sans 3, JetBrains Mono). If these are blocked, the page falls back to system fonts.
- [mammoth.js 1.6.0](https://github.com/mwilliamson/mammoth.js) from cdnjs, used only to read `.docx` uploads. Everything else works without it.

If your site has a Content Security Policy, allow `fonts.googleapis.com`, `fonts.gstatic.com` and `cdnjs.cloudflare.com`, or download those files and host them yourself.

## Testing the character limit

`test/limit-test.txt` is a 2,099-character story used to confirm Discord's limit. Pasted into Discord, the counter reads **-99**. Removing the last paragraph and the blank line before it leaves exactly 1,999 characters, which sends.

## License

MIT. See [LICENSE](LICENSE). The Auldwyn team and anyone else may use, change and host it.
