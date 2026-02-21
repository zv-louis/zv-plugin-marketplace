# Update ADR Status — Workflow

## Step 1: Identify the target ADR

Determine which ADR to update from the user's request:

- By number: find the file with the matching `NNNN-` prefix in `docs/decisions/`
- By name or partial title: search for a matching filename
- If ambiguous, list candidates and ask the user to confirm

## Step 2: Show the current state

Read the target file and display:

- Filename
- Current `status` value
- Current `date` value

## Step 3: Determine the new status

If the user has not specified the new status, ask. Valid values:

| Value | Meaning |
|---|---|
| `proposed` | Under discussion, not yet decided |
| `accepted` | Agreed and in effect |
| `rejected` | Evaluated and not adopted |
| `deprecated` | Was valid but is no longer recommended |
| `superseded by ADR-XXXX` | Replaced by another ADR (specify the number) |

## Step 4: Apply the update

Edit the `status` field in the YAML front matter of the target file.

```yaml
# Before
status: "proposed"

# After
status: "accepted"
```

If the new status is `superseded by ADR-XXXX`:
- Set `status: "superseded by ADR-XXXX"` (replace XXXX with the actual number).
- Append a note in the `More Information` section referencing the superseding ADR. If the section does not exist, add it:

  ```markdown
  ## More Information

  * Superseded by [ADR-XXXX](NNNN-title-of-superseding-adr.md)
  ```

## Step 5: Confirm to the user

Show the updated file path and the new status value.

**Important:** Never delete or truncate the ADR. Status updates are the only change — all other content must be preserved.
