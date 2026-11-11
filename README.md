# HumanCalls

A person phones a US or Canadian business for you and reports back what was said.

HumanCalls connects Claude, ChatGPT, Cursor and other MCP clients to [HumanCalls](https://humancalls.ai). Your assistant describes the call, a person places it, and a reviewed summary comes back. Callers introduce themselves, say who they are calling for, and say the call is recorded.

**Server URL:** `https://humancalls.ai/mcp` (Streamable HTTP, OAuth 2.1 with PKCE)

Ask things like:

- "Call Harbor Supply at (512) 555-0142 and ask if SKU 7712 is in stock and what 40 units cost. Information only."
- "Call Lakeside Hardware and ask if they are open on Friday and whether they cut keys in store."
- "How did that call go?"

## Install

### Claude Code

```
claude mcp add --transport http humancalls https://humancalls.ai/mcp
```

Start Claude Code, type `/mcp`, pick humancalls and sign in. Your browser opens HumanCalls. Enter your email and the six-digit code, then choose Allow. A first sign-in creates a workspace with 10 free minutes once you verify your email.

This repository is also a Claude plugin, which adds the same server plus a skill for requesting and following up calls: `/plugin marketplace add Hire-Overseas/humancalls-mcp`, then `/plugin install humancalls@humancalls`.

### Cursor

Add this to `~/.cursor/mcp.json`, or to `.cursor/mcp.json` inside one project:

```json
{
  "mcpServers": {
    "humancalls": {
      "url": "https://humancalls.ai/mcp"
    }
  }
}
```

Cursor shows the server as needing sign-in. Choose it, enter your email and the six-digit code, then choose Allow. A first sign-in creates a workspace with 10 free minutes. To use an API key from the dashboard instead of the browser sign-in, send it as a Bearer token and keep the key out of files you commit:

```json
{
  "mcpServers": {
    "humancalls": {
      "url": "https://humancalls.ai/mcp",
      "headers": { "Authorization": "Bearer YOUR_API_KEY" }
    }
  }
}
```

### Claude

1. Open Customize, then Connectors.
2. Choose Add, then Add custom connector.
3. Name it HumanCalls and paste `https://humancalls.ai/mcp`.
4. Continue and choose Add. Claude sends you to HumanCalls to sign in.
5. Enter your email and the six-digit code, then choose Allow.
6. In a chat, open the + menu, choose Connectors and switch HumanCalls on.

This works on every Claude plan. The free plan allows one custom connector. On a Team or Enterprise plan an owner adds it under Organization settings, then each person opens Customize, Connectors and chooses Connect.

### ChatGPT

1. Go to `chatgpt.com/plugins`, choose the plus button, then Add custom MCP server.
2. Name it HumanCalls, add a short description, and under Connection paste `https://humancalls.ai/mcp`.
3. Leave sign-in on OAuth, confirm that you want to continue, and choose Create as a plugin. ChatGPT sends you to HumanCalls.
4. Enter your email and the six-digit code, then choose Allow. A first sign-in creates your account with 10 free minutes.
5. In a new chat, type @ and pick HumanCalls.

Adding your own app is not offered on every ChatGPT plan or workspace. If you do not see the option, your plan or your workspace admin does not allow it yet.

Any other client that supports MCP over Streamable HTTP with OAuth can use the same server URL. Setup steps stay current on the [Connect page](https://humancalls.ai/connect).

## Tools

| Tool | What it does | Changes anything |
| --- | --- | --- |
| `request_call` | Creates the call: the business, number, goal and the answers to bring back. Returns a call id at once. The call happens later. | Yes: a real call is placed |
| `get_call` | Status and, once finished, the summary, typed answers, cost, and links to the recording and transcript. | No |
| `list_calls` | Recent calls. | No |
| `cancel_call` | Cancels a call that is still queued or assigned, before anyone dials. | Yes |
| `answer_question` | Replies when the caller asks a question before dialing. | Yes |
| `add_details` | Adds information before the first dial. | Yes |
| `get_account` | Remaining credit and minutes. | No |

In ChatGPT and Claude, a finished call shows as a card with status, summary, answers and cost. Results are read with `get_call` when you ask. Recordings and transcripts can arrive a little after the call finishes, so ask again if those links are missing.

## How a call runs

Calls go to businesses in the United States and Canada, between 8am and 9pm in the business's local time. A result can take a few minutes, or arrive the next business morning.

Every request is checked before anyone dials. Clear prohibited requests are declined with no charge. Callers stay inside the instructions you gave. An information request leaves purchases, bookings and cancellations unauthorized until you say otherwise.

These calls are not accepted: sales calls, debt collection, political calls, cold calls to consumers, sensitive healthcare workflows, and anything deceptive. Leave passwords, verification codes, full card numbers and Social Security numbers out of a request.

## Pricing

$1 per connected minute, rounded up to the next minute. The charge covers time after the business answers, including phone menus and hold. A call costs $0 when nobody answers, or when the request is declined or canceled. A new workspace gets 10 free minutes once the owner verifies their email. You buy more credit on your dashboard. The assistant can read the balance with `get_account`.

## Links

- [HumanCalls](https://humancalls.ai)
- [API docs](https://humancalls.ai/docs)
- [Connect a chat app](https://humancalls.ai/connect)
- [Pricing](https://humancalls.ai/pricing)
- [Trust and process](https://humancalls.ai/trust)
- [Privacy policy](https://humancalls.ai/privacy)
- [Terms](https://humancalls.ai/terms)

Questions: support@humancalls.ai

## License

MIT, for the files in this repository. The service is operated by Hire Overseas.
