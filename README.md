# storno-import-obb-eu[README (1).md](https://github.com/user-attachments/files/29937537/README.1.md)
# Mat Star → UBB import file generator

A single static page. No server, no backend — everything happens in the
visitor's browser (the .docx never leaves their computer).

## What it does

1. Drag & drop the `.docx` list of customers (name / IBAN / reference / amount blocks).
2. The page groups the lines into one record per customer, pulls out the IBAN,
   guesses the bank's BIC from the IBAN's bank code, and sums any amount-looking
   numbers in that customer's block.
3. You get an editable table to check and fix anything before exporting —
   rows highlighted in orange are missing an IBAN or amount and need a manual fix.
4. Click "Изтегли .txt" to download a file in UBB's **"Превод в евро в
   страната" (IBAN311)** format, ready to upload under eBB → Импорт на файл.

## Known limitation — please read

The source Word file isn't perfectly consistent: most customers have a clean
4-line block (name / IBAN / reference / amount), but some have several
invoice lines with their own amounts, and a few of those blocks also include
a pre-summed subtotal line. The tool sums *every* number that looks like an
amount (digits + `,` or `.` + 2 decimals) in a customer's block — for the
simple cases this is exactly right, but for a handful of multi-line entries
it can double-count if the source already included a subtotal.

**Always glance at the "Суров текст" (raw text) column for any customer with
more than one invoice line before exporting**, and correct the amount field
by hand if needed. The three rows that have no recognizable amount at all
are flagged automatically and blocked from being right until you fill them in.

## Hosting on GitHub Pages

1. Create a new repo (or a folder in an existing one) and add `index.html` from this folder.
2. Push to GitHub.
3. In the repo: **Settings → Pages → Deploy from a branch**, pick `main` (or `master`) and the `/ (root)` folder.
4. GitHub gives you a URL like `https://<username>.github.io/<repo>/` — share that with your colleague. That's it, no build step, no dependencies to install.

## Local use

You can also just double-click `index.html` to open it in a browser — it works
fully offline once the one CDN script (JSZip, for reading the .docx) has loaded once.
