# Change review exercise



## Prediction before review

I expect the diff to show an updated empty-notebook message in notes.js.



## Exercise setup

I also deliberately introduced a small stray edit in another file to check whether Claude would flag it.

## Claude's review

Summary of the changes

I made no changes, commits or pushes.

**Intended-looking: `notes.js` (line 22)**
- The empty-list message changed from `"No notes yet. Add one with: notes add <text>"` to `"Your notebook is empty. Add your first note with: notes add <text>"`.
- The command hint is unchanged, so the behaviour is the same and only the wording differs.
- This matches the prediction in `notes.md`.

**Likely unintended: `lib/config.js` (line 4)**
- `SESSION_TIMEOUT_MINUTES` changed from `15` to `150`.
- The comment says the session locks after this many minutes of inactivity, so the auto-lock window went from 15 minutes to 2.5 hours.
- That is a tenfold change to a security-relevant setting, and nothing in the diff or the file explains it. Check whether the value was meant to be 15 and whether it should be reverted before committing.

**Untracked: `notes.md`**
- This is a review-exercise file with a prediction about the `notes.js` change and a note that a stray edit was added to another file. That stray edit is the `config.js` change above.
- It is not source code and probably should not be committed with the feature changes.

## My reflection

Claude caught the deliberately introduced stray edit: SESSION_TIMEOUT_MINUTES changed from 15 to 150. It also correctly identified the intended wording change in notes.js. However, its suggestion to exclude notes.md conflicts with the assignment, which explicitly requires committing this file; its claim about actual auto-lock behaviour also needs verification, since the code shown only uses the setting in a displayed message.
