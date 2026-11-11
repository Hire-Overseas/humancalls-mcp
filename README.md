# HumanCalls.ai MCP

Have a real person make the phone call. This connects Claude, ChatGPT, Grok, Cursor and other MCP clients to [HumanCalls.ai](https://calls.hireoverseas.com) by [Hire Overseas](https://www.hireoverseas.com): your assistant describes a call to a business in the United States or Canada, a person places it, and a reviewed summary comes back.

**Server URL:** `https://calls.hireoverseas.com/mcp` (Streamable HTTP, OAuth sign-in with your email)

Ask things like:

- "Have someone call Ace Plumbing at (303) 555-0199 and ask their earliest appointment for a leaking water heater."
- "Call Harbor Supply and ask if SKU 7712 is in stock and what 40 units cost."
- "How did that call go?"

## Install

- **Claude Code:** `/plugin marketplace add Hire-Overseas/humancalls-mcp`, then `/plugin install humancalls@humancalls`.
- **Claude (web and desktop):** Customize → Connectors → Add custom connector, and paste the server URL.
- **ChatGPT:** Plugins → Add → Add custom MCP server, and paste the server URL.
- **Grok:** grok.com/connectors → New Connector → Custom, and paste the server URL.
- **Cursor, VS Code and other MCP clients:** add an HTTP server with the URL above.

The first time, you sign in with your email and a six-digit code. A new account gets 10 free call minutes.

## Tools

| Tool | What it does | Changes anything |
| --- | --- | --- |
| `request_call` | Asks a person to phone a business. Returns a call id at once; the call happens later. | Yes: a real call is placed |
| `get_call` | Status and, once finished, the summary, answers, cost and optional transcript. | No |
| `list_calls` | Recent calls. | No |
| `cancel_call` | Cancels a call that hasn't started dialing. | Yes |
| `answer_question` | Answers a question the caller asked before dialing. | Yes |
| `add_details` | Adds information to a call that hasn't started dialing. | Yes |
| `get_account` | Remaining credit and minutes. | No |

In ChatGPT and Claude, calls appear as a card with status, summary, answers and cost.

## How it works

- Calls go to businesses in the United States and Canada, during the business's local hours (8am to 9pm). Results arrive minutes to hours after a request; nothing is pushed into the chat, so ask your assistant to check.
- Every request is checked against calling rules before anyone dials. Callers say who they are calling for and that the call is recorded, and never pretend to be you.
- Not supported: consumer sales or cold calls, debt collection, political calls, anything deceptive, and anything needing passwords, verification codes or card numbers.

## Cost

Calls are paid per connected minute from prepaid credit, capped per call. Unanswered, declined and canceled calls are free. Credit is bought on your dashboard, never through the assistant.

## Privacy and support

[Privacy policy](https://calls.hireoverseas.com/privacy) · [Terms](https://calls.hireoverseas.com/terms) · [Support](https://calls.hireoverseas.com/support) · support@hireoverseas.com

## License

MIT, for the files in this repository. The service itself is operated by Hire Overseas.
