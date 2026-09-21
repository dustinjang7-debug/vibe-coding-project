# PROMPTS.md: Living Prompt Pack

> Module 3 · Prompt Chaining. Re-architect the build with prompt chains; capture the reusable ones here.

## How to use this pack

_Each prompt is a reusable step. Chain them: the output of one becomes the input to the next._

## Prompt chain: Follow-up detail screen

### Step 1: Expand, build new screens in a strict sequence
```
Build the next phase of this app in a strict sequence:
1. Add a screen "Today". Match the layout and spacing of the attached "Today screen" screenshot.
2. Add a screen "Follow-up detail". Match the data density of the attached "Follow-up detail" screenshot.
3. Navigation: write the logic so "Today" links to "Follow-up detail".

Build these in order so "Today" is the anchor for "Follow-up detail".
```

### Step 2: Behavior, hard-code the states
```
Apply the following logic constraints to the Follow-up detail flow:

Use skeleton screens for the recent activity list loading state.
If no data is present, show the empty state: "No activity yet. Log the first touch to keep this follow-up moving."
On fetch failure, trigger the error state: "We couldn’t load this follow-up. Try again."
Maintain the same design language throughout and tether all behavior strictly to these rules.
```

### Step 3: Refine, one surgical polish
```
The Today Screeen needs a professional motivating polish.

Start by listing the 3 biggest gaps in typography and spacing compared to Customer.io.
Once you've identified those, resize the headers and advice me which to match.
Don't change anything else in the project or touch the underlying logic.
```

## Reusable techniques learned

- _____
- _____

## What broke (and the fix)

_Where a single mega-prompt failed and chaining fixed it._

_____
