# Lilavana / Kitchen Share — Website TODO

## Open

### Redo the site architecture
- [ ] Decide on the final structure — two options on the table:
  - **A. Nested:** everything under `/kitchen-share/` (`kitchen-share/index.html`, `kitchen-share/products/`, `kitchen-share/nutrition/`) — makes the URL itself signal "you're in this project," sets up cleanly for future Lilavana projects with their own namespace
  - **B. Flat (current):** `kitchen-share.html` at root just links out to `/yields` and `/nutrition` where they already live — zero file moves, lower risk
- [ ] If going with A: `git mv yields.html kitchen-share/products/index.html`
- [ ] If going with A: `git mv nutrition/ kitchen-share/nutrition/`
- [ ] If going with A: update every internal link across `index.html`, `kitchen-share.html`, and the nutrition/archive pages to the new paths
- [ ] If going with A: update the link already sent out in Stirrings emails pointing to `/nutrition`
- [ ] Either way: confirm GitHub Pages is serving the right `index.html` for each folder path after the change

### Finish the /nutrition current-week + archive setup
- [ ] Commit `nutrition/archive/index.html` (built, not yet pushed)
- [ ] Confirm `nutrition/index.html` is the "always overwritten with current week" file going forward
- [ ] Archive past weeks into `nutrition/archive/` as each new week goes up (`cp` the outgoing week before overwriting)
- [ ] Add `nutrition/SOP.md` to the repo
- [ ] Update the SOP to reference the `nutrition/source/` folder (TEMPLATE + ingredient database)
- [ ] Double check `TEMPLATE.html` and `kitchen_share_nutrition_database.xlsx` actually made it into `nutrition/source/` after the earlier merge conflict — confirm with `git log` / a look at GitHub

### Publish the Kitchen Share hub page
- [ ] Decide how to design the `kitchen-share.html` landing page.
- [ ] Add `kitchen-share.html` to the repo (root, or wherever the architecture decision above lands it)
- [ ] Replace `index.html` with the updated nav version (single "Kitchen Share →" link)
- [ ] Read through the hero/how-it-works copy once more for voice before it goes live
- [ ] Commit + push

### Set up the nutrition-sheet pipeline (separate chat)
- [ ] Start the dedicated pipeline chat (prompt already drafted, saved from earlier)
- [ ] Give it the repo's local folder path
- [ ] Decide nutrition sheet file naming/organization convention
- [ ] Walk through one full example end to end to confirm it works

## Done
- [x] Nutrition Sheet Excel workbook + Ingredient Database (reusable, linked via INDEX/MATCH)
- [x] Member-facing nutrition sheet HTML (photo upload, clean client-facing download)
- [x] `TEMPLATE.html` for future weekly sheets
- [x] Kitchen Share hub page — full-bleed alternating green boxes, scroll fade-in
- [x] Root `index.html` nav simplified to point to Kitchen Share hub
