# CodeAssist Demo

> **Educational demo only.** All patient notes and codes are fictional or sample data. This project is not for real patients, medical decisions, insurance claims, or billing. Never enter real patient information.

CodeAssist Demo shows a safe, simplified medical-coding workflow: an assistant suggests codes for a fictional patient note, and a **human approves, edits, or rejects every suggestion**. It is a portfolio and learning project.

**Live demo:** `https://nidheesh1205.github.io/codeassist-demo/` (after you turn on GitHub Pages, see below)

## What it does

- Eight fictional sample notes (diabetes follow-up, cough and wheeze, ankle injury, sore throat, asthma flare, migraine, urinary symptoms, low back pain), or type your own made-up note
- **Suggest codes** returns sample ICD-10-CM and CPT suggestions with:
  - a confidence score (High, Medium, or "Review closely")
  - a plain-language explanation
  - highlighted evidence in the note (hover a card to see where it came from)
- **Missing information** lists details the note doesn't state that would make the codes more specific
- **Approve / Edit / Reject** on every suggestion. Rejecting asks for a reason, and you can leave reviewer notes
- **Recent reviews** shows fictional history, plus any review you finish in the session
- Responsive layout for laptop and phone, light theme with blue and teal accents

## How it works

There is no AI model and no backend in the default version. Suggestions come from hard-coded keyword rules in the `analyze()` function in `index.html`. The confidence scores are fixed sample values, not model outputs. Some are low on purpose (for example, a symptom code that a diagnosis already explains) to show why human review matters.

Everything runs in the browser. Nothing you type is sent anywhere.

## Run it locally

No build step. Download the repo and open `index.html` in a browser.

## Add your own sample notes

1. Add an entry to the `SAMPLES` array in `index.html` (an `id`, a `label`, and the note `text`).
2. Add or adjust a rule in `analyze()` so the note produces suggestions. Each rule checks the text with a regular expression and calls `add({...})` with a code, description, confidence, evidence, and explanation.
3. Keep every note fictional.

## Optional live mode

The page contains an optional "Claude (live)" switch that only appears when the page runs inside claude.ai. On GitHub Pages or a local file it stays hidden, and the sample rules are used.

To add real AI suggestions to your own deployment, put a small server-side function (for example on Vercel or Cloudflare Workers) between the page and an AI provider so your API key never reaches the browser. Have the page send the note to that function and render the returned suggestions in the same format `analyze()` produces. Keep the human review step, and keep the data fictional.

## Notes on code sets

ICD-10-CM codes are published by the U.S. government. CPT codes and official descriptions are owned by the American Medical Association. The descriptions in this demo are simplified, in the author's own words, and illustrative only, so they may not match official code descriptions. Check the AMA's licensing terms before expanding CPT use in a public project.

## Limitations

- Sample rules cover only a handful of conditions and will return nothing for other text
- Codes, confidence scores, and explanations are illustrative and not clinically or financially validated
- Review history lives in memory and resets on reload

## License

MIT. See `LICENSE`.
