# Create a New ADR — Workflow

## Step 1: Read the MADR spec

Read `references/spec/structured-madr-spec.md` to understand the full format before proceeding.

## Step 2: Determine the ADR storage directory

- Default: `docs/decisions/` relative to the user's working directory.
- If the directory does not exist and the user has not stated a preference, ask whether to use the default or a different location.

## Step 3: Determine the next sequence number

- List existing files matching `NNNN-*.md` in the target directory.
- Use the next available 4-digit number (e.g., `0001`, `0002`, …).
- If no files exist, start from `0001`.

## Step 4: Gather required information

Collect the following via conversation or `AskUserQuestion`:

| Field | Required | Notes |
|---|---|---|
| Title | Yes | Short phrase describing problem + solution. Pattern: `Use [X] for [Y]` |
| Context and Problem Statement | Yes | Background and why this decision is needed |
| Considered Options | Yes | All options actually evaluated (≥2 items) |
| Decision Outcome (chosen option + reason) | Yes | Which option was chosen and why |
| Status | Yes | Default: `accepted`. Values: `proposed`, `accepted`, `rejected`, `deprecated`, `superseded by ADR-XXXX` |
| Date | Yes | Default: today's date (YYYY-MM-DD) — use without asking |
| Decision Makers | Optional | Who made the decision |
| Consulted | Optional | Who was consulted (two-way communication) |
| Informed | Optional | Who is informed (one-way communication) |
| Decision Drivers | Optional | Constraints and quality requirements |
| Consequences | Optional (recommended) | Good/Bad/Neutral impacts of the chosen option |
| Confirmation | Optional (recommended) | How to verify the decision is implemented correctly |
| Pros and Cons of the Options | Optional | Detailed comparison per option |
| More Information | Optional | Links, related ADRs, review dates |

**Gathering guidelines:**

- Ask for title and problem statement first.
- Then ask for considered options and the chosen outcome.
- Offer to fill in optional sections (Consequences, Confirmation, Pros and Cons) — suggest including them, as they improve record quality.
- If the user doesn't specify a date, use today's date without asking.

## Step 5: Generate the filename

Pattern: `NNNN-title-with-dashes.md`

- Convert the title to lowercase.
- Replace spaces with hyphens.
- Remove or replace special characters with hyphens.
- Example: "Use PostgreSQL for relational data" → `0001-use-postgresql-for-relational-data.md`

## Step 6: Create the directory if needed

```bash
mkdir -p docs/decisions
```

## Step 7: Write the ADR file

Read `references/spec/adr-template.md` to get the template and template rules, then write the file.

Omit optional sections if no content was provided — never leave placeholder text.

## Step 8: Confirm to the user

Show the created file path and a brief content summary.
