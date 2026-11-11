---
name: humancalls
description: Use when the user wants something found out or done by phoning a business in the United States or Canada (check stock, get a quote, confirm opening hours, ask about an appointment, follow up on an order or a booking), or asks how a call they requested went. A real person at Hire Overseas places the call and reports back.
---

# Getting a phone call made with HumanCalls.ai

HumanCalls.ai has a real person phone a business for the user and report back a reviewed summary. The `humancalls` MCP server requests and tracks those calls. Calls are placed by people, during the business's local hours (8am to 9pm), so results arrive minutes to hours later, never instantly.

## 1. Get the request right before placing it

A request places a real phone call to a real business. Before `request_call`, have:

- The business name and its phone number (US or Canada only). If the user gave no number, find it and confirm it with them.
- Who the caller should say they are calling for: the user's name or company.
- The goal, in plain words, and anything the caller may be asked (an order or account number, dates, preferences).
- The specific answers to bring back, as `collect` fields, when the user wants particular facts.

Read the business, number and goal back to the user and get a yes. An information request does not authorize a purchase, booking or cancellation unless the user says so.

## 2. Place the call

Call `request_call`. Tell the user the call is under way, roughly when to expect it (now if the business is open, otherwise the next morning there), and the most it can cost. Nothing is charged unless the call connects.

Do not promise a result time, and do not poll in a loop. Check with `get_call` when the user asks or comes back.

## 3. Follow up

- `get_call` gives the status and, once finished, the summary, answers and cost. Offer the transcript only if the user wants what was said.
- If `open_questions` has an entry, the caller needs something before dialing. Ask the user, then send it with `answer_question`. If the user doesn't know, say so with `unavailable`.
- `add_details` adds information to a call that hasn't started dialing.
- `cancel_call` cancels a call that hasn't started dialing; canceled calls cost nothing.
- `list_calls` shows recent calls; `get_account` shows remaining credit and minutes.

## What it won't do

Requests are checked before anyone dials, and some are declined: consumer sales or cold calls, debt collection, political calls, anything deceptive or pressuring, pretending to be the user or someone else, and anything that needs passwords, verification codes, full card numbers or Social Security numbers. Callers always say who they are calling for and that the call is recorded. If a request is declined, tell the user why and do not rephrase it to get around the rule.

## Cost

Calls are paid per connected minute from prepaid credit; `max_minutes` caps one call. Unanswered, declined and canceled calls are free. New accounts start with 10 free minutes. More credit is bought by the user on their dashboard; you cannot buy it for them. When credit runs out, say so and point them to the dashboard link from `get_account`.
