# Kitchen Share Nutrition Sheet — Weekly SOP

A reference for the full pipeline: describing a week's dishes → getting a finished
page → publishing it to lilavana.org/nutrition.

---

## Site structure (set once, don't touch again)

```
/ (repo root)
  index.html
  yields.html
  CNAME
  assets/images/
  nutrition/
    index.html          ← lilavana.org/nutrition — always THIS WEEK
    archive/
      index.html        ← lilavana.org/nutrition/archive — list of past weeks
      2026-07-21.html
      2026-07-14.html
      ...
```

GitHub Pages serves `index.html` automatically for any folder path, which is why
`/nutrition` and `/nutrition/archive` work with no filenames in the URL.

---

## What you need on hand

- **TEMPLATE.html** — the placeholder-driven page template (dish cards, photo
  upload buttons, styling). Never edit this file directly — always work from a copy.
- **Ingredient Database workbook** — your master per-100g nutrition reference.
  Only needed if this week includes an ingredient that isn't in it yet.
- The local folder path to your `lilavana.org` git repo. (currently C:\Users\yasit\LilavanaWebsite\Lilavana\nutrition)

---

## Weekly steps

### 1. Describe the week to Claude
In a chat, just talk through it naturally — dish name, what's in it, roughly how
much of each thing. No special format needed. Attach TEMPLATE.html if it's a new
chat. If an ingredient isn't in the database yet, Claude will flag it and ask for
its nutrition rather than guess.

### 2. Get the finished page back
Claude fills in the template's placeholders (calories, macros, the fixed
micronutrient order — Iron, Calcium, Magnesium, Potassium, Zinc, Vitamin A,
Vitamin C, Folate — and a gram-free ingredient list) and returns one finished
HTML file.

### 3. Add photos
Open the file in a browser. Click into each card's photo area and upload your
edited photo — it displays at full size, uncropped, no pre-formatting needed.
When all dishes have photos (or you're ready to skip any that don't), click
**"Download page with photos"** at the top. This saves a second, clean copy with
the upload buttons stripped out — that's the one that goes to members.

### 4. Archive last week, publish this week
From your repo folder, in order:

```bash
# 1. Move last week's page into the archive, dated for the week it covered
cp nutrition/index.html nutrition/archive/2026-07-21.html

# 2. Add the new week to the archive list
#    (Claude will give you the exact <li> line to paste into
#    nutrition/archive/index.html — add it to the top of the <ul class="weeks"> list)

# 3. Replace this week's page
cp ~/Downloads/kitchen_share_nutrition_week.html nutrition/index.html

# 4. Commit and push
git add -A
git commit -m "Nutrition: week of July 28"
git push
```

### 5. Share it
Add one line to that week's Stirrings email: *"This week's nutrition sheet:
lilavana.org/nutrition"* — no separate distribution needed since the URL is
permanent and always current.

---

## Fixed conventions (don't re-decide these each week)

- **File naming:** `YYYY-MM-DD.html`, dated for the week the sheet covers.
- **Micronutrient order, every card, always:** Iron, Calcium, Magnesium,
  Potassium, Zinc, Vitamin A, Vitamin C, Folate.
- **Ingredient notes:** plain ingredient names, no gram amounts.
- **Macro order:** Protein, Carbs, Fat, Fiber.
- **Sanity check on any dish's numbers:** Calories ≈ (Protein × 4) + (Net Carbs
  × 4, where Net Carbs = Carbs − Fiber) + (Fiber × 2) + (Fat × 9). Within ~5–8%
  is normal; bigger gaps mean a macro entry is off.

---

## Troubleshooting

- **Forgot to archive before overwriting `nutrition/index.html`?** Check `git
  log` for the previous commit — the old version is recoverable with `git show
  <commit-hash>:nutrition/index.html > nutrition/archive/YYYY-MM-DD.html`.
- **New ingredient not in the database?** Give Claude its nutrition (or ask
  Claude to look it up) and add it as a new row in the Ingredient Database
  workbook so it's there permanently next time.
- **Page looks broken after editing the template?** Check that every
  `{{PLACEHOLDER}}` got filled in and that opening/closing `<div>` tags still
  match — an unclosed dish block is the most common cause.
