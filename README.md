# HitPay

Cursor plugin that connects agents to [HitPay](https://hit-pay.com) through HitPay's hosted [Model Context Protocol](https://modelcontextprotocol.io/) server.

Ask about your HitPay business in plain language: sales, transactions, payouts, and balances. Create payment links, invoices, products, and recurring plans. The server cannot refund, cancel, move money, or change settings.

## Install

1. Open **Cursor Settings → Plugins**.
2. Search for **HitPay**.
3. Click **Install**, then complete the HitPay sign-in prompt.

Or run `/add-plugin hitpay` in chat.

Signing in opens the HitPay dashboard in your browser. Choose the business to connect under **Connect as** and approve. Only users with the **owner** or **admin** role on a business can authorize a connection.

## MCP

```json
{
  "mcpServers": {
    "hitpay": {
      "type": "http",
      "url": "https://mcp.hit-pay.com/"
    }
  }
}
```

Auth is OAuth 2.0 with Dynamic Client Registration and PKCE (`S256`). Cursor registers itself and prompts for HitPay sign-in when the plugin connects. There is no API key or client ID to configure.

## What agents can do

The server exposes 24 tools: 20 read tools and 4 create tools.

| Category | Tools |
| --- | --- |
| Sales and analytics | `get_sales_summary`, `get_top_products`, `get_sales_by_payment_method`, `get_sales_by_category`, `get_transactions_volume`, `get_channel_distribution`, `get_growth_indicator` |
| Transactions | `list_charges`, `get_charge_details`, `get_charge_refunds` |
| Payouts and balances | `list_payouts`, `get_payout_schedule`, `get_balances` |
| Commerce records | `list_orders`, `list_invoices`, `list_payment_links`, `get_payment_link` |
| Create | `create_payment_link`, `create_invoice`, `create_product`, `create_recurring_plan` |
| Account | `get_payment_methods`, `get_verification_status`, `get_integrations` |

The hosted server is the source of truth for tool names and schemas.

## Example prompts

- "What were my total sales last month, and how do they compare to the month before?"
- "List my recent transactions above SGD 100"
- "When is my next payout, and what's my current balance?"
- "Create a payment link for SGD 49.90 for a consultation session"

## Notes

- Each connection is scoped to the one business it was authorized for.
- Requests are rate limited to 30 per minute per business.
- The server connects to live accounts only. There is no sandbox endpoint yet.
- Remove the plugin, or disconnect it in Cursor, to stop it making new requests.
- This plugin points at `https://mcp.hit-pay.com/`, the URL in HitPay's documentation.

## Docs

- HitPay MCP Server: https://docs.hitpayapp.com/apis/guide/mcp-server
- Server URL: https://mcp.hit-pay.com/

Logo is HitPay's official mark.

## License

MIT
