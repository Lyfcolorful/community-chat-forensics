---
name: community-chat-forensics
description: Analyze customer service group chats or online support logs - merge messages into consultation cases, classify and tag them, judge closure and broken chains, spot credential exposure and business signals, and produce a case index and findings report.
---

# Customer Chat Forensics

Use this method to analyze chat records from customer service groups (WeCom/WeChat Work, DingTalk, Feishu/Lark, Slack, etc.) or online support conversations. The goal is not just to measure how fast replies come. It is to see three things clearly: whether each customer request was carried through to a result, where it broke down, and which practices need to change.

Reply in the user's language. Category, tag and status names below may be translated, but keep their meanings.

## When to use

- You have a batch of group chat or online support records and need to analyze the current state of service. Records can be exported HTML, text, screenshots or pasted content.
- You need evidence to design service processes, rules, a knowledge base, or an AI support agent.
- You need to review a specific group, time period, or support account.

## Confirm before starting (ask if any item is missing)

1. **Scope**: which groups, what time period, and where the source files are. Check for duplicates when a group has several exports: identical content counts once; a "superset" covering a longer period replaces the older one and is not counted twice.
2. **Speaker list**: which accounts are our support agents, account managers or sales, and other staff; who on the customer side is an administrator. You may pre-identify speakers from member types in the export (e.g. "internal member / external contact"), our account naming rules, and any list the user provides, but **the user must confirm the list**. Never rely on automatic identification alone.
3. **Purpose**: a full baseline review, a deep dive on one type of problem, or a comparison of service practices. The emphasis of the output depends on the purpose.

## Steps

### 1 Convert to plain text and label speakers

- Convert the chat into one line per message: time | speaker | role | content | link to the original message.
- If images, videos or files were not reviewed one by one, **state "images not reviewed" in the method notes**, and downgrade any conclusion that depends on them to "to be verified".
- If there is an "AI answer" tag, explain what it means. Usually it is not an AI replying in the group: either the customer asked the in-product assistant first and then came to a human, or an agent pasted a screenshot of the assistant's answer.

### 2 Merge messages into consultation cases

A case is one thing the customer is trying to get done. It is not a single message, and it is not a ticket.

- Merge follow-ups, additions and chasers about the same request into one case. If one message contains several independent requests, split them, or record one case and note "contains N sub-questions".
- Remove greetings, promotional posts, stickers and pure pleasantries ("OK", "thanks", "got it"). But keep a customer's "OK" as evidence of closure.
- For large volumes, first split automatically at "no messages for 4 hours", then read and merge manually. Numbers from the two methods are not directly comparable; state which one you used.
- Number cases as group code + sequence, e.g. A-01, B-12, and link each case to the original message. **Do not use abbreviations of real customer names as group codes**, especially in material shared outside the team.

### 3 Classify, tag, and record visible status

**Main category (one per case, by main handling path):**

| Main category | Typical questions |
|---|---|
| Navigation and data export | Where is the entry point, how to export, steps |
| Business rules and data changes | Rules for exams, certificates, etc.; delete and restore; data edits |
| Accounts and permissions | Cannot find a person, cannot see data, admin changes, quotas |
| Feature limits and new requests | Not supported, wants a new feature, workarounds |
| Technical issues and troubleshooting | Upload failures, abnormal status, errors, compatibility |
| Messages and notifications | Notifications not received, sent by mistake, recalled |
| Internal business and system coordination | Customer's internal ownership, data sync chains |

You may adapt categories to your industry and product, but state the changes in the method notes.

**Tags (multiple allowed):** customer internal admin, spans multiple days, account manager involved, repeat contact, escalated to engineering, escalated to product, complaint or dissatisfaction, wrong answer corrected, credential exposure, moved to private chat or phone, urgent impact, AI answer. Add second-level tags as needed (e.g. overseas, exams) so similar issues are not lumped together.

**Visible status (only what can be seen in the chat):** answered and confirmed by customer | path given, no confirmation seen | waiting on customer's internal handling | request not taken up | customer solved it themselves | escalated, no result seen | no answer seen in chat | cause located, no retest seen | waiting for customer information.

### 4 Measure responses and broken chains

- **Request message**: a customer message containing a question, a request for help, a fault report or an application; exclude pure closing remarks.
- **Method**: time from the request message to our first reply in the chat within 3 calendar days. A first reply after more than 24 hours is "late reply"; no reply from us in the chat within 3 days is "broken chain, no response". Also report the median response time.
- **Automatic results must be reviewed manually** to remove false hits: customers answering each other, welcome templates, and wrap-ups such as "solved / never mind". Report both the automatic count and the reviewed estimate.
- **State what this method cannot measure**:
  - we replied "one moment" and then nothing followed (cover this with the case-level method);
  - work moved to private chat or phone is invisible in the group;
  - quoted messages missing from the export.
- **Root causes of broken chains** fall into four groups: no one covering outside working hours, no one tracking after escalation, permission dead ends, customers fixing it themselves.

### 5 Judge closure; silence is not resolution

- Report separately the share of cases where we actively confirmed the problem was solved.
- Record the following separately. **None of them counts as satisfied closure**:
  - the customer solved it themselves;
  - silent ending: the customer only said "OK" and never came back;
  - reluctant acceptance: the customer accepted the answer while clearly unhappy.
- If the customer reopens after a fix, or the same problem comes back, link it to the original case.

### 6 Identify risks and signals

| What to look for | How to record it |
|---|---|
| Credential exposure | Record only that it happened and who did it (customer posted it / we asked for it). **Never transcribe any account, password or authorization code** |
| Dissatisfaction or complaint signals | Summarize the key words; pass them to the account owner as a business signal; count separately from formal complaints |
| Handoff that went nowhere | Moved to private chat, passed to a colleague, moved to a meeting, asked for materials, shift change, then nothing; list by type |
| "Not supported" with no next step | Was a request logged? Was there an answer the customer could be given? |
| Urgent impact | Live broadcasts, on-site training, mistaken mass notifications, etc.; record scope of impact and time to first response |
| Acting on the customer's behalf | Who did it, with or without the customer's consent, and whether the rule was applied consistently |
| Out-of-scope requests | Other product lines, business partnerships, etc.; was there a handoff receipt? |

### 7 Find problem clusters

When the same root cause appears across several cases or groups (e.g. account master-data sync, mismatched progress and status, platform-wide incidents), create a "parent issue + child cases": list the affected customers and note that each one should be followed up after recovery. Repeat contacts are the entry point for checking what was avoidable, but do not treat them directly as a volume of problems that can be eliminated.

### 8 (Optional) Compare service practices

- Compare practices only; **do not evaluate individuals**. Treat accounts with fewer than 30 cases as reference only.
- Metrics: median and P90 of first response, misunderstanding rate, whether the tone was curt, whether assistant answers were pasted verbatim, active confirmation, handling of credentials.
- Test differences for significance (e.g. chi-square test), and state confounders such as customer mix and problem types.

## Output

Produce the following three layers as needed, leading with the conclusions:

1. **Case index** (one per group):

| No. | Date | Main category | Case (link to original message) | Evidence and handling in chat | Visible status |
|---|---|---|---|---|---|

2. **Categories and handling**: for each category, the number of cases, typical questions, how we handle it, and who should own it; then pick 3-5 concrete cases to show which practices should change.
3. **Overall findings**, in this order:
   - conclusions: 3-5 points, with numbers;
   - scope and method;
   - volume and distribution;
   - main findings: for each, the scale, example case numbers, and what it means;
   - implications for service design;
   - limitations.

## Rules that must hold

- **Visible status is not a resolution rate**, and must not be used to calculate resolution rates or SLA attainment.
- Separate facts, judgments and guesses. Product rules stated in the chat only reflect "what was said at the time" and must not be written up as current rules unless verified.
- A cause without supporting evidence is written as "to be investigated", never as a confirmed root cause.
- State the method behind every number: manual merging or automatic splitting, and what the denominator is.
- Cite cases with their number and a link to the original message so they can be traced.
- Quote personal information about customers and staff only when necessary; never transcribe credentials.
- Findings are for improving practices and design, not for appraising individuals.
- Before sharing results outside the team, de-identify them: replace or remove customer names, group names, personal names, accounts, links and personal details in screenshots.
