---
name: bybit-mcp
description: Skill da REST API do Bybit na MCP.AI: 337 endpoints em /api/bybit. Exchange de criptomoedas Bybit, saldo da conta unificada e da carteira Funding, posições abertas em derivativos, ordens, execuções com taxa por trade, empréstimos, bots e cotação de mercado, via API REST oficial V5, com cobertura total de leitura e de escrita. Criar e cancelar ordem exigem uma chave com permissão de negociação. Saque e transferência entre carteiras não são expostos. Autenticação por api_key e api_secret gerados na sua conta Bybit. Autentique com workspace API key (sk_live) gerada em app.mcp.ai/settings/api-keys. Use quando o usuário pedir algo coberto pelos endpoints.
---

# Bybit — REST API skill

Você tem acesso à **Bybit** REST API na MCP.AI.

> Exchange de criptomoedas Bybit, saldo da conta unificada e da carteira Funding, posições abertas em derivativos, ordens, execuções com taxa por trade, empréstimos, bots e cotação de mercado, via API REST oficial V5, com cobertura total de leitura e de escrita. Criar e cancelar ordem exigem uma chave com permissão de negociação. Saque e transferência entre carteiras não são expostos. Autenticação por api_key e api_secret gerados na sua conta Bybit.

## Base URL

```
https://api.mcp.ai/api/bybit
```

Todo endpoint é um **POST** na Base URL + o path abaixo. Os parâmetros vão no corpo JSON.

## Autenticação

Inclua em toda request:

```
Authorization: Bearer sk_live_...
Content-Type: application/json
```

> Gere sua chave em **https://app.mcp.ai/settings/api-keys** (workspace API key `sk_live_…`, não expira, revogável). Uma única chave serve pra todos os seus MCPs.

## Formato de resposta

```json
{ "ok": true, "tool": "<tool_id>", "result": <payload> }
```

## Exemplo cURL

```bash
curl -X POST https://api.mcp.ai/api/bybit/accept/non/lp/quote \
  -H "Authorization: Bearer sk_live_..." \
  -H "Content-Type: application/json" \
  -d '{"rfqId":"..."}'
```

## Reportar problemas

Se um endpoint retornar erro, vazio ou dado inesperado, reporte (não desista calado): **POST /api/bybit/report** com `{ "message": "...", "context"?: "...", "conversation"?: [...] }`. Isso notifica o time da MCP.AI.

## Endpoints (337)

#### `bybit_accept_non_lp_quote`

Enable acceptance of non-LP quotes for a specific RFQ. _(POST /api/bybit/accept/non/lp/quote)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `rfqId` | string | Sim |  |

#### `bybit_account_borrow`

Manual borrow for Unified account. _(POST /api/bybit/account/borrow)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coin` | string | Sim |  |
| `amount` | string | Sim |  |

#### `bybit_account_coin_balance_query`

Query the balance of a specific coin in a specific account type. _(POST /api/bybit/account/coin/balance/query)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `accountType` | string | Sim |  |
| `coin` | string | Sim |  |
| `memberId` | number | Não | Opcional. |
| `toMemberId` | number | Não | Opcional. |
| `toAccountType` | string | Não | Opcional. |
| `withBonus` | string | Não | Opcional. (0, 1) |
| `withTransferSafeAmount` | string | Não | Opcional. (0, 1) |
| `withLtvTransferSafeAmount` | string | Não | Opcional. (0, 1) |

#### `bybit_account_fixed_borrow`

Create a fixed-rate borrow order for Unified account. _(POST /api/bybit/account/fixed/borrow)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderCurrency` | string | Sim |  |
| `orderAmount` | string | Sim |  |
| `annualRate` | string | Sim |  |
| `term` | string | Sim |  (7, 14, 30, 90, 180) |
| `repayType` | string | Não | Opcional. (1, 2) |
| `strategyType` | string | Não | Opcional. (PARTIAL, FULL) |

#### `bybit_account_no_convert_repay`

Manual repay without asset conversion (lossless repay). _(POST /api/bybit/account/no/convert/repay)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coin` | string | Não | Opcional. |
| `amount` | string | Não | Opcional. |
| `repaymentType` | string | Não | Opcional. (ALL, FIXED, FLEXIBLE) |

#### `bybit_account_repay`

Manually repay the liabilities of Unified account. _(POST /api/bybit/account/repay)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coin` | string | Não | Opcional. |
| `amount` | string | Não | Opcional. |
| `repaymentType` | string | Não | Opcional. (ALL, FIXED, FLEXIBLE) |

#### `bybit_add_liquidity`

Inject funds into a Liquidity Mining pool. _(POST /api/bybit/add/liquidity)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `productId` | string | Sim |  |
| `orderLinkId` | string | Sim |  |
| `quoteAccountType` | string | Não | Opcional. (FUND, UNIFIED) |
| `baseAccountType` | string | Não | Opcional. (FUND, UNIFIED) |
| `quoteAmount` | string | Não | Opcional. |
| `baseAmount` | string | Não | Opcional. |
| `leverage` | string | Não | Opcional. |

#### `bybit_add_margin`

Add additional collateral (margin) to a leveraged Liquidity Mining position to avoid liquidation. _(POST /api/bybit/add/margin)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `productId` | string | Sim |  |
| `orderLinkId` | string | Sim |  |
| `positionId` | string | Sim |  |
| `amount` | string | Sim |  |
| `quoteAccountType` | string | Sim |  (FUND, UNIFIED) |

#### `bybit_add_reduce_margin`

Add or reduce margin for a position in isolated margin mode. _(POST /api/bybit/add/reduce/margin)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (linear, inverse) |
| `symbol` | string | Sim |  |
| `margin` | string | Sim |  |
| `positionIdx` | string | Não | Opcional. (0, 1, 2) |

#### `bybit_amend_order`

Modify an existing open order. _(POST /api/bybit/amend/order)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (spot, linear, inverse, option) |
| `symbol` | string | Sim |  |
| `orderId` | string | Não | Opcional. |
| `orderLinkId` | string | Não | Opcional. |
| `orderIv` | string | Não | Opcional. |
| `triggerPrice` | string | Não | Opcional. |
| `qty` | string | Não | Opcional. |
| `price` | string | Não | Opcional. |
| `tpslMode` | string | Não | Opcional. (Full, Partial) |
| `takeProfit` | string | Não | Opcional. |
| `stopLoss` | string | Não | Opcional. |
| `tpTriggerBy` | string | Não | Opcional. (LastPrice, IndexPrice, MarkPrice) |
| `slTriggerBy` | string | Não | Opcional. (LastPrice, IndexPrice, MarkPrice) |
| `triggerBy` | string | Não | Opcional. (LastPrice, IndexPrice, MarkPrice) |
| `tpLimitPrice` | string | Não | Opcional. |
| `slLimitPrice` | string | Não | Opcional. |

#### `bybit_amend_spread_order`

Amend (modify) the price and/or quantity of an existing spread trading order. _(POST /api/bybit/amend/spread/order)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `symbol` | string | Sim |  |
| `orderId` | string | Não | Opcional. |
| `orderLinkId` | string | Não | Opcional. |
| `qty` | string | Não | Opcional. |
| `price` | string | Não | Opcional. |

#### `bybit_apply_quote`

Apply for a conversion quote. The system will return: (POST /v5/fiat/quote-apply). [write, mexe em dinheiro na sua conta Bybit] _(POST /api/bybit/apply/quote)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `fromCoin` | string | Sim |  |
| `fromCoinType` | string | Sim |  (fiat, crypto) |
| `toCoin` | string | Sim |  |
| `toCoinType` | string | Sim |  (fiat, crypto) |
| `requestAmount` | string | Sim |  |
| `requestCoinType` | string | Não | Opcional. (fiat, crypto) |

#### `bybit_batch_amend_orders`

Modify multiple existing open orders in a single API call. _(POST /api/bybit/batch/amend/orders)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (spot, linear, inverse, option) |
| `request` | string | Sim | Lista como JSON string, ex.: [{...}]. |

#### `bybit_batch_cancel_orders`

Cancel multiple orders in a single API call. _(POST /api/bybit/batch/cancel/orders)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (spot, linear, inverse, option) |
| `request` | string | Sim | Lista como JSON string, ex.: [{...}]. |

#### `bybit_batch_create_orders`

Place multiple orders in a single API call. _(POST /api/bybit/batch/create/orders)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (spot, linear, inverse, option) |
| `request` | string | Sim | Lista como JSON string, ex.: [{...}]. |

#### `bybit_cancel_all_orders`

Cancel all open orders matching the specified criteria. _(POST /api/bybit/cancel/all/orders)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (spot, linear, inverse, option) |
| `symbol` | string | Não | Opcional. |
| `baseCoin` | string | Não | Opcional. |
| `settleCoin` | string | Não | Opcional. |
| `orderFilter` | string | Não | Opcional. (Order, tpslOrder, StopOrder, OcoOrder, BidirectionalTpslOrder, OpenOrder) |
| `stopOrderType` | string | Não | Opcional. (Stop) |

#### `bybit_cancel_all_quotes`

Cancel all active quotes for the authenticated account. _(POST /api/bybit/cancel/all/quotes)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_cancel_all_rfqs`

Cancel all active RFQs for the authenticated account. _(POST /api/bybit/cancel/all/rfqs)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_cancel_all_spread_orders`

Cancel all open spread trading orders, optionally filtered by symbol. _(POST /api/bybit/cancel/all/spread/orders)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `symbol` | string | Não | Opcional. |
| `cancelAll` | boolean | Não | Opcional. |

#### `bybit_cancel_order`

Cancel a single open order by `orderId` or `orderLinkId`. _(POST /api/bybit/cancel/order)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (spot, linear, inverse, option) |
| `symbol` | string | Sim |  |
| `orderId` | string | Não | Opcional. |
| `orderLinkId` | string | Não | Opcional. |
| `orderFilter` | string | Não | Opcional. (Order, tpslOrder, StopOrder) |

#### `bybit_cancel_quote`

Cancel an active quote. You must pass one of the following parameters: `quoteId`, `rfqId`, or `quoteLinkId`. (POST /v5/rfq/cancel-quote). [write, mexe em dinheiro na sua conta Bybit] _(POST /api/bybit/cancel/quote)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `quoteId` | string | Não | Opcional. |
| `rfqId` | string | Não | Opcional. |
| `quoteLinkId` | string | Não | Opcional. |

#### `bybit_cancel_rfq`

Cancel an active RFQ. You must pass either `rfqId` or `rfqLinkId`. (POST /v5/rfq/cancel-rfq). [write, mexe em dinheiro na sua conta Bybit] _(POST /api/bybit/cancel/rfq)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `rfqId` | string | Não | Opcional. |
| `rfqLinkId` | string | Não | Opcional. |

#### `bybit_cancel_spread_order`

Cancel a single spread trading order by its order ID or custom order link ID. _(POST /api/bybit/cancel/spread/order)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderId` | string | Não | Opcional. |
| `orderLinkId` | string | Não | Opcional. |

#### `bybit_claim_liquidity_interest`

Claim all available interest for the specified product in one click. _(POST /api/bybit/claim/liquidity/interest)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `productId` | string | Sim |  |

#### `bybit_close_combo_bot`

Closes (stops) a running futures combo trading bot. _(POST /api/bybit/close/combo/bot)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `bot_id` | number | Sim |  |
| `stop_type` | string | Não | Opcional. (0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15) |
| `bot_ids` | number[] | Não | Bulk mode: multiple values for bot_id |

#### `bybit_close_dca_bot`

Closes a running DCA bot. You must specify a close_mode to determine (POST /v5/dca/close-bot). [write, mexe em dinheiro na sua conta Bybit] _(POST /api/bybit/close/dca/bot)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `bot_id` | number | Sim |  |
| `close_mode` | string | Sim |  (1, 2, 3) |
| `bot_ids` | number[] | Não | Bulk mode: multiple values for bot_id |

#### `bybit_close_f_grid_bot`

Closes (stops) a running futures grid trading bot. _(POST /api/bybit/close/f/grid/bot)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `bot_id` | number | Sim |  |
| `bot_ids` | number[] | Não | Bulk mode: multiple values for bot_id |

#### `bybit_close_f_mart_bot`

Closes (stops) a running futures Martingale trading bot. _(POST /api/bybit/close/f/mart/bot)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `bot_id` | number | Sim |  |
| `stop_type` | string | Não | Opcional. (F_MART_BOT_STOP_TYPE_STOP_TYPE_UNKNOWN_UNSPECIFIED, F_MART_BOT_STOP_TYPE_STOP_TYPE_INIT_ERROR, F_MART_BOT_STOP_TYPE_STOP_TYPE_BY_USER, F_MART_BOT_STOP_TYPE_STOP_TYPE_BY_LIQ, F_MART_BOT_STOP_TYPE_STOP_TYPE_BY_SYMBOL_OFFLINE, F_MART_BOT_STOP_TYPE_STOP_TYPE_BY_SL, F_MART_BOT_STOP_TYPE_STOP_TYPE_BY_SYSTEM, F_MART_BOT_STOP_TYPE_STOP_TYPE_BY_USER_BANNED, F_MART_BOT_STOP_TYPE_STOP_TYPE_BY_TP_SINGLE_ROUND, F_MART_BOT_STOP_TYPE_STOP_TYPE_BY_ORDER_COST, F_MART_BOT_STOP_TYPE_STOP_TYPE_BY_REDUCE_ONLY, F_MART_BOT_STOP_TYPE_STOP_TYPE_BY_BUST_PRICE, F_MART_BOT_STOP_TYPE_STOP_TYPE_BY_NEGATIVE_ARBITRAGE, F_MART_BOT_STOP_TYPE_STOP_TYPE_BY_COMPLIANCE, F_MART_BOT_STOP_TYPE_STOP_TYPE_BY_ADL) |
| `bot_ids` | number[] | Não | Bulk mode: multiple values for bot_id |

#### `bybit_close_grid_bot`

Closes a running spot grid bot. _(POST /api/bybit/close/grid/bot)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `grid_id` | number | Sim |  |
| `close_mode` | string | Sim |  (1, 2, 3, 4) |
| `grid_ids` | number[] | Não | Bulk mode: multiple values for grid_id |

#### `bybit_coin_convert_limit_query`

Query single conversion min/max limit for specified coin pair under specified account type. _(POST /api/bybit/coin/convert/limit/query)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `fromCoin` | string | Sim |  |
| `fromCoinType` | string | Não | Opcional. (0, 1) |
| `toCoin` | string | Sim |  |
| `toCoinType` | string | Não | Opcional. (0, 1) |
| `accountType` | string | Sim |  |

#### `bybit_coin_list_query`

Query convertible coin list under specified account type and conversion direction. _(POST /api/bybit/coin/list/query)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `accountType` | string | Sim |  (eb_convert_funding, eb_convert_uta, eb_convert_spot, eb_convert_contract, eb_convert_inverse) |
| `side` | string | Não | Opcional. (0, 1) |
| `coin` | string | Não | Opcional. |

#### `bybit_confirm_new_risk_limit`

Confirm the pending maintenance margin rate update for a position. _(POST /api/bybit/confirm/new/risk/limit)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (linear, inverse) |
| `symbol` | string | Sim |  |

#### `bybit_confirm_quote`

Confirm the quote and execute the conversion trade. _(POST /api/bybit/confirm/quote)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `quoteTxId` | string | Sim |  |
| `subUserId` | string | Sim |  |
| `webhookUrl` | string | Não | Opcional. |
| `merchantRequestId` | string | Não | Opcional. |

#### `bybit_convert_execute`

Confirm and execute a conversion based on quote ID. _(POST /api/bybit/convert/execute)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `quoteTxId` | string | Sim |  |

#### `bybit_convert_history_query`

Query all confirmed conversion records. _(POST /api/bybit/convert/history/query)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `accountType` | string | Não | Opcional. |
| `index` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |

#### `bybit_create_chase_order_strategy`

Creates a Chase Order strategy that continuously monitors market price and (POST /v5/strategy/create). _(POST /api/bybit/create/chase/order/strategy)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (UTA_USDT, UTA_USDC, UTA_USDC_FUTURE, UTA_SPOT, UTA_INVERSE, UTA_INVERSE_FUTURE, UTA_USDT_FUTURE) |
| `symbol` | string | Sim |  |
| `side` | string | Sim |  (Buy, Sell) |
| `size` | string | Sim |  |
| `strategyType` | string | Não | Opcional. (chaseOrder) |
| `chaseDistance` | string | Não | Opcional. |
| `chasePercentE4` | number | Não | Opcional. |
| `maxChasePrice` | string | Não | Opcional. |
| `triggerPrice` | string | Não | Opcional. |
| `reduceOnly` | boolean | Não | Opcional. |
| `positionIdx` | string | Não | Opcional. (0, 1, 2) |
| `leverageType` | string | Não | Opcional. (0, 1) |

#### `bybit_create_combo_bot`

Creates a futures combo trading bot that manages a portfolio of multiple (POST /v5/fcombobot/create). _(POST /api/bybit/create/combo/bot)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `leverage` | string | Sim |  |
| `init_margin` | string | Sim |  |
| `adjust_position_mode` | string | Sim |  (0, 1, 2, 3, 4, 5, 6) |
| `adjust_position_percent` | string | Não | Opcional. |
| `adjust_position_time_interval` | number | Não | Opcional. |
| `symbol_settings` | string | Sim | Lista como JSON string, ex.: [{...}]. |
| `sl_percent` | string | Não | Opcional. |
| `tp_percent` | string | Não | Opcional. |
| `source` | string | Não | Opcional. (0, 1, 2) |
| `block_source` | string | Não | Opcional. (0, 1, 2, 3, 4) |
| `create_type` | string | Não | Opcional. (0, 1, 2, 3) |
| `followed_bot_id` | number | Não | Opcional. |
| `init_bonus` | string | Não | Opcional. |
| `trailing_stop_percent` | string | Não | Opcional. |
| `channel` | string | Não | Opcional. |
| `followed_bot_ids` | number[] | Não | Bulk mode: multiple values for followed_bot_id |

#### `bybit_create_copy_mt5_bind`

Create a new Copy Trading TradFi follow binding by specifying a target `providerMark` (POST /v5/copy-mt5/private/follower/trade-setting/create). _(POST /api/bybit/create/copy/mt5/bind)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `providerMark` | string | Sim |  |
| `investmentE8` | number | Sim |  |

#### `bybit_create_copy_trade_bind`

Create a new Copy Trading Classic follow binding by specifying a target `leaderMark` (POST /v5/copy-trade/private/follower/trade-setting/create). _(POST /api/bybit/create/copy/trade/bind)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `leaderMark` | string | Sim |  |
| `investmentE8` | string | Sim |  |

#### `bybit_create_dca_bot`

Creates a DCA bot that automatically invests at regular intervals. _(POST /api/bybit/create/dca/bot)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `parameters` | string | Sim | Objeto como JSON string, ex.: {...}. |
| `toolsDiscoveryParameter` | string | Não | Objeto como JSON string, ex.: {...}. Opcional. |
| `channel` | string | Não | Opcional. |

#### `bybit_create_f_grid_bot`

Creates a single futures grid trading bot. _(POST /api/bybit/create/f/grid/bot)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `symbol` | string | Sim |  |
| `grid_mode` | string | Sim |  (0, 1, 2, 3) |
| `min_price` | string | Sim |  |
| `max_price` | string | Sim |  |
| `cell_number` | number | Sim |  |
| `leverage` | string | Sim |  |
| `grid_type` | string | Sim |  (0, 1, 2) |
| `total_investment` | string | Sim |  |
| `take_profit_per` | string | Não | Opcional. |
| `stop_loss_per` | string | Não | Opcional. |
| `entry_price` | string | Não | Opcional. |
| `source` | string | Não | Opcional. (0, 1, 2, 3) |
| `followed_grid_id` | number | Não | Opcional. |
| `toolsDiscoveryParameter` | string | Não | Objeto como JSON string, ex.: {...}. Opcional. |
| `stop_loss_price` | string | Não | Opcional. |
| `take_profit_price` | string | Não | Opcional. |
| `tp_sl_type` | string | Não | Opcional. (0, 1, 2, 3, 4) |
| `block_source` | string | Não | Opcional. (0, 1, 2, 3, 4) |
| `create_type` | string | Não | Opcional. (0, 1, 2, 3) |
| `init_bonus` | string | Não | Opcional. |
| `business_remark` | string | Não | Opcional. |
| `trailing_stop_per` | string | Não | Opcional. |
| `move_up_price` | string | Não | Opcional. |
| `move_down_price` | string | Não | Opcional. |
| `channel` | string | Não | Opcional. |
| `followed_grid_ids` | number[] | Não | Bulk mode: multiple values for followed_grid_id |

#### `bybit_create_f_mart_bot`

Creates a futures Martingale trading bot. _(POST /api/bybit/create/f/mart/bot)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `symbol` | string | Sim |  |
| `martingale_mode` | string | Sim |  (F_MART_MODE_MARTINGALE_MODE_UNKNOWN_UNSPECIFIED, F_MART_MODE_MARTINGALE_MODE_LONG, F_MART_MODE_MARTINGALE_MODE_SHORT) |
| `leverage` | string | Sim |  |
| `price_float_percent` | string | Sim |  |
| `add_position_percent` | string | Sim |  |
| `add_position_num` | number | Sim |  |
| `init_margin` | string | Sim |  |
| `round_tp_percent` | string | Sim |  |
| `auto_cycle_toggle` | string | Não | Opcional. (AUTO_CYCLE_TOGGLE_AUTO_CYCLE_TOGGLE_UNKNOWN_UNSPECIFIED, AUTO_CYCLE_TOGGLE_AUTO_CYCLE_TOGGLE_ENABLE, AUTO_CYCLE_TOGGLE_AUTO_CYCLE_TOGGLE_DISABLE) |
| `sl_percent` | string | Não | Opcional. |
| `entry_price` | string | Não | Opcional. |
| `source` | string | Não | Opcional. (F_MART_SOURCE_UNSPECIFIED, F_MART_SOURCE_TRADING_BOT_PAGE, F_MART_SOURCE_DERIVATIVES_PAGE) |
| `followed_bot_id` | number | Não | Opcional. |
| `block_source` | string | Não | Opcional. (BLOCK_SOURCE_UNSPECIFIED, BLOCK_SOURCE_MAIN_PAGE_CREATE_BLOCK, BLOCK_SOURCE_AI_CREATE_BLOCK, BLOCK_SOURCE_RANK_LIST, BLOCK_SOURCE_PAGE_AI_BLOCK) |
| `create_type` | string | Não | Opcional. (CREATE_TYPE_UNSPECIFIED, CREATE_TYPE_COPY, CREATE_TYPE_AUTO, CREATE_TYPE_MANUAL) |
| `init_bonus` | string | Não | Opcional. |
| `channel` | string | Não | Opcional. |
| `followed_bot_ids` | number[] | Não | Bulk mode: multiple values for followed_bot_id |

#### `bybit_create_grid_bot`

Creates a spot grid bot with the specified trading pair, price range, (POST /v5/grid/create-grid). _(POST /api/bybit/create/grid/bot)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `symbol` | string | Sim |  |
| `max_price` | string | Sim |  |
| `min_price` | string | Sim |  |
| `total_investment` | string | Sim |  |
| `cell_number` | number | Sim |  |
| `followed_grid_id` | number | Não | Opcional. |
| `source` | string | Não | Opcional. (1, 2) |
| `entry_price` | string | Não | Opcional. |
| `stop_loss_price` | string | Não | Opcional. |
| `take_profit_price` | string | Não | Opcional. |
| `toolsDiscoveryParameter` | string | Não | Objeto como JSON string, ex.: {...}. Opcional. |
| `base_investment` | string | Não | Opcional. |
| `quote_investment` | string | Não | Opcional. |
| `invest_mode` | string | Não | Opcional. (0, 1, 2) |
| `block_source` | string | Não | Opcional. (0, 1, 2, 3, 4) |
| `create_type` | string | Não | Opcional. (0, 1, 2, 3) |
| `ts_percent` | string | Não | Opcional. |
| `enable_trailing` | boolean | Não | Opcional. |
| `limit_up_price` | string | Não | Opcional. |
| `channel` | string | Não | Opcional. |
| `followed_grid_ids` | number[] | Não | Bulk mode: multiple values for followed_grid_id |

#### `bybit_create_iceberg_strategy`

Creates an Iceberg strategy that splits a large order into multiple smaller child orders, (POST /v5/strategy/create). _(POST /api/bybit/create/iceberg/strategy)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (UTA_USDT, UTA_USDC, UTA_USDC_FUTURE, UTA_SPOT, UTA_INVERSE, UTA_INVERSE_FUTURE, UTA_USDT_FUTURE) |
| `symbol` | string | Sim |  |
| `side` | string | Sim |  (Buy, Sell) |
| `size` | string | Sim |  |
| `strategyType` | string | Não | Opcional. (iceberg) |
| `subSize` | string | Não | Opcional. |
| `orderCount` | number | Não | Opcional. |
| `limitPrice` | string | Não | Opcional. |
| `chaseDistance` | string | Não | Opcional. |
| `chasePercentE4` | number | Não | Opcional. |
| `maxChasePrice` | string | Não | Opcional. |
| `postOnly` | string | Não | Opcional. (0, 1) |
| `reduceOnly` | boolean | Não | Opcional. |
| `positionIdx` | string | Não | Opcional. (0, 1, 2) |
| `leverageType` | string | Não | Opcional. (0, 1) |

#### `bybit_create_order`

Place a new order on the Bybit exchange. _(POST /api/bybit/create/order)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (spot, linear, inverse, option) |
| `symbol` | string | Sim |  |
| `isLeverage` | string | Não | Opcional. (0, 1) |
| `side` | string | Sim |  (Buy, Sell) |
| `orderType` | string | Sim |  (Market, Limit) |
| `qty` | string | Sim |  |
| `marketUnit` | string | Não | Opcional. (baseCoin, quoteCoin) |
| `slippageToleranceType` | string | Não | Opcional. (TickSize, Percent) |
| `slippageTolerance` | string | Não | Opcional. |
| `price` | string | Não | Opcional. |
| `triggerDirection` | string | Não | Opcional. (1, 2) |
| `orderFilter` | string | Não | Opcional. (Order, tpslOrder, StopOrder) |
| `triggerPrice` | string | Não | Opcional. |
| `triggerBy` | string | Não | Opcional. (LastPrice, IndexPrice, MarkPrice) |
| `orderIv` | string | Não | Opcional. |
| `timeInForce` | string | Não | Opcional. (GTC, IOC, FOK, PostOnly, RPI) |
| `positionIdx` | string | Não | Opcional. (0, 1, 2) |
| `orderLinkId` | string | Não | Opcional. |
| `takeProfit` | string | Não | Opcional. |
| `stopLoss` | string | Não | Opcional. |
| `tpTriggerBy` | string | Não | Opcional. (LastPrice, IndexPrice, MarkPrice) |
| `slTriggerBy` | string | Não | Opcional. (LastPrice, IndexPrice, MarkPrice) |
| `reduceOnly` | boolean | Não | Opcional. |
| `closeOnTrigger` | boolean | Não | Opcional. |
| `smpType` | string | Não | Opcional. |
| `mmp` | boolean | Não | Opcional. |
| `tpslMode` | string | Não | Opcional. (Full, Partial) |
| `tpLimitPrice` | string | Não | Opcional. |
| `slLimitPrice` | string | Não | Opcional. |
| `tpOrderType` | string | Não | Opcional. (Market, Limit) |
| `slOrderType` | string | Não | Opcional. (Market, Limit) |
| `bboSideType` | string | Não | Opcional. (Queue, Counterparty) |
| `bboLevel` | string | Não | Opcional. (1, 2, 3, 4, 5) |
| `rpiTakerAccess` | boolean | Não | Opcional. |

#### `bybit_create_quote`

Submit a quote for an existing RFQ. _(POST /api/bybit/create/quote)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `rfqId` | string | Sim |  |
| `quoteLinkId` | string | Não | Opcional. |
| `anonymous` | boolean | Não | Opcional. |
| `expireIn` | number | Não | Opcional. |
| `quoteBuyList` | string | Não | Lista como JSON string, ex.: [{...}]. Opcional. |
| `quoteSellList` | string | Não | Lista como JSON string, ex.: [{...}]. Opcional. |

#### `bybit_create_rfq`

Create a new Request for Quote (RFQ) to solicit pricing from selected counterparties. _(POST /api/bybit/create/rfq)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `counterparties` | string | Sim | Lista como JSON string, ex.: [{...}]. |
| `rfqLinkId` | string | Não | Opcional. |
| `anonymous` | boolean | Não | Opcional. |
| `strategyType` | string | Não | Opcional. |
| `list` | string | Sim | Lista como JSON string, ex.: [{...}]. |

#### `bybit_create_spread_order`

Create a new spread trading order. _(POST /api/bybit/create/spread/order)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `symbol` | string | Sim |  |
| `side` | string | Sim |  (Buy, Sell) |
| `orderType` | string | Sim |  (Limit, Market) |
| `qty` | string | Sim |  |
| `price` | string | Não | Opcional. |
| `orderLinkId` | string | Não | Opcional. |
| `timeInForce` | string | Não | Opcional. (GTC, IOC, FOK, PostOnly) |

#### `bybit_create_twap_strategy`

Creates a TWAP strategy that splits a large order into smaller chunks and executes them (POST /v5/strategy/create). _(POST /api/bybit/create/twap/strategy)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (UTA_USDT, UTA_USDC, UTA_USDC_FUTURE, UTA_SPOT, UTA_INVERSE, UTA_INVERSE_FUTURE, UTA_USDT_FUTURE) |
| `symbol` | string | Sim |  |
| `side` | string | Sim |  (Buy, Sell) |
| `size` | string | Sim |  |
| `strategyType` | string | Não | Opcional. (twap) |
| `duration` | number | Sim |  |
| `interval` | number | Não | Opcional. |
| `isRandom` | boolean | Não | Opcional. |
| `triggerPrice` | string | Não | Opcional. |
| `maxChasePrice` | string | Não | Opcional. |
| `chaseDistance` | string | Não | Opcional. |
| `chasePercentE4` | number | Não | Opcional. |
| `reduceOnly` | boolean | Não | Opcional. |
| `positionIdx` | string | Não | Opcional. (0, 1, 2) |
| `leverageType` | string | Não | Opcional. (0, 1) |

#### `bybit_distribute_award`

Distribute a voucher to a specified user. _(POST /api/bybit/distribute/award)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `accountId` | string | Sim |  |
| `awardId` | string | Sim |  |
| `specCode` | string | Sim |  |
| `amount` | string | Sim |  |
| `brokerId` | string | Sim |  |

#### `bybit_execute_lp_redeem`

Execute LP redemption to withdraw liquidity from a pool position. _(POST /api/bybit/execute/lp/redeem)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `positionId` | number | Sim |  |
| `poolAddress` | string | Sim |  |
| `dercRatio` | string | Sim |  |
| `receiveTokenCode` | string | Não | Opcional. |

#### `bybit_execute_lp_stake`

Execute LP stake to provide liquidity and earn rewards. _(POST /api/bybit/execute/lp/stake)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_execute_prediction_buy`

Execute a buy order for prediction outcome tokens. _(POST /api/bybit/execute/prediction/buy)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `tokenId` | string | Sim |  |
| `amount` | string | Sim |  |
| `payTokenCode` | string | Sim |  |
| `orderType` | string | Sim |  (1) |
| `slippage` | string | Sim |  |
| `eventId` | string | Sim |  |

#### `bybit_execute_prediction_sell`

Execute a sell order for prediction outcome tokens. _(POST /api/bybit/execute/prediction/sell)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `tokenId` | string | Sim |  |
| `size` | string | Sim |  |
| `orderType` | string | Sim |  (1) |
| `slippage` | string | Sim |  |
| `eventId` | string | Sim |  |
| `toTokenCode` | string | Não | Opcional. |

#### `bybit_execute_purchase`

Place a buy order to purchase on-chain tokens with payment tokens. _(POST /api/bybit/execute/purchase)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `fromTokenCode` | string | Sim |  |
| `fromTokenAmount` | string | Sim |  |
| `toTokenCode` | string | Sim |  |
| `slippage` | string | Sim |  |
| `quoteData` | string | Sim |  |
| `gas` | string | Sim |  |
| `quoteMode` | string | Sim |  (0, 1, 2) |
| `correctingCode` | string | Sim |  |
| `tenant` | string | Não | Opcional. |

#### `bybit_execute_quote`

Execute (accept) a quote to initiate the multi-leg trade. _(POST /api/bybit/execute/quote)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `rfqId` | string | Sim |  |
| `quoteId` | string | Sim |  |
| `quoteSide` | string | Sim |  (Buy, Sell) |

#### `bybit_execute_redeem`

Place a sell order to redeem on-chain tokens for payment tokens. _(POST /api/bybit/execute/redeem)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `fromTokenCode` | string | Sim |  |
| `fromTokenAmount` | string | Sim |  |
| `toTokenCode` | string | Sim |  |
| `slippage` | string | Sim |  |
| `quoteData` | string | Sim |  |
| `gas` | string | Sim |  |
| `quoteMode` | string | Sim |  (0, 1, 2) |
| `correctingCode` | string | Sim |  |
| `tenant` | string | Não | Opcional. |

#### `bybit_get_account_info`

Retrieve unified account configuration including margin mode, account status, (GET /v5/account/info). _(POST /api/bybit/get/account/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_get_account_instruments`

Query tradable instrument specifications for the user's account. _(POST /api/bybit/get/account/instruments)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (spot, linear, inverse) |
| `symbol` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_account_withdrawal_info`

Query available withdrawal balance for specified coin(s) in the Unified account. _(POST /api/bybit/get/account/withdrawal/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coinName` | string | Sim |  |

#### `bybit_get_adl_alert`

Query ADL (Auto-Deleveraging) alert data and insurance fund metrics for derivative contracts, (GET /v5/market/adlAlert). _(POST /api/bybit/get/adl/alert)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `symbol` | string | Não | Opcional. |

#### `bybit_get_ads`

Get online P2P advertisements. _(POST /api/bybit/get/ads)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `tokenId` | string | Sim |  |
| `currencyId` | string | Sim |  |
| `side` | string | Sim |  (0, 1) |
| `page` | string | Não | Opcional. |
| `size` | string | Não | Opcional. |

#### `bybit_get_advance_earn_order`

Query your order history. Requires **Earn** permission on the API key. (GET /v5/earn/advance/order). _(POST /api/bybit/get/advance/earn/order)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (DualAssets, SmartLeverage, DoubleWin, DiscountBuy) |
| `productId` | number | Não | Opcional. |
| `orderId` | string | Não | Opcional. |
| `orderLinkId` | string | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_advance_earn_position`

Query your active positions. Requires **Earn** permission on the API key. (GET /v5/earn/advance/position). _(POST /api/bybit/get/advance/earn/position)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (DualAssets, SmartLeverage, DoubleWin, DiscountBuy) |
| `productId` | number | Não | Opcional. |
| `coin` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_advance_earn_product`

Query available Advance Earn product listings. _(POST /api/bybit/get/advance/earn/product)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (DualAssets, SmartLeverage, DoubleWin, DiscountBuy) |
| `coin` | string | Não | Opcional. |
| `duration` | string | Não | Opcional. |

#### `bybit_get_advance_earn_product_extra_info`

Get real-time quotes (target prices and APY) for a specific Dual Assets product. _(POST /api/bybit/get/advance/earn/product/extra/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (DualAssets, SmartLeverage, DoubleWin, DiscountBuy) |
| `productId` | number | Não | Opcional. |

#### `bybit_get_affiliate_user_info`

Query detailed information for a specified direct client user under the affiliate account, (GET /v5/user/aff-customer-info). _(POST /api/bybit/get/affiliate/user/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `uid` | string | Sim |  |

#### `bybit_get_affiliate_user_list`

Query the list of all direct client users under the current affiliate account. _(POST /api/bybit/get/affiliate/user/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `cursor` | string | Não | Opcional. |
| `size` | number | Não | Opcional. |
| `needDeposit` | boolean | Não | Opcional. |
| `need30` | boolean | Não | Opcional. |
| `need365` | boolean | Não | Opcional. |
| `startDate` | string | Não | Opcional. |
| `endDate` | string | Não | Opcional. |

#### `bybit_get_all_orders`

Get a list of P2P orders. Returns 90 days of orders by default. Orders are accessible up to 180 days in the past. (POST /v5/p2p/order/simplifyList). _(POST /api/bybit/get/all/orders)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `page` | number | Sim |  |
| `size` | number | Sim |  |
| `status` | number | Não | Opcional. |
| `beginTime` | string | Não | Opcional. |
| `endTime` | string | Não | Opcional. |
| `tokenId` | string | Não | Opcional. |
| `side` | number | Não | Opcional. |

#### `bybit_get_asset_detail`

Query detailed holding information for a specific token by chain code and token address. _(POST /api/bybit/get/asset/detail)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `chainCode` | string | Sim |  |
| `tokenAddress` | string | Sim |  |

#### `bybit_get_asset_list`

Query user's on-chain token portfolio. _(POST /api/bybit/get/asset/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_get_asset_overview`

Query the total asset overview for the current account, including per-account-type equity breakdowns, category details, and coin-level details. _(POST /api/bybit/get/asset/overview)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `accountType` | string | Não | Opcional. |
| `memberId` | string | Não | Opcional. |
| `valuationCurrency` | string | Não | Opcional. |

#### `bybit_get_aurora_strategy`

Returns the full Aurora AI strategy (params + backtest metrics) identified (POST /v5/aurora/info). _(POST /api/bybit/get/aurora/strategy)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `aurora_id` | string | Sim |  |
| `aurora_ids` | string[] | Não | Bulk mode: multiple values for aurora_id |

#### `bybit_get_award_info`

Get basic information of a specified voucher, including coin, denomination unit, product line, total amount, and distributed amount. _(POST /api/bybit/get/award/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `id` | string | Sim |  |
| `ids` | string[] | Não | Bulk mode: multiple values for id |

#### `bybit_get_biz_token_details`

Query detailed information for a specific on-chain token. _(POST /api/bybit/get/biz/token/details)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `chainCode` | string | Sim |  |
| `tokenAddress` | string | Sim |  |

#### `bybit_get_biz_token_list`

Query on-chain tokens available for trading, optionally filtered by tag. _(POST /api/bybit/get/biz/token/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `tokenTag` | string | Não | Opcional. (0, 1, 2) |

#### `bybit_get_biz_token_price_list`

Batch query token prices and market data by chain code + token address pairs. _(POST /api/bybit/get/biz/token/price/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `tokenAddressInfo` | string | Sim | Lista como JSON string, ex.: [{...}]. |

#### `bybit_get_borrow_history`

Query interest and borrowing records for the unified account. _(POST /api/bybit/get/borrow/history)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `currency` | string | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_chat_messages`

Get chat messages for a P2P order. _(POST /api/bybit/get/chat/messages)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderId` | string | Sim |  |
| `currentPage` | string | Não | Opcional. |
| `size` | string | Sim |  |

#### `bybit_get_close_position`

Query closed option position data including entry/exit prices, fees, delivery details, and realized PnL. _(POST /api/bybit/get/close/position)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (option) |
| `symbol` | string | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_closed_pnl`

Query closed PnL records for the current user. _(POST /api/bybit/get/closed/pnl)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (linear) |
| `symbol` | string | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_coin_greeks`

Query option Greeks aggregated by base coin. _(POST /api/bybit/get/coin/greeks)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `baseCoin` | string | Não | Opcional. |

#### `bybit_get_collateral_info`

Query collateral information including borrowing rates, limits, and collateral (GET /v5/account/collateral-info). _(POST /api/bybit/get/collateral/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `currency` | string | Não | Opcional. |

#### `bybit_get_combo_detail`

Retrieves comprehensive details for a specific futures combo bot, including (POST /v5/fcombobot/detail). _(POST /api/bybit/get/combo/detail)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `bot_id` | number | Sim |  |
| `bot_ids` | number[] | Não | Bulk mode: multiple values for bot_id |

#### `bybit_get_combo_limit`

Validates the input parameters for creating a futures combo bot and returns (POST /v5/fcombobot/getlimit). _(POST /api/bybit/get/combo/limit)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `leverage` | string | Sim |  |
| `init_margin` | string | Sim |  |
| `adjust_position_mode` | string | Sim |  (0, 1, 2, 3, 4, 5, 6) |
| `adjust_position_percent` | string | Não | Opcional. |
| `adjust_position_time_interval` | number | Não | Opcional. |
| `symbol_settings` | string | Sim | Lista como JSON string, ex.: [{...}]. |
| `sl_percent` | string | Não | Opcional. |
| `tp_percent` | string | Não | Opcional. |
| `need_to_slippage` | boolean | Não | Opcional. |
| `app_name` | string | Não | Opcional. |
| `trailing_stop_percent` | string | Não | Opcional. |

#### `bybit_get_copy_trading_classic_leaderboard`

Get a curated Copy Trading Classic leaderboard for conversational (GET /v5/copy-trade/recommend-leader-list). _(POST /api/bybit/get/copy/trading/classic/leaderboard)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_get_copy_trading_trad_fi_leaderboard`

Get a curated Copy Trading TradFi leaderboard for conversational (GET /v5/copy-mt5/recommend-provider-list). _(POST /api/bybit/get/copy/trading/trad/fi/leaderboard)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_get_counterparty_user_info`

Get information about a counterparty user in a specific order. _(POST /api/bybit/get/counterparty/user/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `originalUid` | string | Não | Opcional. |
| `orderId` | string | Não | Opcional. |

#### `bybit_get_crypto_loan_common_adjustment_history`

Query historical collateral adjustment operations with pagination support. _(POST /api/bybit/get/crypto/loan/common/adjustment/history)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `adjustId` | number | Não | Opcional. |
| `collateralCurrency` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | number | Não | Opcional. |

#### `bybit_get_crypto_loan_common_collateral_data`

Query information about currencies available as collateral in the crypto loan system. _(POST /api/bybit/get/crypto/loan/common/collateral/data)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `currency` | string | Não | Opcional. |

#### `bybit_get_crypto_loan_common_loanable_data`

Query information about currencies available for borrowing in the crypto loan system. _(POST /api/bybit/get/crypto/loan/common/loanable/data)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `currency` | string | Não | Opcional. |
| `vipLevel` | string | Não | Opcional. |

#### `bybit_get_crypto_loan_common_max_collateral_amount`

Query the maximum amount of collateral that can be redeemed (withdrawn) for a specific currency. _(POST /api/bybit/get/crypto/loan/common/max/collateral/amount)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `currency` | string | Sim |  |

#### `bybit_get_crypto_loan_common_position`

Query the user's current crypto loan position with comprehensive details. _(POST /api/bybit/get/crypto/loan/common/position)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_get_crypto_loan_fixed_borrow_contract_info`

Query active borrow contracts (loans). _(POST /api/bybit/get/crypto/loan/fixed/borrow/contract/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderId` | string | Não | Opcional. |
| `loanId` | string | Não | Opcional. |
| `orderCurrency` | string | Não | Opcional. |
| `term` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | number | Não | Opcional. |

#### `bybit_get_crypto_loan_fixed_borrow_order_info`

Query borrow order details and history. _(POST /api/bybit/get/crypto/loan/fixed/borrow/order/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderId` | string | Não | Opcional. |
| `orderCurrency` | string | Não | Opcional. |
| `state` | string | Não | Opcional. |
| `term` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | number | Não | Opcional. |

#### `bybit_get_crypto_loan_fixed_borrow_order_quote`

Query available supply orders (lending offers) from the market for a specific currency and term. _(POST /api/bybit/get/crypto/loan/fixed/borrow/order/quote)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderCurrency` | string | Não | Opcional. |
| `term` | string | Não | Opcional. |
| `orderBy` | string | Não | Opcional. (annualRate, qty) |
| `sort` | string | Não | Opcional. (1, 2) |
| `limit` | number | Não | Opcional. |

#### `bybit_get_crypto_loan_fixed_renew_info`

Query loan renewal history and information. _(POST /api/bybit/get/crypto/loan/fixed/renew/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderId` | string | Não | Opcional. |
| `orderCurrency` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | number | Não | Opcional. |

#### `bybit_get_crypto_loan_fixed_repayment_history`

Query loan repayment records. (GET /v5/crypto-loan-fixed/repayment-history). _(POST /api/bybit/get/crypto/loan/fixed/repayment/history)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `repayId` | string | Não | Opcional. |
| `loanCurrency` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | number | Não | Opcional. |

#### `bybit_get_crypto_loan_fixed_supply_contract_info`

Query active supply contracts (lending positions). _(POST /api/bybit/get/crypto/loan/fixed/supply/contract/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderId` | string | Não | Opcional. |
| `supplyId` | string | Não | Opcional. |
| `supplyCurrency` | string | Não | Opcional. |
| `term` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | number | Não | Opcional. |

#### `bybit_get_crypto_loan_fixed_supply_order_info`

Query supply (lending) order details and history. _(POST /api/bybit/get/crypto/loan/fixed/supply/order/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderId` | string | Não | Opcional. |
| `orderCurrency` | string | Não | Opcional. |
| `state` | string | Não | Opcional. |
| `term` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | number | Não | Opcional. |

#### `bybit_get_crypto_loan_fixed_supply_order_quote`

Query available borrow orders (demand) in the market (GET /v5/crypto-loan-fixed/supply-order-quote). _(POST /api/bybit/get/crypto/loan/fixed/supply/order/quote)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderCurrency` | string | Não | Opcional. |
| `term` | string | Não | Opcional. |
| `orderBy` | string | Não | Opcional. |
| `sort` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |

#### `bybit_get_crypto_loan_flexible_borrow_history`

Query historical flexible borrow records with pagination. _(POST /api/bybit/get/crypto/loan/flexible/borrow/history)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderId` | string | Não | Opcional. |
| `loanCurrency` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | number | Não | Opcional. |

#### `bybit_get_crypto_loan_flexible_ongoing_coin`

Query current flexible borrow positions by currency. _(POST /api/bybit/get/crypto/loan/flexible/ongoing/coin)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `loanCurrency` | string | Não | Opcional. |

#### `bybit_get_crypto_loan_flexible_repayment_history`

Query historical flexible repayment records with pagination. _(POST /api/bybit/get/crypto/loan/flexible/repayment/history)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `repayId` | string | Não | Opcional. |
| `loanCurrency` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | number | Não | Opcional. |

#### `bybit_get_dcp_info`

Query Disconnection Protection (DCP) configuration. _(POST /api/bybit/get/dcp/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_get_delivery_price`

Retrieve historical delivery (settlement) prices for expired futures and options contracts, (GET /v5/market/delivery-price). _(POST /api/bybit/get/delivery/price)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (linear, inverse, option) |
| `symbol` | string | Não | Opcional. |
| `baseCoin` | string | Não | Opcional. |
| `settleCoin` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_delivery_record`

Query delivery records of USDC futures, Inverse futures, and Options. _(POST /api/bybit/get/delivery/record)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (linear, inverse, option) |
| `symbol` | string | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `expDate` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_distribution_record`

Query voucher distribution records for a specified user, including claim status, validity period, consumed amount, etc. _(POST /api/bybit/get/distribution/record)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `accountId` | string | Sim |  |
| `awardId` | string | Sim |  |
| `specCode` | string | Sim |  |
| `withUsedAmount` | boolean | Não | Opcional. |

#### `bybit_get_double_win_leverage`

Query the leverage for a Double Win RFQ product with user-selected price range. _(POST /api/bybit/get/double/win/leverage)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `productId` | number | Sim |  |
| `initialPrice` | string | Sim |  |
| `lowerPrice` | string | Sim |  |
| `upperPrice` | string | Sim |  |

#### `bybit_get_earn_apr_history`

Query historical daily APR for a product. _(POST /api/bybit/get/earn/apr/history)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (FlexibleSaving, OnChain) |
| `productId` | string | Sim |  |
| `startTime` | number | Sim |  |
| `endTime` | number | Sim |  |

#### `bybit_get_earn_hourly_yield_history`

Query hourly yield details. Only supports `FlexibleSaving`. (GET /v5/earn/hourly-yield). _(POST /api/bybit/get/earn/hourly/yield/history)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (FlexibleSaving) |
| `productId` | string | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_earn_order_history`

Query stake/redeem order history. _(POST /api/bybit/get/earn/order/history)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (FlexibleSaving, OnChain) |
| `orderId` | string | Não | Opcional. |
| `orderLinkId` | string | Não | Opcional. |
| `productId` | string | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_earn_position`

Query current staked position information. _(POST /api/bybit/get/earn/position)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (FlexibleSaving, OnChain) |
| `productId` | string | Não | Opcional. |
| `coin` | string | Não | Opcional. |

#### `bybit_get_earn_product`

Query earn product information, including estimated APR, min/max stake amount, product status, etc. _(POST /api/bybit/get/earn/product)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (FlexibleSaving, OnChain) |
| `coin` | string | Não | Opcional. |

#### `bybit_get_earn_yield_history`

Query yield history. Supports `FlexibleSaving` and `OnChain`. (GET /v5/earn/yield). _(POST /api/bybit/get/earn/yield/history)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (FlexibleSaving, OnChain) |
| `productId` | number | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_execution_list`

Trade history: execuções efetivamente preenchidas, com preço, quantidade, taxa por trade e se foi maker ou taker. _(POST /api/bybit/get/execution/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim | Tipo de produto. (spot, linear, inverse, option) |
| `symbol` | string | Não | Par, ex.: BTCUSDT. Opcional. |
| `orderId` | string | Não | Filtra as execuções de uma ordem. Opcional. |
| `orderLinkId` | string | Não | Id customizado da ordem. Opcional. |
| `baseCoin` | string | Não | Moeda base. Opcional. |
| `startTime` | number | Não | Início em ms. Opcional. |
| `endTime` | number | Não | Fim em ms, no máximo 7 dias após o início. Opcional. |
| `execType` | string | Não | Tipo de execução, ex.: Trade, Funding, AdlTrade. Opcional. |
| `limit` | number | Não | 1 a 100, default 50. Opcional. |
| `cursor` | string | Não | Cursor de paginação. Opcional. |

#### `bybit_get_f_grid_detail`

Retrieves comprehensive details for a specific futures grid bot, including (POST /v5/fgridbot/detail). _(POST /api/bybit/get/f/grid/detail)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `bot_id` | number | Sim |  |
| `bot_ids` | number[] | Não | Bulk mode: multiple values for bot_id |

#### `bybit_get_f_mart_detail`

Retrieves comprehensive details for a specific futures Martingale bot, including (POST /v5/fmartingalebot/detail). _(POST /api/bybit/get/f/mart/detail)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `bot_id` | number | Sim |  |
| `bot_ids` | number[] | Não | Bulk mode: multiple values for bot_id |

#### `bybit_get_f_mart_limit`

Validates the input parameters for creating a futures Martingale bot and (POST /v5/fmartingalebot/getlimit). _(POST /api/bybit/get/f/mart/limit)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `symbol` | string | Sim |  |
| `martingale_mode` | string | Sim |  (F_MART_MODE_MARTINGALE_MODE_UNKNOWN_UNSPECIFIED, F_MART_MODE_MARTINGALE_MODE_LONG, F_MART_MODE_MARTINGALE_MODE_SHORT) |
| `leverage` | string | Sim |  |
| `price_float_percent` | string | Não | Opcional. |
| `add_position_percent` | string | Não | Opcional. |
| `add_position_num` | number | Não | Opcional. |
| `init_margin` | string | Não | Opcional. |
| `round_tp_percent` | string | Não | Opcional. |
| `sl_percent` | string | Não | Opcional. |
| `entry_price` | string | Não | Opcional. |
| `need_to_slippage` | boolean | Não | Opcional. |
| `app_name` | string | Não | Opcional. |

#### `bybit_get_fee_group_info`

Query the tiered fee structure for Pro-level and Market Maker clients, organized by (GET /v5/market/fee-group-info). _(POST /api/bybit/get/fee/group/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `productType` | string | Sim |  (contract) |
| `groupId` | string | Não | Opcional. (1, 2, 3, 4, 5, 6, 7, 8) |

#### `bybit_get_fee_rate`

Query the maker and taker fee rates for the specified product category. _(POST /api/bybit/get/fee/rate)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (spot, linear, inverse, option) |
| `symbol` | string | Não | Opcional. |
| `baseCoin` | string | Não | Opcional. |

#### `bybit_get_fixed_term_order`

Query fixed term order history. _(POST /api/bybit/get/fixed/term/order)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderType` | string | Não | Opcional. (Stake, Redeem, Reinvest) |
| `productId` | string | Não | Opcional. |
| `category` | string | Não | Opcional. (FixedTermSaving, FundPool, FundPoolPremium) |
| `orderId` | string | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_fixed_term_position`

Query current fixed term position information. _(POST /api/bybit/get/fixed/term/position)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `productId` | string | Não | Opcional. |
| `category` | string | Não | Opcional. (FixedTermSaving, FundPool, FundPoolPremium) |
| `coin` | string | Não | Opcional. |

#### `bybit_get_fixed_term_product`

Query fixed term product information, including tiered APY, min/max stake amount, product status, etc. _(POST /api/bybit/get/fixed/term/product)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coin` | string | Não | Opcional. |

#### `bybit_get_funding_rate_history`

Query historical funding rate records for perpetual contracts. _(POST /api/bybit/get/funding/rate/history)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (linear, inverse) |
| `symbol` | string | Sim |  |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |

#### `bybit_get_historical_interest_rate`

Query historical borrowing interest rate data for UTA spot margin. _(POST /api/bybit/get/historical/interest/rate)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `currency` | string | Sim |  |
| `vipLevel` | string | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |

#### `bybit_get_historical_volatility`

Query historical implied volatility data for options with hourly granularity. _(POST /api/bybit/get/historical/volatility)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (option) |
| `baseCoin` | string | Não | Opcional. |
| `quoteCoin` | string | Não | Opcional. (USD, USDT) |
| `period` | number | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |

#### `bybit_get_hold_to_earn_product`

Query available Hold-to-Earn product listings. _(POST /api/bybit/get/hold/to/earn/product)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_get_hold_to_earn_yield_history`

Query personal yield distribution history for Hold-to-Earn products. _(POST /api/bybit/get/hold/to/earn/yield/history)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `timeStart` | number | Não | Opcional. |
| `timeEnd` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_index_price_components`

Retrieve the component exchanges and trading pairs that make up a Bybit index price, (GET /v5/market/index-price-components). _(POST /api/bybit/get/index/price/components)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `indexName` | string | Sim |  |

#### `bybit_get_index_price_kline`

Query historical index price klines derived from the composite spot price across multiple exchanges. _(POST /api/bybit/get/index/price/kline)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Não | Opcional. (linear, inverse) |
| `symbol` | string | Sim |  |
| `interval` | string | Sim |  (1, 3, 5, 15, 30, 60, 120, 240, 360, 720, D, W, M) |
| `start` | number | Não | Opcional. |
| `end` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |

#### `bybit_get_instruments_info`

Query instrument specifications for active trading pairs across spot, USDT contracts, (GET /v5/market/instruments-info). _(POST /api/bybit/get/instruments/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (spot, linear, inverse, option) |
| `symbol` | string | Não | Opcional. |
| `status` | string | Não | Opcional. (Trading, PreLaunch, Delivering) |
| `baseCoin` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |
| `symbolType` | string | Não | Opcional. (linear, option, spot, xstocks, stock, commodity) |

#### `bybit_get_insurance_pool`

Query Bybit's insurance pool balances and USD-denominated values for various settlement coins. _(POST /api/bybit/get/insurance/pool)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coin` | string | Não | Opcional. |

#### `bybit_get_liquidity_mining_liquidation_records`

Query liquidation records for Liquidity Mining positions with cursor-based pagination. _(POST /api/bybit/get/liquidity/mining/liquidation/records)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `baseCoin` | string | Não | Opcional. |
| `quoteCoin` | string | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_liquidity_mining_orders`

Query Liquidity Mining order history with cursor-based pagination. _(POST /api/bybit/get/liquidity/mining/orders)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderId` | string | Não | Opcional. |
| `orderLinkId` | string | Não | Opcional. |
| `productId` | string | Não | Opcional. |
| `orderType` | string | Não | Opcional. (AddLiquidity, RemoveLiquidity, Reinvest, AddMargin) |
| `status` | string | Não | Opcional. (Success, Processing) |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_liquidity_mining_positions`

Query active Liquidity Mining positions for the current user. _(POST /api/bybit/get/liquidity/mining/positions)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `productId` | string | Não | Opcional. |
| `baseCoin` | string | Não | Opcional. |

#### `bybit_get_liquidity_mining_products`

Query available Liquidity Mining product listings. _(POST /api/bybit/get/liquidity/mining/products)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `baseCoin` | string | Não | Opcional. |
| `quoteCoin` | string | Não | Opcional. |

#### `bybit_get_liquidity_mining_yield_records`

Query yield claim records for Liquidity Mining positions with cursor-based pagination. _(POST /api/bybit/get/liquidity/mining/yield/records)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `baseCoin` | string | Não | Opcional. |
| `quoteCoin` | string | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_long_short_ratio`

Query the net long and short position ratios as percentages of all position holders, (GET /v5/market/account-ratio). _(POST /api/bybit/get/long/short/ratio)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (linear, inverse) |
| `symbol` | string | Sim |  |
| `period` | string | Sim |  (5min, 15min, 30min, 1h, 4h, 1d) |
| `startTime` | string | Não | Opcional. |
| `endTime` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_lp_order_list`

Query the user's LP order history (stake and redeem operations) with optional filters. _(POST /api/bybit/get/lp/order/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderType` | string | Não | Opcional. (0, 1, 2) |
| `tokenCode` | string | Não | Opcional. |
| `orderStatus` | string | Não | Lista como JSON string, ex.: [{...}]. Opcional. |
| `days` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `pageIndex` | number | Não | Opcional. |
| `poolAddress` | string | Não | Opcional. |

#### `bybit_get_lp_pay_token_list`

Query available payment tokens that can be used for LP staking. _(POST /api/bybit/get/lp/pay/token/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `chainCode` | string | Não | Opcional. |
| `tokenAddress` | string | Não | Opcional. |

#### `bybit_get_lp_pay_token_price`

Query current USD prices for one or more payment tokens. _(POST /api/bybit/get/lp/pay/token/price)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `tokenCode` | string | Sim | Lista como JSON string, ex.: [{...}]. |
| `chainCode` | string | Não | Opcional. |

#### `bybit_get_lp_pool_info`

Query detailed pool information including APY breakdown, fees, token reserves, (POST /v5/alpha/lp/pool-info). _(POST /api/bybit/get/lp/pool/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `poolAddress` | string | Sim |  |

#### `bybit_get_lp_pool_list`

Query available liquidity pools with optional filtering by tag and token. _(POST /api/bybit/get/lp/pool/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `tokenSymbol` | string | Não | Opcional. |

#### `bybit_get_lp_position_list`

Query the user's liquidity pool positions with real-time valuation. _(POST /api/bybit/get/lp/position/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_get_mark_price_kline`

Query historical mark price klines used for margin and liquidation calculations in derivative contracts. _(POST /api/bybit/get/mark/price/kline)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Não | Opcional. (linear, inverse) |
| `symbol` | string | Sim |  |
| `interval` | string | Sim |  (1, 3, 5, 15, 30, 60, 120, 240, 360, 720, D, W, M) |
| `start` | number | Não | Opcional. |
| `end` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |

#### `bybit_get_market_kline`

Query historical klines (OHLCV candlestick data) including open, high, low, close, volume, and turnover. _(POST /api/bybit/get/market/kline)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Não | Opcional. (spot, linear, inverse) |
| `symbol` | string | Sim |  |
| `interval` | string | Sim |  (1, 3, 5, 15, 30, 60, 120, 240, 360, 720, D, W, M) |
| `start` | number | Não | Opcional. |
| `end` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |

#### `bybit_get_member_account_type`

Get account type information for specified member IDs. _(POST /api/bybit/get/member/account/type)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `memberIds` | string | Não | Opcional. |

#### `bybit_get_mmp_state`

Query Market Maker Protection configuration and freeze status for the specified (GET /v5/account/mmp-state). _(POST /api/bybit/get/mmp/state)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `baseCoin` | string | Sim |  |

#### `bybit_get_move_position_history`

Query the history of position move (block trade) orders. _(POST /api/bybit/get/move/position/history)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Não | Opcional. (linear, spot, option, inverse) |
| `symbol` | string | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `status` | string | Não | Opcional. (Processing, Filled, Rejected) |
| `blockTradeId` | string | Não | Opcional. |
| `limit` | string | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_my_ad_details`

Get details of a specific P2P advertisement. _(POST /api/bybit/get/my/ad/details)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `itemId` | string | Sim |  |

#### `bybit_get_my_ads`

Get the list of my P2P advertisements. _(POST /api/bybit/get/my/ads)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `itemId` | string | Não | Opcional. |
| `status` | string | Não | Opcional. |
| `side` | string | Não | Opcional. |
| `tokenId` | string | Não | Opcional. |
| `page` | string | Não | Opcional. |
| `size` | string | Não | Opcional. |
| `currencyId` | string | Não | Opcional. |

#### `bybit_get_new_delivery_price`

Retrieve historical option delivery prices grouped by base coin and settlement coin, (GET /v5/market/new-delivery-price). _(POST /api/bybit/get/new/delivery/price)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (option) |
| `baseCoin` | string | Sim |  |
| `settleCoin` | string | Não | Opcional. |

#### `bybit_get_open_interest`

Query historical open interest data for derivative contracts at specified time intervals. _(POST /api/bybit/get/open/interest)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (linear, inverse) |
| `symbol` | string | Sim |  |
| `intervalTime` | string | Sim |  (5min, 15min, 30min, 1h, 4h, 1d) |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_open_orders`

Query real-time unfilled or partially filled orders. _(POST /api/bybit/get/open/orders)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (spot, linear, inverse, option) |
| `symbol` | string | Não | Opcional. |
| `baseCoin` | string | Não | Opcional. |
| `settleCoin` | string | Não | Opcional. |
| `orderId` | string | Não | Opcional. |
| `orderLinkId` | string | Não | Opcional. |
| `openOnly` | string | Não | Opcional. (0, 1) |
| `orderFilter` | string | Não | Opcional. (Order, StopOrder, tpslOrder, OcoOrder, BidirectionalTpslOrder) |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_order_detail`

Get detailed information of a specific P2P order. _(POST /api/bybit/get/order/detail)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderId` | string | Sim |  |

#### `bybit_get_order_history`

Query historical order records. _(POST /api/bybit/get/order/history)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (spot, linear, inverse, option) |
| `symbol` | string | Não | Opcional. |
| `baseCoin` | string | Não | Opcional. |
| `settleCoin` | string | Não | Opcional. |
| `orderId` | string | Não | Opcional. |
| `orderLinkId` | string | Não | Opcional. |
| `orderFilter` | string | Não | Opcional. (Order, StopOrder, tpslOrder, OcoOrder, BidirectionalTpslOrder) |
| `orderStatus` | string | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_order_list`

Query the user's trade order history with optional filters. _(POST /api/bybit/get/order/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `tradeType` | string | Não | Opcional. (0, 1, 2) |
| `tokenCode` | string | Não | Opcional. |
| `orderStatus` | string | Não | Lista como JSON string, ex.: [{...}]. Opcional. |
| `days` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `pageIndex` | number | Não | Opcional. |
| `direction` | string | Não | Opcional. (prev, next) |

#### `bybit_get_order_price_limit`

Retrieve the current allowable price range for order placement, including the maximum (GET /v5/market/price-limit). _(POST /api/bybit/get/order/price/limit)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Não | Opcional. (spot, linear, inverse) |
| `symbol` | string | Sim |  |

#### `bybit_get_orderbook`

Retrieve orderbook depth data for a trading pair. _(POST /api/bybit/get/orderbook)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (spot, linear, inverse, option) |
| `symbol` | string | Sim |  |
| `limit` | number | Não | Opcional. |

#### `bybit_get_pay_token_list`

Query available payment tokens for trading. _(POST /api/bybit/get/pay/token/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `chainCode` | string | Sim |  |
| `tokenAddress` | string | Sim |  |

#### `bybit_get_pending_orders`

Get a list of pending P2P orders. _(POST /api/bybit/get/pending/orders)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `status` | number | Não | Opcional. |
| `beginTime` | string | Não | Opcional. |
| `endTime` | string | Não | Opcional. |
| `tokenId` | string | Não | Opcional. |
| `side` | number | Não | Opcional. |
| `page` | number | Sim |  |
| `size` | number | Sim |  |

#### `bybit_get_portfolio_margin`

Query the portfolio margin information including wallet balance, margin rates, and asset PNL range. _(POST /api/bybit/get/portfolio/margin)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `baseCoin` | string | Não | Opcional. |

#### `bybit_get_position_info`

Query real-time position data such as PnL, leverage, liquidation price, and margin info. _(POST /api/bybit/get/position/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (linear, inverse, option) |
| `symbol` | string | Não | Opcional. |
| `baseCoin` | string | Não | Opcional. |
| `settleCoin` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_position_symbol_info`

Query futures leverage info, such as symbol leverage, side, and position mode. _(POST /api/bybit/get/position/symbol/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (linear, inverse) |
| `symbol` | string | Não | Opcional. |

#### `bybit_get_position_tiers`

Query position tier data for spot margin trading. _(POST /api/bybit/get/position/tiers)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `currency` | string | Não | Opcional. |

#### `bybit_get_prediction_engine_status`

Query whether the prediction market matching engine is currently available. _(POST /api/bybit/get/prediction/engine/status)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_get_prediction_event_detail`

Get detailed information about a prediction event, including all associated markets, (POST /v5/alpha/prediction/event-detail). _(POST /api/bybit/get/prediction/event/detail)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `eventId` | string | Não | Opcional. |
| `slug` | string | Não | Opcional. |
| `hasMoreMarkets` | boolean | Não | Opcional. |

#### `bybit_get_prediction_group_stage_detail`

Query detailed standings and match results for a specific tournament stage. _(POST /api/bybit/get/prediction/group/stage/detail)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `eventType` | string | Sim |  (1) |
| `stageCode` | string | Sim |  (Groups, R32, R16, QF, SF, Final) |

#### `bybit_get_prediction_match_list`

Query all matches for a sports event with their current status and prediction market info. _(POST /api/bybit/get/prediction/match/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `eventType` | string | Sim |  (1) |

#### `bybit_get_prediction_order_book`

Query the full order book (bid/ask depth) for prediction outcome tokens. _(POST /api/bybit/get/prediction/order/book)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `tokenIds` | string | Sim | Lista como JSON string, ex.: [{...}]. |

#### `bybit_get_prediction_order_estimate`

Get estimated execution details for a prediction market order before placing it. _(POST /api/bybit/get/prediction/order/estimate)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `tokenId` | string | Sim |  |
| `side` | string | Sim |  (1, 2) |
| `eventId` | string | Sim |  |
| `amount` | string | Sim |  |
| `orderType` | string | Sim |  (1) |
| `payTokenCode` | string | Não | Opcional. |

#### `bybit_get_prediction_order_list`

Query the authenticated user's prediction market order history. _(POST /api/bybit/get/prediction/order/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `status` | string | Não | Opcional. (1, 2, 3, 4, 5) |
| `tokenId` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `pageIndex` | number | Não | Opcional. |
| `eventId` | string | Não | Opcional. |
| `side` | string | Não | Opcional. (1, 2) |
| `days` | number | Não | Opcional. |

#### `bybit_get_prediction_pay_token_list`

Query available payment tokens for prediction market trading. _(POST /api/bybit/get/prediction/pay/token/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_get_prediction_portfolio_summary`

Query an aggregated summary of the authenticated user's prediction market portfolio. _(POST /api/bybit/get/prediction/portfolio/summary)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_get_prediction_position_history`

Query the authenticated user's historical prediction positions that have been (POST /v5/alpha/prediction/position-history). _(POST /api/bybit/get/prediction/position/history)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `limit` | number | Não | Opcional. |
| `pageIndex` | number | Não | Opcional. |
| `direction` | string | Não | Opcional. (prev, next) |

#### `bybit_get_prediction_position_list`

Query the authenticated user's current open prediction positions. _(POST /api/bybit/get/prediction/position/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `limit` | number | Não | Opcional. |
| `pageIndex` | number | Não | Opcional. |
| `direction` | string | Não | Opcional. (prev, next) |

#### `bybit_get_prediction_price_history`

Query historical price data for prediction outcome tokens. _(POST /api/bybit/get/prediction/price/history)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `tokenIds` | string | Não | Lista como JSON string, ex.: [{...}]. Opcional. |
| `eventId` | string | Não | Opcional. |
| `interval` | string | Sim |  (1H, 6H, 1D, 1W, 1M, ALL) |
| `fidelity` | number | Não | Opcional. |

#### `bybit_get_prediction_side_market_list`

Query the list of side/related markets for a specific sports event type. _(POST /api/bybit/get/prediction/side/market/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `eventType` | string | Sim |  (1) |

#### `bybit_get_prediction_timeline_stages`

Query the tournament stages timeline for a sports prediction event. _(POST /api/bybit/get/prediction/timeline/stages)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `eventType` | string | Não | Opcional. |

#### `bybit_get_prediction_token_price`

Query current market prices for up to 20 prediction outcome tokens. _(POST /api/bybit/get/prediction/token/price)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `tokenIds` | string | Sim | Lista como JSON string, ex.: [{...}]. |

#### `bybit_get_premium_index_price_kline`

Query historical premium index price klines, representing the basis between mark price and index price (GET /v5/market/premium-index-price-kline). _(POST /api/bybit/get/premium/index/price/kline)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Não | Opcional. (linear) |
| `symbol` | string | Sim |  |
| `interval` | string | Sim |  (1, 3, 5, 15, 30, 60, 120, 240, 360, 720, D, W, M) |
| `start` | number | Não | Opcional. |
| `end` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |

#### `bybit_get_public_trades`

Query publicly available RFQ trade data with optional time range filtering (GET /v5/rfq/public-trades). _(POST /api/bybit/get/public/trades)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_quotes`

Query historical quotes with optional filtering by IDs, trader type, and status. _(POST /api/bybit/get/quotes)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `rfqId` | string | Não | Opcional. |
| `quoteId` | string | Não | Opcional. |
| `quoteLinkId` | string | Não | Opcional. |
| `traderType` | string | Não | Opcional. (quote, request) |
| `status` | string | Não | Opcional. (Active, Canceled, PendingFill, Filled, Expired, Failed) |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_quotes_realtime`

Query quotes in real-time from the RFQ engine. _(POST /api/bybit/get/quotes/realtime)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `rfqId` | string | Não | Opcional. |
| `quoteId` | string | Não | Opcional. |
| `quoteLinkId` | string | Não | Opcional. |
| `traderType` | string | Não | Opcional. (quote, request) |

#### `bybit_get_recent_public_trades`

Query recent public trading history for a symbol, returning execution records with (GET /v5/market/recent-trade). _(POST /api/bybit/get/recent/public/trades)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (spot, linear, inverse, option) |
| `symbol` | string | Não | Opcional. |
| `baseCoin` | string | Não | Opcional. |
| `optionType` | string | Não | Opcional. (Call, Put) |
| `limit` | number | Não | Opcional. |

#### `bybit_get_reference_price`

Query the reference exchange rate for a specified trading pair. _(POST /api/bybit/get/reference/price)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `symbol` | string | Sim |  |
| `paymentMethod` | string | Não | Opcional. |

#### `bybit_get_rfq_config`

Retrieve the RFQ configuration for the authenticated account, including available counterparties, (GET /v5/rfq/config). _(POST /api/bybit/get/rfq/config)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_get_rfqs`

Query historical RFQs with optional filtering by ID, trader type, and status. _(POST /api/bybit/get/rfqs)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `rfqId` | string | Não | Opcional. |
| `rfqLinkId` | string | Não | Opcional. |
| `traderType` | string | Não | Opcional. (quote, request) |
| `status` | string | Não | Opcional. (Active, Canceled, Filled, Expired, Failed) |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_rfqs_realtime`

Query RFQs in real-time from the RFQ engine. _(POST /api/bybit/get/rfqs/realtime)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `rfqId` | string | Não | Opcional. |
| `rfqLinkId` | string | Não | Opcional. |
| `traderType` | string | Não | Opcional. (quote, request) |

#### `bybit_get_risk_limit`

Query tiered risk limit parameters for perpetual and futures contracts, including (GET /v5/market/risk-limit). _(POST /api/bybit/get/risk/limit)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (linear, inverse) |
| `symbol` | string | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_rpi_orderbook`

Retrieve orderbook depth data that explicitly shows RPI (Retail Price Improvement) order sizes (GET /v5/market/rpi_orderbook). _(POST /api/bybit/get/rpi/orderbook)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Não | Opcional. (spot, linear, inverse) |
| `symbol` | string | Sim |  |
| `limit` | number | Sim |  |

#### `bybit_get_rwa_nav_chart`

Query historical NAV (Net Asset Value) data points for an RWA product. _(POST /api/bybit/get/rwa/nav/chart)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_get_rwa_order_list`

Query RWA order history. Supports exact lookup by `orderId` or `orderLinkId`, (GET /v5/earn/rwa/order). _(POST /api/bybit/get/rwa/order/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderId` | string | Não | Opcional. |
| `orderLinkId` | string | Não | Opcional. |
| `orderType` | string | Não | Opcional. (Stake, Redeem) |
| `productId` | number | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_rwa_position_list`

Query the user's RWA holding positions, including effective shares, (GET /v5/earn/rwa/position). _(POST /api/bybit/get/rwa/position/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_get_rwa_product_list`

Query the list of RWA products, including base APR, bonus APR, NAV, stake limits, (GET /v5/earn/rwa/product). _(POST /api/bybit/get/rwa/product/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coin` | string | Não | Opcional. |

#### `bybit_get_server_time`

Query Bybit server time, returned in both seconds and nanoseconds precision. _(POST /api/bybit/get/server/time)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_get_settlement_record`

Query session settlement records of USDC perpetual contracts. _(POST /api/bybit/get/settlement/record)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (linear) |
| `symbol` | string | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_smart_leverage_redeem_est_amount_list`

Query the estimated redemption amount for one or more Smart Leverage / Double Win positions. _(POST /api/bybit/get/smart/leverage/redeem/est/amount/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (SmartLeverage, DoubleWin) |
| `positionIds` | string | Sim | Lista como JSON string, ex.: [{...}]. |

#### `bybit_get_smp_group`

Query the Self-Matching Prevention (SMP) group ID associated with the account. _(POST /api/bybit/get/smp/group)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_get_spot_borrow_quota`

Query the borrowing quota for spot margin trading. _(POST /api/bybit/get/spot/borrow/quota)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (spot) |
| `symbol` | string | Sim |  |
| `side` | string | Sim |  (Buy, Sell) |

#### `bybit_get_spot_margin_trade_auto_repay_mode`

Retrieve the current automatic repayment mode settings for margin trading accounts. _(POST /api/bybit/get/spot/margin/trade/auto/repay/mode)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `currency` | string | Não | Opcional. |

#### `bybit_get_spot_margin_trade_coin_state`

Retrieve spot margin leverage information for cryptocurrencies. _(POST /api/bybit/get/spot/margin/trade/coin/state)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `currency` | string | Não | Opcional. |

#### `bybit_get_spot_margin_trade_flexible_available_inventory`

Retrieve the flexible available inventory (remaining borrowable amount from the lending pool) for a specified cryptocurrency in spot margin trading. _(POST /api/bybit/get/spot/margin/trade/flexible/available/inventory)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `currency` | string | Sim |  |

#### `bybit_get_spot_margin_trade_max_borrowable`

Retrieve the maximum borrowable amount for a specified cryptocurrency in spot margin trading. _(POST /api/bybit/get/spot/margin/trade/max/borrowable)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `currency` | string | Sim |  |

#### `bybit_get_spot_margin_trade_repayment_available_amount`

Retrieve the available amount that can be repaid for a specific cryptocurrency in spot margin trading. _(POST /api/bybit/get/spot/margin/trade/repayment/available/amount)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `currency` | string | Sim |  |

#### `bybit_get_spot_margin_trade_state`

Query the Spot margin status and leverage of the unified account. _(POST /api/bybit/get/spot/margin/trade/state)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_get_spread_instruments_info`

Query instrument specifications for spread combination trading pairs, including (GET /v5/spread/instrument). _(POST /api/bybit/get/spread/instruments/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `symbol` | string | Não | Opcional. |
| `baseCoin` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_spread_max_qty`

Query the spread wallet available balance for a given symbol and side. _(POST /api/bybit/get/spread/max/qty)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `symbol` | string | Sim |  |
| `side` | string | Sim |  (1, 2) |
| `orderPrice` | string | Sim |  |

#### `bybit_get_spread_open_orders`

Query real-time open spread trading orders. _(POST /api/bybit/get/spread/open/orders)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `symbol` | string | Não | Opcional. |
| `baseCoin` | string | Não | Opcional. |
| `orderId` | string | Não | Opcional. |
| `orderLinkId` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_spread_order_history`

Query historical spread trading orders including filled, cancelled, and rejected orders. _(POST /api/bybit/get/spread/order/history)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `symbol` | string | Não | Opcional. |
| `baseCoin` | string | Não | Opcional. |
| `orderId` | string | Não | Opcional. |
| `orderLinkId` | string | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_spread_orderbook`

Retrieve spread orderbook depth data for a specific spread combination symbol. _(POST /api/bybit/get/spread/orderbook)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `symbol` | string | Sim |  |
| `limit` | number | Não | Opcional. |

#### `bybit_get_spread_recent_trades`

Query recent public spread trading history for a specific spread combination symbol. _(POST /api/bybit/get/spread/recent/trades)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `symbol` | string | Sim |  |
| `limit` | number | Não | Opcional. |

#### `bybit_get_spread_tickers`

Retrieve the latest price snapshot, best bid/ask price, and 24-hour trading (GET /v5/spread/tickers). _(POST /api/bybit/get/spread/tickers)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `symbol` | string | Sim |  |

#### `bybit_get_spread_trade_history`

Query spread trading execution (trade) history, including individual leg execution details. _(POST /api/bybit/get/spread/trade/history)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `symbol` | string | Não | Opcional. |
| `orderId` | string | Não | Opcional. |
| `orderLinkId` | string | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_tickers`

Retrieve the latest price snapshot, best bid/ask price, and 24-hour trading statistics (GET /v5/market/tickers). _(POST /api/bybit/get/tickers)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (spot, linear, inverse, option) |
| `symbol` | string | Não | Opcional. |
| `baseCoin` | string | Não | Opcional. |
| `expDate` | string | Não | Opcional. |

#### `bybit_get_tiered_collateral_ratio`

Query UTA loan tiered collateral ratio for spot margin trading. _(POST /api/bybit/get/tiered/collateral/ratio)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `currency` | string | Não | Opcional. |

#### `bybit_get_token_daily_yield`

Query user's daily yield distribution records. _(POST /api/bybit/get/token/daily/yield)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coin` | string | Sim |  (BYUSDT) |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |

#### `bybit_get_token_historical_apr`

Query product's historical APR data. _(POST /api/bybit/get/token/historical/apr)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coin` | string | Sim |  (BYUSDT) |
| `range` | string | Sim |  (1, 2, 3) |

#### `bybit_get_token_hourly_yield`

Query user's hourly yield calculation records (distributed yields). _(POST /api/bybit/get/token/hourly/yield)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coin` | string | Sim |  (BYUSDT) |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |

#### `bybit_get_token_order_list`

Query BYUSDT Token order history. _(POST /api/bybit/get/token/order/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coin` | string | Sim |  (BYUSDT) |
| `orderLinkId` | string | Não | Opcional. |
| `orderId` | string | Não | Opcional. |
| `orderType` | string | Não | Opcional. (Mint, Redeem) |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |

#### `bybit_get_token_position`

Query user's BYUSDT Token position and yield summary. _(POST /api/bybit/get/token/position)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coin` | string | Sim |  (BYUSDT) |

#### `bybit_get_token_product`

Query BYUSDT Token product details, including user's FlexibleSaving balance, (GET /v5/earn/token/product). _(POST /api/bybit/get/token/product)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coin` | string | Sim |  (BYUSDT) |

#### `bybit_get_total_members_assets`

Query the aggregated total assets overview for parent and sub accounts. _(POST /api/bybit/get/total/members/assets)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coin` | string | Não | Opcional. |

#### `bybit_get_trade_history`

Query RFQ trade execution history with optional filtering by IDs, trader type, and status. _(POST /api/bybit/get/trade/history)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `rfqId` | string | Não | Opcional. |
| `rfqLinkId` | string | Não | Opcional. |
| `quoteId` | string | Não | Opcional. |
| `quoteLinkId` | string | Não | Opcional. |
| `traderType` | string | Não | Opcional. (quote, request) |
| `status` | string | Não | Opcional. (Filled, Failed) |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_trade_quote`

Get a price quote before executing a purchase or redeem trade. _(POST /api/bybit/get/trade/quote)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `tradeType` | string | Sim |  (1, 2) |
| `fromTokenCode` | string | Sim |  |
| `fromTokenAmount` | string | Sim |  |
| `toTokenCode` | string | Sim |  |
| `quoteMode` | string | Não | Opcional. (0, 1, 2) |

#### `bybit_get_transaction_log`

Query unified account wallet transaction logs. _(POST /api/bybit/get/transaction/log)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `accountType` | string | Não | Opcional. (UNIFIED) |
| `category` | string | Não | Opcional. (spot, linear, option, inverse) |
| `currency` | string | Não | Opcional. |
| `baseCoin` | string | Não | Opcional. |
| `type` | string | Não | Opcional. |
| `transSubType` | string | Não | Opcional. (movePosition) |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_get_user_payment`

Get your payment methods configured in P2P. _(POST /api/bybit/get/user/payment)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_get_user_setting_config`

Query the user account setting configuration, including margin mode, account mode, spot hedging status, and other account-level settings. _(POST /api/bybit/get/user/setting/config)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_get_vasp_list`

Query the list of available VASPs (Virtual Asset Service Providers). _(POST /api/bybit/get/vasp/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_get_vip_margin_data`

Query margin data for Unified accounts by VIP level and/or coin. _(POST /api/bybit/get/vip/margin/data)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `vipLevel` | string | Não | Opcional. |
| `currency` | string | Não | Opcional. |

#### `bybit_get_wallet_balance`

Obtain wallet balance, query asset information of each currency, and each currency carries the risk rate of the current position. _(POST /api/bybit/get/wallet/balance)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `accountType` | string | Sim |  (UNIFIED) |
| `coin` | string | Não | Opcional. |

#### `bybit_get_withdrawable_amount_by_coin`

Get the withdrawable amount for a specific coin across different account types. _(POST /api/bybit/get/withdrawable/amount/by/coin)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coin` | string | Sim |  |

#### `bybit_ins_loan_coin_delta_amount`

Query coin delta amount details for institutional lending hedge product. _(POST /api/bybit/ins/loan/coin/delta/amount)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coin` | string | Não | Opcional. |

#### `bybit_ins_loan_product_infos`

Get institutional loan product information including leverage, risk lines, and trading pair whitelists. _(POST /api/bybit/ins/loan/product/infos)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `productId` | string | Não | Opcional. |

#### `bybit_inter_transfer_list_query`

Query the internal transfer records between different account types under the same UID. _(POST /api/bybit/inter/transfer/list/query)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `transferId` | string | Não | Opcional. |
| `coin` | string | Não | Opcional. |
| `status` | string | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_list_accounts`

Lista as contas Bybit conectadas a este install, com id e label. _(POST /api/bybit/list/accounts)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_list_earn_coupons`

Query the user's interest-rate coupons (`interestCards`) and Dual Assets reward cards (GET /v5/earn/coupons). _(POST /api/bybit/list/earn/coupons)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (FlexibleSaving, DualAssets) |

#### `bybit_list_sub_api_keys_v5`

Query all API keys of a sub-account with pagination support. _(POST /api/bybit/list/sub/api/keys/v5)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `subuid` | number | Sim |  |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_mark_order_as_paid`

Mark a P2P order as paid. (POST /v5/p2p/order/pay). [write, mexe em dinheiro na sua conta Bybit] _(POST /api/bybit/mark/order/as/paid)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderId` | string | Sim |  |
| `paymentType` | string | Sim |  |
| `paymentId` | string | Sim |  |

#### `bybit_modify_earn_position`

Set or unset auto-reinvest for a fixed-term OnChain position (`SavingType=FixedTermSaving`). _(POST /api/bybit/modify/earn/position)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (OnChain) |
| `productId` | number | Sim |  |
| `positionId` | number | Sim |  |
| `autoReinvest` | string | Sim |  (0, 1) |

#### `bybit_move_position`

Transfer positions between two unified trading accounts (UIDs) without fees. _(POST /api/bybit/move/position)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `fromUid` | string | Sim |  |
| `toUid` | string | Sim |  |
| `list` | string | Sim | Lista como JSON string, ex.: [{...}]. |

#### `bybit_place_advance_earn_order`

Place a Dual Assets staking order. _(POST /api/bybit/place/advance/earn/order)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (DualAssets, SmartLeverage, DoubleWin, DiscountBuy) |
| `productId` | number | Sim |  |
| `orderType` | string | Sim |  (Stake, Redeem) |
| `amount` | string | Sim |  |
| `accountType` | string | Sim |  (FUND, UNIFIED) |
| `coin` | string | Sim |  |
| `orderLinkId` | string | Sim |  |
| `dualAssetsExtra` | string | Não | Objeto como JSON string, ex.: {...}. Opcional. |
| `interestCard` | string | Não | Objeto como JSON string, ex.: {...}. Opcional. |
| `smartLeverageStakeExtra` | string | Não | Objeto como JSON string, ex.: {...}. Opcional. |
| `smartLeverageRedeemExtra` | string | Não | Objeto como JSON string, ex.: {...}. Opcional. |
| `doubleWinStakeExtra` | string | Não | Objeto como JSON string, ex.: {...}. Opcional. |
| `doubleWinRedeemExtra` | string | Não | Objeto como JSON string, ex.: {...}. Opcional. |
| `discountBuyExtra` | string | Não | Objeto como JSON string, ex.: {...}. Opcional. |

#### `bybit_place_earn_order`

Place a Stake or Redeem order. _(POST /api/bybit/place/earn/order)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (FlexibleSaving, OnChain) |
| `orderType` | string | Sim |  (Stake, Redeem) |
| `accountType` | string | Sim |  (FUND, UNIFIED) |
| `amount` | string | Sim |  |
| `coin` | string | Sim |  |
| `productId` | string | Sim |  |
| `orderLinkId` | string | Sim |  |
| `redeemPositionId` | string | Não | Opcional. |
| `toAccountType` | string | Não | Opcional. (FUND, UNIFIED) |
| `interestCard` | string | Não | Objeto como JSON string, ex.: {...}. Opcional. |

#### `bybit_place_fixed_term_order`

Place a staking order for a fixed term product. _(POST /api/bybit/place/fixed/term/order)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `productId` | string | Sim |  |
| `category` | string | Sim |  (FixedTermSaving, FundPool, FundPoolPremium) |
| `coin` | string | Sim |  |
| `amount` | string | Sim |  |
| `accountType` | string | Sim |  (FUND, UNIFIED) |
| `orderLinkId` | string | Sim |  |
| `autoInvest` | boolean | Não | Opcional. |

#### `bybit_place_rwa_order`

Place a Stake (subscription) or Redeem order for an RWA product. _(POST /api/bybit/place/rwa/order)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_place_token_order`

Place a Mint (minting) or Redeem (redemption) order for BYUSDT Token. _(POST /api/bybit/place/token/order)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coin` | string | Sim |  (BYUSDT) |
| `orderLinkId` | string | Sim |  |
| `orderType` | string | Sim |  (Mint, Redeem) |
| `amount` | string | Sim |  |
| `accountType` | string | Sim |  (FlexibleSaving, UNIFIED) |

#### `bybit_post_ad`

Create a new P2P advertisement. _(POST /api/bybit/post/ad)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `tokenId` | string | Sim |  |
| `currencyId` | string | Sim |  |
| `side` | string | Sim |  (0, 1) |
| `priceType` | string | Sim |  (0, 1) |
| `premium` | string | Sim |  |
| `price` | string | Sim |  |
| `minAmount` | string | Sim |  |
| `maxAmount` | string | Sim |  |
| `remark` | string | Sim |  |
| `tradingPreferenceSet` | string | Sim | Objeto como JSON string, ex.: {...}. |
| `paymentIds` | string | Sim | Lista como JSON string, ex.: [{...}]. |
| `quantity` | string | Sim |  |
| `paymentPeriod` | string | Sim |  |
| `itemType` | string | Sim |  (ORIGIN, BULK) |

#### `bybit_post_crypto_loan_common_adjust_ltv`

Adjust the amount of collateral for a specific currency to manage the LTV ratio. _(POST /api/bybit/post/crypto/loan/common/adjust/ltv)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `currency` | string | Sim |  |
| `amount` | string | Sim |  |
| `direction` | string | Sim |  (1, 2) |

#### `bybit_post_crypto_loan_common_max_loan`

Calculate the maximum amount that can be borrowed for a specific currency based on provided collateral. _(POST /api/bybit/post/crypto/loan/common/max/loan)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `currency` | string | Sim |  |
| `collateralList` | string | Sim | Lista como JSON string, ex.: [{...}]. |

#### `bybit_post_crypto_loan_fixed_borrow`

Create a fixed-term borrow order with specified loan currency, amount, rate, term, and collateral. _(POST /api/bybit/post/crypto/loan/fixed/borrow)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderCurrency` | string | Sim |  |
| `orderAmount` | string | Sim |  |
| `annualRate` | string | Sim |  |
| `term` | string | Sim |  (7, 14, 30, 60, 90, 180) |
| `autoRepay` | string | Não | Opcional. (0, 1) |
| `collateralList` | string | Sim | Lista como JSON string, ex.: [{...}]. |
| `repayType` | string | Não | Opcional. |

#### `bybit_post_crypto_loan_fixed_borrow_order_cancel`

Cancel a pending borrow order. _(POST /api/bybit/post/crypto/loan/fixed/borrow/order/cancel)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderId` | string | Sim |  |

#### `bybit_post_crypto_loan_fixed_fully_repay`

Repay entire loan principal and interest. _(POST /api/bybit/post/crypto/loan/fixed/fully/repay)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `loanId` | string | Sim |  |
| `loanCurrency` | string | Sim |  |

#### `bybit_post_crypto_loan_fixed_renew`

Renew an existing loan by creating a new loan to repay the old one. _(POST /api/bybit/post/crypto/loan/fixed/renew)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `loanId` | string | Sim |  |
| `collateralList` | string | Sim | Lista como JSON string, ex.: [{...}]. |

#### `bybit_post_crypto_loan_fixed_repay_collateral`

Repay loan by converting collateral to loan currency. _(POST /api/bybit/post/crypto/loan/fixed/repay/collateral)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `loanId` | number | Sim |  |
| `loanCurrency` | string | Sim |  |
| `collateralCoin` | string | Sim |  |
| `amount` | string | Sim |  |

#### `bybit_post_crypto_loan_fixed_supply`

Lend crypto to earn fixed interest. _(POST /api/bybit/post/crypto/loan/fixed/supply)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderCurrency` | string | Sim |  |
| `orderAmount` | string | Sim |  |
| `annualRate` | string | Sim |  |
| `term` | string | Sim |  |
| `availableSource` | string | Não | Opcional. (0, 1, 2) |

#### `bybit_post_crypto_loan_fixed_supply_order_cancel`

Cancel a pending supply (lending) order. _(POST /api/bybit/post/crypto/loan/fixed/supply/order/cancel)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderId` | string | Sim |  |
| `refundedAccount` | string | Não | Opcional. (0, 1) |

#### `bybit_post_crypto_loan_flexible_borrow`

Borrow crypto with flexible hourly interest rates. _(POST /api/bybit/post/crypto/loan/flexible/borrow)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `loanCurrency` | string | Sim |  |
| `loanAmount` | string | Sim |  |
| `collateralList` | string | Sim | Lista como JSON string, ex.: [{...}]. |

#### `bybit_post_crypto_loan_flexible_repay`

Repay flexible loan with loan currency. _(POST /api/bybit/post/crypto/loan/flexible/repay)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `loanCurrency` | string | Sim |  |
| `amount` | string | Sim |  |

#### `bybit_post_crypto_loan_flexible_repay_collateral`

Repay loan by converting collateral to loan currency. _(POST /api/bybit/post/crypto/loan/flexible/repay/collateral)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `loanCurrency` | string | Sim |  |
| `collateralCoin` | string | Sim |  |
| `amount` | string | Sim |  |

#### `bybit_pre_check_order`

Validate an order before placing it to check margin requirements. _(POST /api/bybit/pre/check/order)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (linear, option) |
| `symbol` | string | Sim |  |
| `side` | string | Sim |  (Buy, Sell) |
| `orderType` | string | Sim |  (Market, Limit) |
| `qty` | string | Sim |  |
| `price` | string | Não | Opcional. |
| `isLeverage` | string | Não | Opcional. (0, 1) |
| `timeInForce` | string | Não | Opcional. (GTC, IOC, FOK, PostOnly) |
| `positionIdx` | string | Não | Opcional. (0, 1, 2) |
| `orderLinkId` | string | Não | Opcional. |
| `takeProfit` | string | Não | Opcional. |
| `stopLoss` | string | Não | Opcional. |
| `tpTriggerBy` | string | Não | Opcional. (LastPrice, IndexPrice, MarkPrice) |
| `slTriggerBy` | string | Não | Opcional. (LastPrice, IndexPrice, MarkPrice) |
| `reduceOnly` | boolean | Não | Opcional. |
| `tpslMode` | string | Não | Opcional. (Full, Partial) |
| `tpLimitPrice` | string | Não | Opcional. |
| `slLimitPrice` | string | Não | Opcional. |
| `tpOrderType` | string | Não | Opcional. (Market, Limit) |
| `slOrderType` | string | Não | Opcional. (Market, Limit) |
| `orderIv` | string | Não | Opcional. |

#### `bybit_query_api_key`

Query comprehensive information about an API key. _(POST /api/bybit/query/api/key)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_query_balance`

Query fiat or crypto account balances. _(POST /api/bybit/query/balance)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `accountCategory` | string | Não | Opcional. (fiat, crypto) |
| `currency` | string | Não | Opcional. |

#### `bybit_query_borrow_liability`

Query the borrow liability breakdown for a specific coin, including fixed-rate and flexible-rate liabilities. _(POST /api/bybit/query/borrow/liability)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `currency` | string | Sim |  |

#### `bybit_query_broker_account_info`

Use exchange broker master account to query account information. _(POST /api/bybit/query/broker/account/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_query_broker_all_uid_details`

Use the master account to query for all your UID-level rate limits, including all master accounts and subaccounts. _(POST /api/bybit/query/broker/all/uid/details)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `uids` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_query_broker_cap`

Get your exchange broker account entity total rate limit usage and cap, across the board. _(POST /api/bybit/query/broker/cap)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_query_broker_earning`

Use exchange broker master account to query earnings and rebate information. _(POST /api/bybit/query/broker/earning)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `bizType` | string | Não | Opcional. (SPOT, DERIVATIVES, OPTIONS, CONVERT) |
| `begin` | string | Não | Opcional. |
| `end` | string | Não | Opcional. |
| `uid` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_query_card_asset_records`

Query Bybit Card asset (transaction) records for the authenticated account. _(POST /api/bybit/query/card/asset/records)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `statusCode` | string | Não | Opcional. (0, 1, 2) |
| `limit` | number | Não | Opcional. |
| `page` | number | Não | Opcional. |
| `pan4` | string | Não | Opcional. |
| `createBeginTime` | number | Não | Opcional. |
| `createEndTime` | number | Não | Opcional. |
| `merchName` | string | Não | Opcional. |
| `type` | string | Não | Opcional. (SIDE_QUERY_AUTH, SIDE_QUERY_FINANCIAL, SIDE_QUERY_REFUND) |
| `txnId` | string | Não | Opcional. |
| `cardToken` | string | Não | Opcional. |
| `orderNo` | string | Não | Opcional. |

#### `bybit_query_coin_chain_info`

Query coin information, including chain configuration, deposit and withdrawal status. _(POST /api/bybit/query/coin/chain/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coin` | string | Não | Opcional. |

#### `bybit_query_coin_list`

Query the list of supported fiat currencies and cryptocurrencies. _(POST /api/bybit/query/coin/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `side` | string | Não | Opcional. (0, 1) |

#### `bybit_query_deposit_address`

Query the deposit address information for the master account. _(POST /api/bybit/query/deposit/address)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coin` | string | Sim |  |
| `chainType` | string | Não | Opcional. |

#### `bybit_query_deposit_records`

Query on-chain deposit records (GET /v5/asset/deposit/query-record). _(POST /api/bybit/query/deposit/records)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `id` | string | Não | Opcional. |
| `txID` | string | Não | Opcional. |
| `coin` | string | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |
| `ids` | string[] | Não | Bulk mode: multiple values for id |

#### `bybit_query_escrow_sub_members_v5`

Query escrow (fund management) sub-accounts in paginated format. _(POST /api/bybit/query/escrow/sub/members/v5)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `nextCursor` | number | Não | Opcional. |
| `pageSize` | number | Não | Opcional. |

#### `bybit_query_fixed_available_inventory`

Query available inventory for fixed-rate borrowing by specifying currency, term, and annual rate. _(POST /api/bybit/query/fixed/available/inventory)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `currency` | string | Sim |  |
| `term` | string | Sim |  |
| `annualRate` | string | Sim |  |

#### `bybit_query_fixed_borrow_contracts`

Query fixed-rate borrow contracts (matched loan details). _(POST /api/bybit/query/fixed/borrow/contracts)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderId` | string | Não | Opcional. |
| `orderCurrency` | string | Não | Opcional. |
| `term` | string | Não | Opcional. |
| `limit` | string | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_query_fixed_borrow_market`

Query the fixed-rate borrow market (supply order book) to see available lending offers. _(POST /api/bybit/query/fixed/borrow/market)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderCurrency` | string | Sim |  |
| `term` | string | Não | Opcional. |
| `orderBy` | string | Sim |  (apy, term, quantity) |
| `sort` | string | Não | Opcional. (0, 1) |
| `limit` | number | Não | Opcional. |

#### `bybit_query_fixed_borrow_orders`

Query fixed-rate borrow order history. _(POST /api/bybit/query/fixed/borrow/orders)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `orderId` | string | Não | Opcional. |
| `orderCurrency` | string | Não | Opcional. |
| `state` | string | Não | Opcional. (1, 2, 3, 4) |
| `term` | string | Não | Opcional. |
| `limit` | string | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_query_funding_detail_api`

Query transaction records of the funding account. _(POST /api/bybit/query/funding/detail/api)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `createTimeFrom` | string | Não | Opcional. |
| `createTimeTo` | string | Não | Opcional. |
| `limit` | string | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_query_grid_detail`

Retrieves comprehensive details of a spot grid bot including symbol, (POST /v5/grid/query-grid-detail). _(POST /api/bybit/query/grid/detail)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `grid_id` | number | Sim |  |
| `grid_ids` | number[] | Não | Bulk mode: multiple values for grid_id |

#### `bybit_query_internal_deposit_records`

Query deposit records occurring **within the Bybit platform** (not on blockchain). _(POST /api/bybit/query/internal/deposit/records)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `txID` | string | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `coin` | string | Não | Opcional. |
| `cursor` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `status` | string | Não | Opcional. |

#### `bybit_query_order_by_page`

Aggregates asset account and OBU account data, queries conversion history orders by cursor pagination. _(POST /api/bybit/query/order/by/page)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `cursor` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `toCoin` | string | Não | Opcional. |
| `fromCoin` | string | Não | Opcional. |

#### `bybit_query_order_from_open_api`

Paginated query of conversion order list via OpenAPI, supports asset account and OBU account data. _(POST /api/bybit/query/order/from/open/api)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `accountType` | string | Não | Opcional. (0, 1) |
| `cursor` | string | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `toCoin` | string | Não | Opcional. |
| `fromCoin` | string | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `type` | string | Não | Opcional. (0, 1, 2) |
| `exchangeStatus` | string | Não | Opcional. (0, 1, 2, 3, 4) |
| `direction` | string | Não | Opcional. (next, prev) |

#### `bybit_query_referral_code`

Query the referral codes owned by the current user and their corresponding referral registration links. _(POST /api/bybit/query/referral/code)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_query_referrals`

Query invited users (referrals) for the authenticated account. _(POST /api/bybit/query/referrals)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `cursor` | string | Não | Opcional. |
| `size` | number | Não | Opcional. |
| `status` | string | Não | Lista como JSON string, ex.: [{...}]. Opcional. |

#### `bybit_query_result`

Query cryptocurrency exchange results using a quote transaction ID. _(POST /api/bybit/query/result)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `quoteTxId` | string | Sim |  |
| `accountType` | string | Sim |  |

#### `bybit_query_small_asset_convert_order`

Paginated query of small asset conversion history records. _(POST /api/bybit/query/small/asset/convert/order)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `accountType` | string | Não | Opcional. (eb_convert_uta, eb_convert_funding) |
| `quoteId` | string | Não | Opcional. |
| `cursor` | string | Não | Opcional. |
| `size` | string | Não | Opcional. |
| `startTime` | string | Não | Opcional. |
| `endTime` | string | Não | Opcional. |

#### `bybit_query_small_asset_list`

Query small-balance coins eligible for dust conversion in the account, and supported to-coins. _(POST /api/bybit/query/small/asset/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `accountType` | string | Sim |  |
| `fromCoin` | string | Não | Opcional. |

#### `bybit_query_strategy_list`

Retrieve a list of strategies with filtering options and pagination support. _(POST /api/bybit/query/strategy/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `strategyId` | string | Não | Opcional. |
| `status` | string | Não | Opcional. (2, 3, 4, 5, 6) |
| `symbol` | string | Não | Opcional. |
| `category` | string | Não | Opcional. (UTA_USDT, UTA_USDC, UTA_USDC_FUTURE, UTA_SPOT, UTA_INVERSE, UTA_INVERSE_FUTURE, UTA_USDT_FUTURE) |
| `strategyType` | string | Não | Opcional. (twap, chaseOrder, iceberg, pov) |
| `beginTimeE0` | number | Não | Opcional. |
| `endTimeE0` | number | Não | Opcional. |
| `pageSize` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_query_strategy_order_list`

Retrieve a list of child orders created by a strategy with detailed execution information. _(POST /api/bybit/query/strategy/order/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `strategyId` | string | Sim |  |
| `status` | string | Não | Opcional. (1, 2, 3, 4, 5) |
| `symbol` | string | Não | Opcional. |
| `BeginTimeE0` | number | Não | Opcional. |
| `EndTimeE0` | number | Não | Opcional. |
| `pageSize` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |
| `StrategyType` | string | Não | Opcional. (twap, chaseOrder, iceberg, pov) |

#### `bybit_query_sub_member_deposit_address`

Query deposit address for a sub-account. _(POST /api/bybit/query/sub/member/deposit/address)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coin` | string | Sim |  |
| `chainType` | string | Sim |  |
| `subMemberId` | string | Sim |  |

#### `bybit_query_sub_member_deposit_records`

Query on-chain deposit records for a sub-account using the **main** UID API key. _(POST /api/bybit/query/sub/member/deposit/records)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `id` | string | Não | Opcional. |
| `txID` | string | Não | Opcional. |
| `subMemberId` | string | Sim |  |
| `coin` | string | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |
| `ids` | string[] | Não | Bulk mode: multiple values for id |

#### `bybit_query_sub_members`

Get a complete list of all sub-accounts under the master account. _(POST /api/bybit/query/sub/members)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_query_sub_members_v5`

Query all sub-accounts of the master account with pagination support. _(POST /api/bybit/query/sub/members/v5)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `pageSize` | number | Não | Opcional. |
| `nextCursor` | number | Não | Opcional. |

#### `bybit_query_trade`

Query detailed information and status of a specified trade. _(POST /api/bybit/query/trade)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `tradeNo` | string | Não | Opcional. |
| `merchantRequestId` | string | Não | Opcional. |

#### `bybit_query_trade_history`

Query historical trade records with pagination support. _(POST /api/bybit/query/trade/history)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `index` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `startTime` | string | Não | Opcional. |
| `endTime` | string | Não | Opcional. |

#### `bybit_query_withdraw_addresses`

Retrieve withdrawal addresses from the address book. _(POST /api/bybit/query/withdraw/addresses)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coin` | string | Não | Opcional. |
| `chain` | string | Não | Opcional. |
| `addressType` | string | Não | Opcional. (0, 1, 2) |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_query_withdraw_records`

Query withdrawal records. (GET /v5/asset/withdraw/query-record). _(POST /api/bybit/query/withdraw/records)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `withdrawID` | string | Não | Opcional. |
| `txID` | string | Não | Opcional. |
| `coin` | string | Não | Opcional. |
| `withdrawType` | string | Não | Opcional. (0, 1, 2) |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_quick_repayment`

Execute quick repayment for specified coin (POST /v5/account/quick-repayment). _(POST /api/bybit/quick/repayment)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coin` | string | Não | Opcional. |

#### `bybit_quote_apply`

Apply for a conversion quote via OpenAPI, get conversion rate and quote ID. _(POST /api/bybit/quote/apply)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `requestId` | string | Não | Opcional. |
| `accountType` | string | Sim |  |
| `fromCoin` | string | Sim |  |
| `fromCoinType` | string | Não | Opcional. |
| `toCoin` | string | Sim |  |
| `toCoinType` | string | Não | Opcional. |
| `requestAmount` | string | Sim |  |
| `requestCoin` | string | Sim |  |
| `paramType` | string | Não | Opcional. |
| `paramValue` | string | Não | Opcional. |

#### `bybit_rec_aurora_creation_ai_params`

Returns the strategies Aurora recommends when a user is on the bot (POST /v5/aurora/creation). _(POST /api/bybit/rec/aurora/creation/ai/params)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `biz_type` | string | Sim |  (0, 1, 2, 3, 4, 5, 6, 7, 8) |
| `symbol` | string | Sim |  |

#### `bybit_rec_aurora_home_ai_params`

Returns a curated list of Aurora AI strategy recommendations for the (POST /v5/aurora/home). _(POST /api/bybit/rec/aurora/home/ai/params)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_rec_easy_bot_strategy`

Returns a single Aurora-recommended strategy plus the bot business type (POST /v5/aurora/easy). _(POST /api/bybit/rec/easy/bot/strategy)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `symbol` | string | Sim |  |
| `product` | string | Sim |  (0, 1, 2) |
| `direction` | string | Sim |  (0, 1, 2, 3) |

#### `bybit_rec_explore_strategy`

Returns up to 6 Aurora-recommended strategies for a given `biz_type`, (POST /v5/aurora/explore). _(POST /api/bybit/rec/explore/strategy)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `biz_type` | string | Sim |  (0, 1, 2, 3, 4, 5, 6, 7, 8) |

#### `bybit_redeem_fixed_term`

Early redemption for a fixed term position. _(POST /api/bybit/redeem/fixed/term)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `productId` | string | Sim |  |
| `category` | string | Sim |  (FixedTermSaving, FundPool, FundPoolPremium) |
| `positionId` | string | Sim |  |

#### `bybit_reinvest_liquidity`

Reinvest accumulated interest back into an existing Liquidity Mining position. _(POST /api/bybit/reinvest/liquidity)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `productId` | string | Sim |  |
| `orderLinkId` | string | Sim |  |
| `positionId` | string | Sim |  |

#### `bybit_remove_ad`

Cancel/remove a P2P advertisement. _(POST /api/bybit/remove/ad)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `itemId` | string | Sim |  |

#### `bybit_remove_liquidity`

Withdraw funds from a Liquidity Mining pool position. _(POST /api/bybit/remove/liquidity)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `productId` | string | Sim |  |
| `orderLinkId` | string | Sim |  |
| `positionId` | string | Sim |  |
| `removeRate` | number | Não | Opcional. |
| `removeType` | string | Não | Opcional. (Normal, SingleQuoteCoin, SingleBaseCoin) |

#### `bybit_renew_fixed_borrow`

Renew (extend) an existing fixed-rate borrow contract. _(POST /api/bybit/renew/fixed/borrow)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `loanId` | string | Sim |  |
| `qty` | string | Não | Opcional. |

#### `bybit_reset_mmp`

Reset MMP freeze state and clear trading history counters. _(POST /api/bybit/reset/mmp)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `baseCoin` | string | Sim |  |

#### `bybit_set_auto_add_margin`

Toggle the auto-add-margin feature for a position. _(POST /api/bybit/set/auto/add/margin)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (linear) |
| `symbol` | string | Sim |  |
| `autoAddMargin` | string | Sim |  (0, 1) |
| `positionIdx` | string | Não | Opcional. (0, 1, 2) |

#### `bybit_set_auto_repay_mode`

Set spot automatic repayment mode. _(POST /api/bybit/set/auto/repay/mode)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `currency` | string | Não | Opcional. |
| `autoRepayMode` | string | Sim |  (0, 1) |

#### `bybit_set_batch_collateral_switch`

Batch enable or disable multiple coins as collateral (POST /v5/account/set-collateral-switch-batch). _(POST /api/bybit/set/batch/collateral/switch)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `request` | string | Sim | Lista como JSON string, ex.: [{...}]. |

#### `bybit_set_broker_api_limit`

Set API rate limit for specified UIDs under exchange broker account. _(POST /api/bybit/set/broker/api/limit)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `list` | string | Não | Lista como JSON string, ex.: [{...}]. Opcional. |

#### `bybit_set_collateral_switch`

Enable or disable specified coin as collateral (POST /v5/account/set-collateral-switch). _(POST /api/bybit/set/collateral/switch)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `coin` | string | Sim |  |
| `collateralSwitch` | string | Sim |  (ON, OFF) |

#### `bybit_set_dcp`

Configure the time window for automatic order cancellation when WebSocket connection drops. _(POST /api/bybit/set/dcp)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `product` | string | Não | Opcional. (OPTIONS, DERIVATIVES, SPOT) |
| `timeWindow` | number | Sim |  |

#### `bybit_set_default_deposit_to_account`

Set the default account type for receiving on-chain deposit funds. _(POST /api/bybit/set/default/deposit/to/account)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `accountType` | string | Sim |  (UNIFIED, FUND) |

#### `bybit_set_fixed_term_auto_invest`

Enable or disable auto-reinvestment for a fixed term position. _(POST /api/bybit/set/fixed/term/auto/invest)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `productId` | string | Sim |  |
| `category` | string | Sim |  (FixedTermSaving, FundPool, FundPoolPremium) |
| `positionId` | string | Sim |  |
| `status` | string | Sim |  (Enable, Disable) |

#### `bybit_set_hedging_mode`

Enable or disable PM include spot hedging mode (POST /v5/account/set-hedging-mode). _(POST /api/bybit/set/hedging/mode)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `setHedgingMode` | string | Sim |  (ON, OFF) |

#### `bybit_set_leverage`

Set the leverage for a contract position. _(POST /api/bybit/set/leverage)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (linear, inverse) |
| `symbol` | string | Sim |  |
| `buyLeverage` | string | Sim |  |
| `sellLeverage` | string | Sim |  |

#### `bybit_set_margin_mode`

Set the account margin mode. Supports ISOLATED_MARGIN, REGULAR_MARGIN, and (POST /v5/account/set-margin-mode). [write, mexe em dinheiro na sua conta Bybit] _(POST /api/bybit/set/margin/mode)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `setMarginMode` | string | Sim |  (ISOLATED_MARGIN, REGULAR_MARGIN, PORTFOLIO_MARGIN) |

#### `bybit_set_mmp`

Configure Market Maker Protection parameters for options trading. _(POST /api/bybit/set/mmp)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `baseCoin` | string | Sim |  |
| `window` | string | Sim |  |
| `frozenPeriod` | string | Sim |  |
| `qtyLimit` | string | Sim |  |
| `deltaLimit` | string | Sim |  |

#### `bybit_set_price_limit`

Configure price limit action behavior per product category. _(POST /api/bybit/set/price/limit)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (linear, inverse, spot) |
| `modifyEnable` | boolean | Sim |  |

#### `bybit_set_trading_stop`

Configure trading stop parameters including take profit, stop loss, and trailing stop. _(POST /api/bybit/set/trading/stop)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (linear, inverse) |
| `symbol` | string | Sim |  |
| `takeProfit` | string | Não | Opcional. |
| `stopLoss` | string | Não | Opcional. |
| `trailingStop` | string | Não | Opcional. |
| `tpTriggerBy` | string | Não | Opcional. (MarkPrice, IndexPrice, LastPrice) |
| `slTriggerBy` | string | Não | Opcional. (MarkPrice, IndexPrice, LastPrice) |
| `activePrice` | string | Não | Opcional. |
| `tpslMode` | string | Sim |  (Full, Partial) |
| `tpSize` | string | Não | Opcional. |
| `slSize` | string | Não | Opcional. |
| `tpLimitPrice` | string | Não | Opcional. |
| `slLimitPrice` | string | Não | Opcional. |
| `tpOrderType` | string | Não | Opcional. (Market, Limit) |
| `slOrderType` | string | Não | Opcional. (Market, Limit) |
| `positionIdx` | string | Sim |  (0, 1, 2) |

#### `bybit_small_asset_convert`

Confirm and execute small asset conversion using the quoteId returned by the get-quote interface. _(POST /api/bybit/small/asset/convert)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `quoteId` | string | Sim |  |

#### `bybit_small_asset_quote`

Apply for batch conversion quote for a small asset list. _(POST /api/bybit/small/asset/quote)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `accountType` | string | Sim |  |
| `toCoin` | string | Sim |  |
| `fromCoinList` | string | Sim | Lista como JSON string, ex.: [{...}]. |

#### `bybit_spot_margin_set_leverage`

Set the maximum leverage for spot cross margin trading. _(POST /api/bybit/spot/margin/set/leverage)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `leverage` | string | Sim |  |
| `currency` | string | Não | Opcional. |

#### `bybit_spot_margin_switch_mode`

Enable or disable spot cross margin trading mode, rate limit 5/user/path/s (POST /v5/spot-margin-trade/switch-mode). _(POST /api/bybit/spot/margin/switch/mode)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `spotMarginMode` | string | Sim |  (0, 1) |

#### `bybit_stop_strategy`

Terminates an active strategy and cancels all associated pending orders. _(POST /api/bybit/stop/strategy)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `strategyId` | string | Sim |  |

#### `bybit_sub_member_list_query`

Query sub UIDs under the current master UID. _(POST /api/bybit/sub/member/list/query)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |

#### `bybit_switch_position_mode`

Switch between one-way mode (mode=0) and hedge mode (mode=3). _(POST /api/bybit/switch/position/mode)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `category` | string | Sim |  (linear) |
| `symbol` | string | Não | Opcional. |
| `coin` | string | Não | Opcional. |
| `mode` | string | Sim |  (0, 3) |

#### `bybit_transfer_coin_list_query`

Query the list of coins that can be transferred between the specified account types. _(POST /api/bybit/transfer/coin/list/query)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `fromAccountType` | string | Sim |  |
| `toAccountType` | string | Sim |  |

#### `bybit_universal_transfer_list_query`

Query universal transfer records. _(POST /api/bybit/universal/transfer/list/query)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `transferId` | string | Não | Opcional. |
| `coin` | string | Não | Opcional. |
| `status` | string | Não | Opcional. |
| `startTime` | number | Não | Opcional. |
| `endTime` | number | Não | Opcional. |
| `limit` | number | Não | Opcional. |
| `cursor` | string | Não | Opcional. |

#### `bybit_update_ad`

Update or relist a P2P advertisement. _(POST /api/bybit/update/ad)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `id` | string | Sim |  |
| `priceType` | string | Sim |  (0, 1) |
| `premium` | string | Sim |  |
| `price` | string | Sim |  |
| `minAmount` | string | Sim |  |
| `maxAmount` | string | Sim |  |
| `remark` | string | Sim |  |
| `tradingPreferenceSet` | string | Sim | Objeto como JSON string, ex.: {...}. |
| `paymentIds` | string | Sim | Lista como JSON string, ex.: [{...}]. |
| `actionType` | string | Sim |  (MODIFY, ACTIVE) |
| `quantity` | string | Sim |  |
| `paymentPeriod` | string | Sim |  |
| `ids` | string[] | Não | Bulk mode: multiple values for id |

#### `bybit_user_asset_info_query`

Query coin balances across a single account type. _(POST /api/bybit/user/asset/info/query)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `accountType` | string | Sim |  |
| `coin` | string | Não | Opcional. |
| `memberId` | number | Não | Opcional. |
| `withBonus` | string | Não | Opcional. (0, 1) |

#### `bybit_validate_f_grid_input`

Validates the input parameters for creating a futures grid bot and returns (POST /v5/fgridbot/validate). _(POST /api/bybit/validate/f/grid/input)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `symbol` | string | Sim |  |
| `cell_number` | number | Sim |  |
| `min_price` | string | Sim |  |
| `max_price` | string | Sim |  |
| `leverage` | string | Sim |  |
| `grid_type` | string | Sim |  (0, 1, 2) |
| `grid_mode` | string | Sim |  (0, 1, 2, 3) |
| `stop_loss_price` | string | Não | Opcional. |
| `take_profit_price` | string | Não | Opcional. |
| `tp_sl_type` | string | Não | Opcional. (0, 1, 2, 3, 4) |
| `entry_price` | string | Não | Opcional. |
| `stop_loss_per` | string | Não | Opcional. |
| `take_profit_per` | string | Não | Opcional. |
| `trailing_stop_per` | string | Não | Opcional. |
| `init_margin` | string | Não | Opcional. |
| `move_up_price` | string | Não | Opcional. |
| `move_down_price` | string | Não | Opcional. |

#### `bybit_validate_grid_input`

Validates the input parameters for creating a spot grid bot, returning (POST /v5/grid/validate-input). _(POST /api/bybit/validate/grid/input)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas Bybit conectadas: id ou label da conexão. Veja bybit_list_accounts. |
| `symbol` | string | Sim |  |
| `cell_number` | number | Sim |  |
| `min_price` | string | Sim |  |
| `max_price` | string | Sim |  |
| `total_investment` | string | Sim |  |
| `stop_loss` | string | Não | Opcional. |
| `take_profit` | string | Não | Opcional. |
| `entry_price` | string | Não | Opcional. |
| `base_investment` | string | Não | Opcional. |
| `quote_investment` | string | Não | Opcional. |
| `invest_mode` | string | Não | Opcional. (0, 1, 2) |
| `ts_percent` | string | Não | Opcional. |
| `enable_trailing` | boolean | Não | Opcional. |
| `limit_up_price` | string | Não | Opcional. |

---

Este MCP também funciona via **conexão MCP** (Claude / Cursor) em `https://api.mcp.ai/p_bybit` — veja o [README](../../README.md). A skill acima é pra consumir a **REST API** direto (agente próprio / código).
