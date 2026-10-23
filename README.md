<img src="assets/salvy-icon.png" alt="Salvy" width="96">

# Salvy MCP server

Connect your AI agent to [Salvy](https://salvy.com.br), the business mobile carrier from Brazil. The agent can look up your company's phone lines, usage, invoices and employees, and make changes such as blocking a line or changing a plan.

This repository only describes the server. The server itself is hosted by Salvy at:

```
https://mcp.salvy.com.br/mcp
```

- Transport: Streamable HTTP
- Authentication: OAuth 2.0. You sign in with your Salvy dashboard account ([app.salvy.com.br](https://app.salvy.com.br)), and the agent can only do what that account can do in the dashboard.
- Full guide (Portuguese): [docs.salvy.com.br/mcp-guide](https://docs.salvy.com.br/mcp-guide)

## What you can do

- **Look into your lines.** List phone lines, their data usage, SMS messages and timeline, and who uses each one.
- **Follow costs.** Read invoices, the current month's estimate and cost by cost center.
- **Act on your lines.** Block, unblock, cancel or create lines, add data, change plans and port numbers in.
- **Organize.** Manage employees, cost centers, line groups and assets such as phones and laptops.

Anything billable (new lines, extra data, plan changes) returns a quote first and is only charged after you confirm.

## Example prompts

- Which lines used the most data this month, and who uses each one?
- How much did each cost center spend on the October invoice?
- Block the line "Sales Team".

## Setup

### GitHub Copilot in VS Code

Add to `.vscode/mcp.json`:

```json
{
  "servers": {
    "salvy": {
      "type": "http",
      "url": "https://mcp.salvy.com.br/mcp"
    }
  }
}
```

Start the server and sign in when VS Code asks.

### Claude

Add Salvy from the Connectors Directory in Claude's settings, or add a custom connector with the URL above.

### Gemini app

In [gemini.google.com](https://gemini.google.com), open Settings → Connected Apps, add a custom app and paste the URL above.

### Gemini CLI

```bash
gemini extensions install https://github.com/SalvyLTD/salvy-mcp
```

Then run `/mcp auth salvy` inside Gemini CLI to sign in.

### Other clients

Any MCP client that supports remote servers over Streamable HTTP with OAuth works: point it at `https://mcp.salvy.com.br/mcp`.

## Tools

| Area | Tools |
| --- | --- |
| Companies | `list_companies` |
| Phone lines | `list_phone_accounts`, `get_phone_account`, `get_phone_account_usage`, `get_phone_account_timeline`, `list_phone_account_sms_messages`, `update_phone_accounts`, `create_phone_account_group` |
| Line actions | `create_phone_accounts`, `block_phone_accounts`, `unblock_phone_accounts`, `cancel_phone_accounts`, `unschedule_phone_account_cancellations`, `add_data_to_phone_accounts`, `change_subscription_plan`, `list_subscription_plans` |
| SIM shipments | `list_sim_card_shipments`, `get_sim_card_shipment` |
| Portability | `port_number`, `get_portability_status` |
| Billing | `list_invoices`, `get_invoice`, `get_current_month_estimate`, `get_cost_by_cost_center` |
| People | `list_employees`, `create_employee`, `list_cost_centers`, `create_cost_center`, `update_cost_center` |
| Assets | `list_assets`, `get_asset`, `get_asset_summary`, `create_assets`, `update_assets`, `list_asset_categories`, `create_asset_category`, `delete_asset_category`, `list_asset_statements`, `send_asset_statement` |
| Other | `get_task`, `submit_mcp_feedback` |

## Requirements

A company that is a Salvy customer, and a user with access to the Salvy dashboard.

## Support

contato@salvy.com.br · [Privacy policy](https://salvy.com.br/politica-de-privacidade) · [Reporting a vulnerability](SECURITY.md)
