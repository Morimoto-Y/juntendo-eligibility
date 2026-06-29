# Juntendo University — Graduate Eligibility Check
## Maintenance Manual

This tool provides a preliminary eligibility check for prospective international graduate students applying to Juntendo University's Master's or Doctoral programs.

**Live URL:** https://juntendo-eligibility.pages.dev
**GitHub:** https://github.com/Morimoto-Y/juntendo-eligibility
**Contact (Admissions):** gsm_nyushi@juntendo.ac.jp

---

## 1. System Overview

### What this tool does
A step-by-step web form that checks whether an international applicant appears to meet the basic eligibility requirements for Juntendo's graduate programs. It is a **preliminary check only** — official eligibility is determined by the Graduate Admissions Office.

### What it checks
1. **Academic background** — years of schooling and degree type
2. **English language proficiency** — English test scores (TOEFL/IELTS/TOEIC)

### Judgment results
| Result | Meaning |
|--------|---------|
| **Qualified** | Appears to meet requirements |
| **Need confirmation** | Requires individual review by admissions office |
| **Not qualified** | Does not appear to meet requirements |

### Doctoral program: two result blocks
When the Doctoral program is selected, the results page displays **two separate result blocks**:
- **Graduate School of Medicine** — uses doctoral (Medicine) thresholds
- **Graduate School of Nursing** — uses doctoral (Nursing) thresholds (same as Master's)

Each block shows Academic background and Language proficiency results independently.

### Important limitations
- Does not check nationality or visa status (handled separately by admissions)
- Does not verify actual documents
- Application deadline dates are intentionally excluded (they change annually)
- Results are non-binding
- The Overall Assessment verdict is not displayed; only individual check results are shown
- The line "This is a preliminary indication only. Official eligibility is determined by the Graduate Admissions Office." appears at the bottom of the results page

---

## 2. File Structure

The entire application is a **single file**: `index.html`

There are no frameworks, build tools, or external dependencies. The file contains:
- HTML structure
- CSS styles (embedded in `<style>` tag)
- All application logic (embedded in `<script>` tag)

---

## 3. Eligibility Logic Reference

### Academic requirements

| Program | Minimum total years |
|---------|-------------------|
| Master's | 16 years |
| Doctoral | 17 years |

**Year counting:** Elementary + Middle + High school + Undergraduate (+ Graduate if applicable)

**Pre-university minimum:** Elementary + Middle + High school combined must total at least 12 years.

**Undergraduate minimums by degree type:**

| Degree selected | Min. undergraduate years |
|----------------|--------------------------|
| 4-year Bachelor's | 4 years |
| 3-year Bachelor's | 3 years |
| 5-year medical degree (e.g. MBBS/MBChB) | 5 years |
| 6-year medical/dental/pharmacy/veterinary | 6 years |
| Master's degree (doctoral applicants) | 3 years (undergraduate) + 2 years (graduate) |

**3-year Bachelor's degree (Master's program only):**
If total effective years fall below 16, the judgment returns **Need confirmation** rather than Not qualified, as some programs may accept this background. Applicants are advised to contact the admissions office directly.

**Leave of absence:** Entered in months and subtracted from total years before judgment.

**Grade skipping / early admission:** If years fall short, a note is displayed advising applicants to disclose this in their formal application.

**Special cases:**
- `research` (Bachelor's + 2+ years research): Always → Need confirmation
- `other`: Always → Need confirmation

### Additional post-graduate study (optional field)
An optional input field appears to the right of the Undergraduate input on Step 3, for all degree types **except** Doctoral + Master's degree (which already has a graduate years field).

This field accepts years spent in post-graduate programs such as postgraduate diplomas, research programs, or bridging courses.

- The value is **added to the Total years display** and shown on the results page
- It does **NOT affect** the Qualified / Need confirmation / Not qualified judgment
- Purpose: allows applicants to accurately represent their total years of education

### Language requirements

| Test | Master's minimum | Doctoral (Medicine) minimum | Doctoral (Nursing) minimum |
|------|-----------------|----------------------------|---------------------------|
| TOEFL iBT | 60 | 76 | 60 |
| TOEFL PBT/ITP | 500 | 540 | 500 |
| IELTS | 5.5 | 6.0 | 5.5 |
| TOEIC | 600 | 700 | 600 |

When Doctoral is selected, Step 5 displays both Med and Nurs thresholds for each test. The results page shows two separate Language proficiency blocks (Graduate School of Medicine and Graduate School of Nursing).

**Score validity:** August 1, 2020 or later only.
**TOEFL My Best™ scores:** Not accepted. A note is shown to qualified TOEFL iBT applicants as a reminder.

---

## 4. How to Make Common Updates

### Prerequisites
- Terminal access (Mac: open Terminal app)
- Claude Code installed (`claude --version` to verify)

### Starting a work session
```
cd ~/juntendo-eligibility
claude
```

Then type your instruction in Japanese or English.

---

### Common update examples

**A. Change a language score threshold**

Example prompt to Claude Code:
```
index.htmlのTOEFL iBTの修士課程の最低スコアを60から65に変更してください。
変更後、git add . && git commit -m "update: TOEFL iBT master threshold to 65" && git push を実行してください。
```

**B. Change the admissions email address**

Example prompt:
```
index.htmlの教務課のメールアドレスをgsm_nyushi@juntendo.ac.jpから
新しいアドレスに変更してください。
変更後、git add . && git commit -m "update: admissions email address" && git push を実行してください。
```

**C. Add a new degree type**

Example prompt:
```
index.htmlの修士課程の学位選択肢に「2-year Associate degree」を追加してください。
この学位は修学年数が2年以上であればOKとします。
変更後、git add . && git commit -m "feat: add associate degree option" && git push を実行してください。
```

**D. Change the language score validity cutoff date**

Example prompt:
```
index.htmlの語学スコアの有効期限の基準日を2020-08-01から2022-04-01に変更してください。
変更後、git add . && git commit -m "update: language score validity date" && git push を実行してください。
```

**E. Update the contact message on the results page**

Example prompt:
```
index.htmlの結果画面の連絡先説明文を変更してください。
現在: "Please prepare copies of your academic transcript, diploma, and language test certificate."
変更後: "（新しいテキスト）"
変更後、git add . && git commit -m "update: contact note text" && git push を実行してください。
```

**F. Update doctoral Nursing language thresholds**

Example prompt:
```
index.htmlの看護博士課程の語学スコアの最低基準を変更してください。
TOEFL iBT: 60 → （新しいスコア）
変更後、git add . && git commit -m "update: nursing doctoral lang threshold" && git push を実行してください。
```

**G. Change the judgment for 3-year Bachelor's (Master's program)**

Example prompt:
```
index.htmlで、修士課程・3年制学士の場合に合計年数が16年未満の場合の
判定を変更してください。
現在: Need confirmation
変更後: （新しい判定）
変更後、git add . && git commit -m "fix: 3-year bachelor master judgment" && git push を実行してください。
```

**H. Update the optional post-graduate study field behavior**

Example prompt:
```
index.htmlのAdditional post-graduate study (optional)フィールドについて、
現在は合計年数の表示にのみ使用されています。
このフィールドの扱いを変更してください：（変更内容を記述）
変更後、git add . && git commit -m "update: post-graduate study field behavior" && git push を実行してください。
```

---

## 5. Deployment

After running `git push`, Cloudflare Pages automatically detects the change and redeploys within 1–2 minutes.

To verify deployment: https://juntendo-eligibility.pages.dev

No manual deployment action is needed.

---

## 6. Sharing with the International Office Account

When ready to share repository access with the international office's shared GitHub account:

1. Go to https://github.com/Morimoto-Y/juntendo-eligibility/settings/access
2. Click **Add people**
3. Enter the shared account's GitHub username
4. Set role to **Write** (allows pushing changes) or **Maintainer**
5. Click **Add to repository**

For Cloudflare Pages sharing, add the shared account as a member of your Cloudflare account at https://dash.cloudflare.com/profile/members.

---

## 7. Key Variables in the Code

For reference when asking Claude Code to make changes:

| Variable | Location | Purpose |
|----------|----------|---------|
| `MIN_YEARS` | top of script | Minimum total years per program |
| `DEGREE_OPTS` | top of script | Degree options shown in Step 2 |
| `LANG_MIN` | top of script | Language score thresholds (Master's and Doctoral Medicine) |
| `LANG_MIN_NURS_DR` | top of script | Language score thresholds for Doctoral Nursing |
| `judgeAcademic()` | function | Academic background judgment logic |
| `judgeLang()` | function | Language proficiency judgment logic |
| `ugMinYears()` | function | Minimum undergraduate years by degree type |

---

## 8. Important Notes for AI-Assisted Updates

When asking Claude Code (or any AI) to modify this file:

- Always specify the **exact text to change** when possible
- Always include the git commit and push command in your request
- After pushing, wait 1–2 minutes and verify at the live URL
- If something breaks, Claude Code can revert: `git revert HEAD && git push`
- The entire app logic is in one file (`index.html`) — no other files need to be changed for most updates

---

*Last updated: June 2026*
