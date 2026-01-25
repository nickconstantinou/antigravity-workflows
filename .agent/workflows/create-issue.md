---
description: Create Issue Workflow
---

---
description: Create Issue Workflow
---

User is mid-development and needs to capture a bug, feature, or improvement without breaking flow.

## Your Goal
Generate a structured, ready-to-submit issue ticket.

## Phase 1: Rapid Context Gathering
**Ask questions** to fill gaps. Be concise. Respect the user's time.
- **What:** What is the specific bug/feature?
- **Why:** What is the desired behavior vs. current reality?
- **Where:** Which specific files or UI components are involved?
- **Priority:** Impact level (Low/Medium/High/Critical).

**Rules:**
- ⚡️ **Max 2 minutes:** Keep the exchange short.
- 🚫 **No Checklists:** Ask conversational questions.
- 🔍 **Smart Context:** Briefly grep the codebase to find the likely file paths if the user describes a specific component. Do not perform deep research yet.

## Phase 2: Output
Once you have the details, output the issue in this exact format:

---
**Title:** [Type]: [Concise Description]
**Labels:** `[bug/feature/refactor]`, `[priority]`, `[effort]`

### 📝 TL;DR
One sentence summary of what this is.

### 🐛 Current Behavior vs. 🎯 Expected Behavior
* **Current:** [What is happening]
* **Expected:** [What should happen]

### 📂 Relevant Files
- `path/to/file.ts`
- `path/to/component.tsx`

### 🛠 Proposed Solution / Notes
Brief technical notes or implementation ideas gathered during the chat.
...

## Phase 3: Action
Don't just output the text. **Create a new file** in `docs/issues/open/` (create the folder if it doesn't exist).
* **Filename:** `YYYY-MM-DD-[kebab-case-title].md`
* **Content:** The markdown issue content generated above.

After creating the file, output: "✅ Issue saved to `[filepath]`"