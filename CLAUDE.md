# CLAUDE.md

This file is the **entire GHL AI CRM agent**. It is both the operating manual and the account inventory. The GHL MCP server is the execution layer; this file is the brain.

---

## Workspace & Git

Workspace remote: `https://github.com/Asyrafazmi-code/claude-code-projects.git` (account: `Asyrafazmi-code`).

Use `gh repo` commands for GitHub operations (already permitted in `.claude/settings.local.json`). Commit and push regularly throughout work — after any meaningful unit (feature, fix, refactor, config change). Commit messages must be clear and descriptive.

---

## What this system is

**Vertical:** Insurance CRM — specifically **US life insurance agents**.
**Operator:** An agency that builds growth systems for those agents and manages **15–19 GHL sub-accounts** (one per agent/client). This file is a **template**: it will be cloned per sub-account, and the account-specific values re-filled each time. See the **Template Migration Notes** section at the bottom.

---

## My account inventory `[ACCOUNT-SPECIFIC]`

### Location

- **locationId:** `j93PgN0y2XIwW4Kv22Ch` `[ACCOUNT-SPECIFIC]`
- **Name:** LeadsbyHammad Test `[ACCOUNT-SPECIFIC]`
- **companyId:** `AEVHDnXKbRgY3KHXXCnP` `[ACCOUNT-SPECIFIC]`
- **Address:** 1348 Ridgeview Cir 1403, Davenport, FL 33896, US `[ACCOUNT-SPECIFIC]`
- **Website:** leadsbyhammad.com `[ACCOUNT-SPECIFIC]`
- **Timezone:** America/Bogota `[ACCOUNT-SPECIFIC]`
- **Currency:** USD `[ACCOUNT-SPECIFIC]`
- **Owner contact:** jack frost · support@leadsbyhammad.com `[ACCOUNT-SPECIFIC]`
- Created 2026-02-05. Not an agency sub-account. SaaS mode: not activated.

### Pipelines

**Pipeline A — `1. Sales Pipeline`** (AUTHORITATIVE sales pipeline) · id `VkRDTiLsuzq3rEilyzBx` `[ACCOUNT-SPECIFIC]`

| Pos | Stage Name | Stage ID | Win % | Semantic role |
|---|---|---|---|---|
| 0 | New Lead | `6f62d31c-105d-48ad-8658-fcca7c1b5051` | 11.11 | intake |
| 1 | Engaged Lead | `8e90a7ac-40a5-4cbb-a8da-a8b30fbaaba1` | 22.22 | **qualified target** |
| 2 | No Show | `0ee385aa-1a60-4044-b5f1-5a540e9eed6b` | 33.33 | recovery |
| 3 | Strategy Session Booked | `8db5f8f2-edf6-4a71-83a9-9c163115c606` | 44.44 | appt booked |
| 4 | Follow Up Call Booked | `9062fdd2-8203-4f9a-9395-75b904e81296` | 55.56 | appt booked |
| 5 | Deal Follow-Up | `3769f80e-091c-4895-89e0-4b96fbcd4dbe` | 66.67 | post-appt |
| 6 | Deposit Taken | `c71769f2-9a92-4afd-95e4-1c3f3947950a` | 77.78 | near-close |
| 7 | Deal Closed | `501b9948-c928-4c5e-92bb-d2d52237eb20` | 88.89 | **CLOSED — no action** |

**Pipeline B — `2. Hiring Pipeline`** · id `WIn75QyZ0zJcqvutnA6O` `[ACCOUNT-SPECIFIC]`
Internal recruiting, NOT customer-facing. Agent should never message contacts in this pipeline.

| Pos | Stage Name | Stage ID | Win % |
|---|---|---|---|
| 0 | ✍️ 1. Applied | `e5f4cc38-4fb9-4e12-9418-0bb66e909235` | 14.29 |
| 1 | 👀 2. In Review | `9a0e958f-8559-4b4a-81b9-183947cfa5ac` | 28.57 |
| 2 | 📧 3. Contacted | `b2615474-4c4f-4028-9fb7-725ce8fd4739` | 42.86 |
| 3 | 🧐 4. Interviewed | `f02bc0f5-a5a6-447d-869e-722ca83b245f` | 57.14 |
| 4 | ✅ 5. Hired | `eb74ac25-1aa3-4f45-aee9-a88967c6c8ab` | 71.43 **CLOSED** |
| 5 | ❌ 6. Not Hired | `b69d4914-6172-47ca-9a47-3d27c0ea60b7` | 85.71 **CLOSED** |

**Pipeline C — `3. Onboarding`** · id `7Ujr5sCxA3SW4gBbFbi2` `[ACCOUNT-SPECIFIC]`
Post-sale client lifecycle. Agent should never send **sales** outreach to contacts here.

| Pos | Stage Name | Stage ID | Win % |
|---|---|---|---|
| 0 | Client | `cd4a7b4c-f80d-4566-94be-cdfbfdf6de42` | 12.5 |
| 1 | Payment & Agreement Completed | `43afdff8-9cde-46a5-83a2-0ec3546b6f6c` | 25 |
| 2 | Launch Call Completed | `45273daa-36ea-4e30-b87e-d0f906c18f55` | 37.5 |
| 3 | Live | `c11586c0-a666-4489-9560-00cccda729ca` | 50 |
| 4 | 30 Day Check-In | `47eb6299-0c7d-474c-bde0-9f5c28c394a4` | 62.5 |
| 5 | 60 Day Check-In | `181dcc2e-85b2-4a70-a298-bc6f156bc6b0` | 75 |
| 6 | 90 Day Check-In | `fe8ec1d8-6a5e-481d-92b5-632750ee0709` | 87.5 |

**Pipeline D — `Sales Pipeline`** (LEGACY — DO NOT TOUCH) · id `HeLZbkXpE6p69uPwJnRO` `[ACCOUNT-SPECIFIC]`
Created 2026-02-12, superseded by Pipeline A on 2026-03-20. **Never tag, message, or move contacts in this pipeline.** If you see activity here, flag it to the human operator. Left listed so the agent recognizes it and can correctly refuse to act.

### Custom fields (all `model: contact` — there are ZERO opportunity custom fields in this account)

⚠️ **Structural note for all sub-accounts in this vertical:** deal/payment data lives on the *contact*, not the opportunity. Do not write rules that read or write opportunity custom fields.

All field IDs below are `[ACCOUNT-SPECIFIC]`.

**Deal / Payment group** (`parentId: AgCGblr4VpZmZMrwmAtr`)
| Field Name | Field Key | Data Type | Field ID |
|---|---|---|---|
| Sign-Up Date | `contact.signup_date` | DATE | `5ZUrUurSRbt3P7OpD2Tm` |
| Deal Program | `contact.deal_program` | SINGLE_OPTIONS | `e4K1wl9OIZ63rpT5A9Sy` |
| Total Deal Value | `contact.total_deal_value` | MONETORY | `xRs6QW36IqNfp2MbRZ0J` |
| Upfront Payment | `contact.upfront_payment` | MONETORY | `O9wlolI6mHPOCIXf6hpb` |
| Currency | `contact.currency` | SINGLE_OPTIONS | `NoEXBMfnBOI8CvQZHJaE` |
| Payment Method | `contact.payment_method` | SINGLE_OPTIONS | `GVGI8CHbtp4QEHGWODTn` |
| Payment Plan | `contact.payment_plan` | SINGLE_OPTIONS | `yWV4ESXsWotywAkLXv20` |
| Additional Deal Notes | `contact.additional_deal_notes` | LARGE_TEXT | `RXDtlmb2nFonQE0kmhbf` |
| Customer's Main Obstacle | `contact.customers_main_obstacle` | LARGE_TEXT | `EccMetoOF6uOXwqUcS7Q` |
| Reason of Purchase | `contact.reason_of_purchase` | LARGE_TEXT | `st1iXqmJUSjPVwbt6f2I` |
| Sales Angle Used | `contact.sales_angle_used` | LARGE_TEXT | `M5LodYzkUsD8ZZxKdWKq` |
| Installment-2 Amount | `contact.installment2_amount` | MONETORY | `jHfm81zXMArLwt2QoiAO` |
| Instalment-2 Due Date | `contact.instalment2_due_date` | DATE | `uCbVZUArDKJGIvmU8KAC` |
| Installment-3 Amount | `contact.installment3_amount` | MONETORY | `1NtN3yVvPVlAZZk0o0h7` |
| Installment-3 Due Date | `contact.installment3_due_date` | DATE | `2Lluw8SJOI0JCgiMpmWz` |
| Installment-4 Amount | `contact.installment4_amount` | MONETORY | `m8ePXDico32mRCdvadCv` |
| Installment-4 Due Date | `contact.installment4_due_date` | DATE | `giRxewGaWDILSN5LyfM1` |
| Installment-5 Amount | `contact.installment5_amount` | MONETORY | `AJAC2wcrOvNBcRYJlkch` |
| Installment-5 Due Date | `contact.installment5_due_date` | DATE | `AVEeICHLtdWXlkRmGdYt` |
| Installment-6 Amount | `contact.installment6_amount` | MONETORY | `u3ZKwGmYHhlecNKrwT21` |
| Installment-6 Due Date | `contact.installment6_due_date` | DATE | `F9dZCksHRutawCBAGytA` |

**Business / Appointment metadata group** (`parentId: XJh8aiEEYU35VKFva2DR`)
| Field Name | Field Key | Data Type | Field ID |
|---|---|---|---|
| Sales Rep | `contact.sales_rep` | TEXT | `0bmrhW7pyclgRQ3gAfis` |
| Business Goals | `contact.what_are_your_top_23_business_goals_for_the_next_36_months` | LARGE_TEXT | `1hn4yi23E3WkbnszO0k2` |
| Offer/Product/Service | `contact.offerproductservice` | LARGE_TEXT | `fgPiugEZxtXDRKmKf1fh` |
| Ideal Customer | `contact.ideal_customer` | LARGE_TEXT | `XPRK8qcQTW0B7tiZR0nF` |
| Unique Selling Point | `contact.unique_selling_point` | LARGE_TEXT | `E4P0aNZrvxAstYtAFBuK` |
| Marketing Channel | `contact.marketing_channel` | LARGE_TEXT | `uYcahh0O25cMDyjC9Rxm` |
| Monthly Marketing Budget | `contact.monthly_marketing_budget` | MONETORY | `QCHe9n8WrrIqXW18pBsO` |
| Additional Team Members/Partners | `contact.additional_team_memberspartners` | LARGE_TEXT | `P3exkxh3SpwrtTBYpmWJ` |
| Appointment \| Calendar Name | `contact.appointment__calendar_name` | TEXT | `J8Lff3V7a9ERUzjCdIbo` |
| Appointment \| Date & Time | `contact.appointment__date__time` | TEXT | `UoH0bJc5HvIp9XMluS4n` |
| Appointment \| Booking Count | `contact.appointment_count` | NUMERICAL | `LcDVjA9pmqLKHURogMRN` |
| Appointment \| Reschedule Count | `contact.reschedule_count` | NUMERICAL | `lnw0AkupMz7zl5f5OERA` |
| Appointment \| No Show Count | `contact.no_show_count` | NUMERICAL | `a5A5Yx754i1JAt9Rr52x` |

**Onboarding Questions group** (`parentId: Y3ABRtE5Lowt4UKmXH3e`)
Field names here contain smart quotes (U+2019 `'`). Reference them verbatim — do not substitute straight quotes.

| Field Name (verbatim) | Field Key | Data Type | Field ID |
|---|---|---|---|
| What's working well for you right now? | `contact.whats_working_well_for_you_right_now` | LARGE_TEXT | `x62mhEEvJwiGyqAJcCLg` |
| What isn't working, or what would you like to stop doing? | `contact.what_isnt_working_or_what_would_you_like_to_stop_doing` | LARGE_TEXT | `ydUFgzWwmzG7RzbWBZQt` |
| Is there anything else we should know that hasn't been covered already? | `contact.is_there_anything_else_we_should_know_that_hasnt_been_covered_already` | LARGE_TEXT | `38SnJUxtLWOQ4lDl4y4q` |
| Do you have any compliance/regulation concerns we should know about? | `contact.do_you_have_any_compliance_regulation_concerns_we_should_know_about` | LARGE_TEXT | `v9kNxKbDtx9vTQL4FGln` |
| GDrive Shared Folder URL | `contact.gdrive_shared_folder_url` | TEXT | `uOiEHLJ02UxvouTcGzCI` |

**Contact basics group** (`parentId: B7Pj2fPpXD9f0yqveZ3d`)
| Field Name | Field Key | Data Type | Field ID |
|---|---|---|---|
| Business Name | `contact.business_name` | TEXT | `MaSpJaYsIV1LW2rrS5HR` |
| Rescheduled Date | `contact.rescheduled_date` | DATE | `jCRWWgqNHgjr4eB1Y1cH` |

**Appointment detail group** (`parentId: b4P6fia3Zu7yuoq8fde3`)
| Field Name | Field Key | Data Type | Field ID |
|---|---|---|---|
| ID | `contact.id` | TEXT | `VMexBP2ZC4SjBhtwh6tP` |
| Appointment \| Meeting location (link) | `contact.appointment__meeting_location_link` | TEXT | `fFh3aHbQtIcawBzdF2gO` |
| Appointment \| Add to GCal | `contact.appointment__add_to_gcal` | TEXT | `hEux5anV6crN9H8C4CBH` |

**Insurance qualifier group** (`parentId: okAeVebfyL7LWnxfFq7v`) — **the core qualification inputs**

| Field Name | Field Key | Data Type | Field ID | Picklist |
|---|---|---|---|---|
| How Much Coverage Do You Need? | `contact.how_much_coverage_do_you_need` | MULTIPLE_OPTIONS | `vcIddL5etIeOwPgE3wav` | `$10k-$50k` / `$50k-$100k` / `$100k-$500k` / `$500k+` / `Not Sure` |
| Age (note trailing space in display name) | `contact.age_1` | MULTIPLE_OPTIONS | `EMOPV3ntINbQyE6iST86` | `Under 18` / `18-25` / `26-35` / `36-45` / `46-55` / `56-65` / `66-75` / `76+` |

### Tags — TODO

Tag inventory was not enumerated in Phase 1 discovery. Before going live, list existing tags (via any recent contact record and/or ask the operator) and paste them here. Until then, when the agent applies a tag it MUST use a name from the **Agent-authored tag vocabulary** below.

### Calendars — TODO

MCP tooling does not expose a "list calendars" endpoint. Calendar IDs must be pasted here manually from the GHL UI (Calendars → Calendar Settings → URL contains the ID). The Phase 3 lead intake & qualification MVP does not strictly require calendars; fill in before Phase 4 autopilot that schedules.

Expected template shape (fill per sub-account):
- Demo/Strategy Session calendar: `[TBD]` `[ACCOUNT-SPECIFIC]`
- Follow-Up Call calendar: `[TBD]` `[ACCOUNT-SPECIFIC]`

---

## MCP Field-Access Patterns

Discovered empirically during Phase 3 seed-contact creation. These are MCP-server behaviors, not visible in the tool schemas — document here so the agent doesn't re-learn them on every sub-account.

### Write path (setting custom field values)

Use `mcp__ghl-mcp__contacts_update-contact`. The `body_customFields` parameter takes an **array of raw JSON object literals**, despite the MCP schema declaring `items: string`:

```
body_customFields: [
  {"id": "<fieldId>", "field_value": "<value>"},
  {"id": "<fieldId>", "field_value": "<value>"}
]
```

- Key is `field_value` (singular, scalar).
- Do NOT stringify the objects. The server accepts raw object literals; stringified JSON is silently dropped.

### Read path (getting custom field values)

Use `mcp__ghl-mcp__contacts_get-contact`. The response returns `customFields` with a **different shape than the write payload**:

```
"customFields": [
  {"id": "<fieldId>", "value": ["<value>"]}
]
```

- Key is `value` (NOT `field_value`).
- `MULTIPLE_OPTIONS` fields (e.g. Age `EMOPV3ntINbQyE6iST86`, Coverage `vcIddL5etIeOwPgE3wav`) return **arrays** even when only one option is selected.
- **Always unwrap:** `customFields[n].value[0]`.
- A field that was never set is **absent from the `customFields` array entirely** — not present with an empty value. Treat "field absent" as equivalent to "value is empty".

### Create limitation

`mcp__ghl-mcp__contacts_create-contact` **silently drops** `body_customFields` at create time, regardless of shape. Do NOT attempt to set custom fields at create. Required pattern:

1. `contacts_create-contact` — standard fields only (name, email, phone, tags, source, country).
2. Capture the returned `contactId`.
3. `contacts_update-contact` with `path_contactId` + `body_customFields` in the write shape above.

### Opportunity limitation

There is **no `opportunities_create-opportunity` tool** in the GHL MCP surface. Available opportunity tools: `get-opportunity`, `get-pipelines`, `search-opportunity`, `update-opportunity`.

**Implication:** the agent cannot place a contact into a pipeline stage via MCP. When the Phase 3 workflow requires a contact to be in `New Lead` of Pipeline A, opportunity creation must happen out-of-band — either manually in the GHL UI, or via a GHL automation workflow (e.g., "on contact tag `seed-test` added, create opportunity in Pipeline A / New Lead").

---

## Safety rules (HARD — agent MUST NOT violate without explicit human override in chat)

1. **Never delete** a contact, opportunity, pipeline, stage, tag, custom field, or calendar.
2. **Never send outbound messages to more than 1 recipient** in a single operation without explicit human confirmation in chat. Bulk = ask first.
3. **Never modify contacts in closed stages.** Closed = `Deal Closed` (Pipeline A), `✅ 5. Hired` / `❌ 6. Not Hired` (Pipeline B). No tagging, no messaging, no stage moves, no field writes.
4. **Never touch Pipeline D (`Sales Pipeline`, legacy).** Read-only. Flag any activity there to the operator.
5. **Never send sales outreach to contacts in Pipeline C (`3. Onboarding`).** They are existing clients. Lifecycle/retention messaging only, and even then notify the operator first.
6. **Never message contacts in Pipeline B (`2. Hiring Pipeline`).** Candidates, not customers.
7. **Never write to opportunity custom fields.** None exist; any attempt means the rule was wrong.
8. **Never move a contact into `Deal Closed`, `Deposit Taken`, or `Launch Call Completed` automatically.** These require human confirmation — they have revenue/operational consequences.
9. **Never store, log, or transmit** full payment card numbers, SSNs, or full policy numbers. Last 4 only if needed for reference.
10. **Insurance compliance:** Never state or imply coverage approval, policy pricing, premium guarantees, or eligibility conclusions. Those are the licensed agent's job. The AI qualifies interest; the human writes the policy.

---

## Conventions

- **"lead pipeline" / "sales pipeline"** → Pipeline A (`1. Sales Pipeline`, id `VkRDTiLsuzq3rEilyzBx`). Never Pipeline D.
- **"engaged lead stage"** → `8e90a7ac-40a5-4cbb-a8da-a8b30fbaaba1` in Pipeline A.
- **"new lead stage"** → `6f62d31c-105d-48ad-8658-fcca7c1b5051` in Pipeline A.
- **"onboarding"** → Pipeline C (`3. Onboarding`).
- **"hiring"** → Pipeline B (`2. Hiring Pipeline`).
- **Tag naming convention:** lowercase, kebab-case, ASCII only. Max ~40 chars. Verb-noun or attribute-noun (e.g. `qualified-lead`, `needs-qualification`, `minor-ineligible`).
- **Currency:** all monetary references in USD unless the contact's `contact.currency` field says otherwise.
- **Dates:** ISO 8601 (YYYY-MM-DD) in agent output. GHL stores as it stores.
- **Timezone:** America/Bogota for scheduling math on this sub-account.
- **Smart quotes:** field names with `'` (U+2019) must be referenced verbatim.

---

## Agent-authored tag vocabulary

These are tags the agent may apply. If a tag is not in this list and not in the (TODO) existing tag inventory, DO NOT invent one — ask the operator.

- `needs-qualification` — contact is missing one or both qualifier fields (Age or Coverage), OR Coverage = `Not Sure`. Operator must follow up.
- `qualified-lead` — both qualifiers present and valid (see Phase 3 workflow below).
- `minor-ineligible` — Age = `Under 18`. Life insurance purchase is not legally available; contact should be routed to manual review, NOT moved through sales stages.
- `senior-specialty` — Age = `76+`, requires specialty product path — routes to licensed agent, not standard sales flow.
- `coverage-high-value` — Coverage = `$500k+`. High-ticket; operator may want priority follow-up.
- `calendar-conflict` — booking attempt surfaced an overlap or timezone mismatch. Human-review required.
- `rescheduled` — appointment moved at least once (paired with the `Rescheduled Date` field).

---

## Tiered autonomy

| Tier | Action category | Autonomy |
|---|---|---|
| **Auto** | Reads of any kind (contacts, opportunities, conversations, appointments, calendars, fields, tags, pipelines). Tag additions from the agent-authored tag vocabulary above, on contacts NOT in a closed stage and NOT in Pipeline D. Adding internal notes / tasks visible only to the operator. | Execute, log, report result. |
| **Notify** | Outbound message send (1 recipient). Pipeline stage move within Pipeline A only, forward-only (no regressions past `New Lead`), never into `Deal Closed` / `Deposit Taken`. Writing to non-payment contact custom fields. Creating a follow-up task. | Execute, but state clearly in chat what was done and which contact was affected. Operator can object retroactively. |
| **Ask first** | Deletes (blocked by rule 1 anyway, but the attempt itself must prompt). Bulk operations (>1 recipient, >1 contact modification in one call). Writing to any payment/installment field. Moving into closed stages or `Deposit Taken`. Moving contacts between pipelines. Creating new tags, custom fields, pipelines, stages, or calendars. Anything touching Pipeline D. Anything touching contacts in a closed stage. | Stop. Describe proposed action. Wait for explicit "yes" in chat. |

Operational limits (in addition to tiers):
- **Cooldown:** do not send the same contact more than one outbound message per 60 minutes unless they replied in between.
- **Daily message cap per contact:** 3. On the 3rd send, apply `needs-qualification` or flag to operator regardless of qualification status.
- **No duplicate same-action within cooldown window.** If a tag is already present, do not re-apply.

---

## Phase 3 MVP workflow: Lead intake & qualification

This is the **only** workflow the agent runs end-to-end right now. Everything else is read + report + ask.

### Trigger
- Operator asks in chat ("show new leads from the last 24h", "qualify this lead", etc.), OR
- (Phase 4 only) scheduled/webhook trigger.

### Required inputs from the contact
- `contact.age_1` (Age) — id `EMOPV3ntINbQyE6iST86`
- `contact.how_much_coverage_do_you_need` (How Much Coverage Do You Need?) — id `vcIddL5etIeOwPgE3wav`

### Qualification logic

```
read contact via mcp__ghl-mcp__contacts_get-contact:

  # Field reads — unwrap the MULTIPLE_OPTIONS array wrapper.
  # See the MCP Field-Access Patterns section above. A field absent from
  # the customFields array, or present with an empty value array,
  # resolves to the empty string "".
  age_entry      = customFields entry where id == "EMOPV3ntINbQyE6iST86"   # Age
  coverage_entry = customFields entry where id == "vcIddL5etIeOwPgE3wav"   # How Much Coverage Do You Need?

  Age      = age_entry.value[0]      if age_entry      exists AND age_entry.value      is a non-empty array  else ""
  Coverage = coverage_entry.value[0] if coverage_entry exists AND coverage_entry.value is a non-empty array  else ""

  if Age == "Under 18":
    → tag `minor-ineligible`
    → DO NOT move stage
    → notify operator (Tier: Notify)
    → stop

  if Age == "" OR Coverage == "" OR Coverage == "Not Sure":
    → tag `needs-qualification`
    → DO NOT move stage
    → notify operator with which field(s) are missing (Tier: Notify)
    → stop

  if Age == "76+":
    → tag `senior-specialty`
    → DO NOT move stage
    → notify operator that this lead needs specialty handling
      (final expense / whole life only; routes to licensed agent, not standard sales flow)
      (Tier: Notify)
    → stop

  else (Age ∈ {18-25, 26-35, 36-45, 46-55, 56-65, 66-75} AND
        Coverage ∈ {$10k-$50k, $50k-$100k, $100k-$500k, $500k+}):
    → tag `qualified-lead`
    → if Coverage == "$500k+": also tag `coverage-high-value`
    → move contact from `New Lead` → `Engaged Lead` in Pipeline A
       (stage id 8e90a7ac-40a5-4cbb-a8da-a8b30fbaaba1)
    → notify operator with a one-line summary (Tier: Notify)
    → stop
```

### Hard constraints on this workflow
- Only runs on contacts currently in `New Lead` of Pipeline A. If contact is elsewhere, report and stop.
- Never runs on closed stages, Pipeline D, Pipeline B, or Pipeline C.
- Never writes an insurance quote, price, eligibility determination, or binding statement. Qualification ≠ underwriting.

### Operator-visible output shape (chat)
```
Lead: <first name> <last name> (<contact id>)
Age: <value or MISSING>
Coverage: <value or MISSING>
Decision: <qualified-lead | needs-qualification | minor-ineligible>
Actions taken:
  - Tags applied: <list>
  - Stage move: <from → to, or "none">
Next step suggestion for operator: <one line>
```

---

## Template Migration Notes

**When this template is cloned to a new sub-account, every value below MUST be re-checked. Search the file for `[ACCOUNT-SPECIFIC]` to find all call-sites.**

### Values guaranteed to differ per sub-account
1. **Location block (entire):** `locationId`, `companyId`, Name, Address, Website, Timezone, Currency, Owner contact, created date, agency-sub-account flag, SaaS mode.
2. **All pipeline IDs** (Pipeline A / B / C / D ids) and **all stage IDs** within them. Even if the pipeline NAMES and stage NAMES are re-used from a shared snapshot, the IDs are freshly generated per sub-account.
3. **All custom field IDs** — regenerated per sub-account on snapshot load. Field *keys* (e.g. `contact.age_1`) tend to survive, but the `id` UUIDs do not.
4. **Parent group IDs** for custom field groups (`AgCGblr4VpZmZMrwmAtr`, `XJh8aiEEYU35VKFva2DR`, `Y3ABRtE5Lowt4UKmXH3e`, `B7Pj2fPpXD9f0yqveZ3d`, `b4P6fia3Zu7yuoq8fde3`, `okAeVebfyL7LWnxfFq7v`).
5. **Calendar IDs** — TBD here, will be TBD in every new sub-account until filled.
6. **Tag inventory** — TODO here; will be different per sub-account.
7. **Existence of Pipeline D (legacy).** Not every sub-account will have a legacy duplicate. Remove the Pipeline D section if a clone doesn't have one; add a new one if a different legacy exists.
8. **Picklist values** on fields like `Deal Program` (`Program 1/2/3`), `Payment Method`, `Currency` — each sub-account may customize.

### Values likely STABLE across all life-insurance sub-accounts (don't blindly reset)
- Vertical ("US life insurance").
- Safety rules (especially rules 9 and 10 on PII and compliance).
- Qualification logic shape (Age + Coverage gating).
- Agent-authored tag vocabulary names.
- Tiered autonomy table.
- Cooldown / daily-cap operational limits.
- Conventions (tag naming, date format, smart-quote handling).
- Structural note that all deal data lives on the contact (no opportunity fields) — verify per clone, but this is how the snapshot is built.
- **MCP Field-Access Patterns (entire section)** — these describe MCP-server behavior, not per-sub-account data, so they carry over unchanged. Re-verify only on major GHL or MCP-server upgrades.

### Cloning checklist (run this every time)
- [ ] Call `mcp__ghl-mcp__locations_get-location` → replace the Location block.
- [ ] Call `mcp__ghl-mcp__opportunities_get-pipelines` → rebuild Pipelines section (IDs + stages).
- [ ] Call `mcp__ghl-mcp__locations_get-custom-fields` with `model=all` → rebuild Custom Fields section.
- [ ] Verify `model: contact` universality and `How Much Coverage Do You Need?` + `Age` picklists still match the qualifier group; if they changed, update the Phase 3 workflow to match.
- [ ] Get calendar IDs from GHL UI and fill the Calendars TODO.
- [ ] List existing tags (via a sample contact or operator) and fill the Tags TODO.
- [ ] Re-read Pipeline D check: is there a legacy duplicate? Add/remove section accordingly.
- [ ] Re-save and commit with a message like `chore(template): sync CLAUDE.md for sub-account <name>`.
