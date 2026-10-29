# Strata: PRC Geology board review

A quiz site built from the PRC Geologist Licensure Exam question bank (1,198 items).

## Put it on GitHub Pages

1. Create a repository and upload `index.html` (that's the only file the site needs).
2. Repository **Settings → Pages → Build and deployment**: Source "Deploy from a branch", branch `main`, folder `/ (root)`. Save.
3. Open the URL GitHub shows (e.g. `https://<username>.github.io/<repo>/`) and enter PIN **1212**.

Do **not** upload the `.xlsx` to the repository; that would expose the questions.

## How the PIN works

The questions are encrypted inside `index.html` (AES-256-GCM, key derived from the PIN with 400,000 PBKDF2 rounds), so viewing the page source shows only scrambled text. A 4-digit PIN can still be brute-forced by someone determined, so treat this as "keep casual visitors out", not real security. Use a longer PIN for stronger protection.

## Change the PIN or update the questions

```
pip install openpyxl cryptography
python3 build.py "PRC_Geology_Board_Exam_Question_Bank_2.xlsx" 1212
```

Replace `1212` with any new PIN. `build.py` reads `template.html` and writes a fresh `index.html`.

## Progress

Progress is saved in the browser on each device. Use Settings → Export / Import to move it between your phone and computer.

## Question IDs

Each question's ID comes from its wording, so you can re-sort or renumber the sheet without breaking anyone's saved progress. Rewording a question gives it a fresh start. Keep `migrate_v1.json` next to `build.py`: it carries over progress saved before this ID scheme existed.
