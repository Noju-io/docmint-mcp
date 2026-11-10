# Docmint

PDF and image tools for Claude: compress, merge, split, rotate, delete and reorder pages, page numbers, watermark,
crop, resize, grayscale, OCR, extract text, PDF to JPG or PNG, images to PDF, text to PDF, sign, protect, unlock,
flatten, edit metadata, compare and inspect PDFs, and compress, resize or convert images (HEIC, WebP, PNG, JPG).

![Docmint](icon.png)

## Install

On claude.ai or in Cowork: **Customize > Plugins > Add > Add marketplace**, enter `Noju-io/docmint-mcp`, then add Docmint.

In Claude Code:

```
/plugin install docmint --marketplace Noju-io/docmint-mcp
```

## Use it

Ask Claude in plain words, for example:

- "Compress report.pdf so it's under 2 MB."
- "Merge these three PDFs in this order."
- "Make this scanned contract searchable."
- "Turn the photos in this folder into one PDF."
- "Remove the password from statement.pdf." (you provide the password)

**In Claude Code, and in Cowork on your computer,** the plugin starts the Docmint MCP server locally
(`npx -y docmint-mcp@0.1.1`, needs Node.js 20 or newer). Claude works on your files directly and writes the
results next to the originals.

**In claude.ai chat,** local servers don't run. Connect **docmint-links** from the plugin's Connectors tab:
Claude finds the right tool and gives you a Docmint link with the settings filled in. You open it, add your
file, and it is processed in your browser.

The plugin's skill tells Claude when to use these tools and how to choose settings.

## Plans

Without an account you get 3 runs a day. Ask Claude to "connect my Docmint account" to use your account's plan:
10 runs a day on the free plan, unlimited on Pro. Plans: https://docmint.io/pricing

## What it runs, sends and fetches

- **Runs:** the `docmint-mcp` package from npm, version 0.1.1 (the built package is in the root of this repository). It reads and
  writes only the files you or Claude point it at.
- **Your files are never uploaded.** All PDF and image processing happens on your computer (local server) or in
  your browser (links).
- **Sent to docmint.io by the local server:** one request per run to count it against your plan, carrying the
  tool name, the number of files, a random device id stored in `~/.docmint/config.json`, and your Docmint API key
  if you connected an account. No file names or contents.
- **Fetched by the local server:** the OCR language model, from the tesseract.js data CDN, the first time you run
  OCR. It is cached in `~/.docmint/tesseract`.
- **Sent to docmint.io by the docmint-links connector:** the task text and the settings Claude passes to its
  tools, used to build the link and not stored.

Privacy policy: https://docmint.io/privacy. Terms: https://docmint.io/terms. Setup guide and other AI apps:
https://docmint.io/mcp. Support: hello@docmint.io.

## License

MIT
