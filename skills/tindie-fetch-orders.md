---
name: Fetch Tindie seller orders
description: Retrieve an authenticated seller's orders and order line items from the Tindie API.
api: openapi/tindie-openapi.yml
operations: [listOrders, getOrder, listOrderItems]
---

# Fetch Tindie seller orders

Retrieve the authenticated seller's own orders. Requires a Tindie API key.

## Auth

Send `api_key` and `username` as query parameters, or the header
`Authorization: ApiKey <username>:<api_key>`. Without valid credentials these
endpoints return **401** (verified live). See authentication/tindie-authentication.yml.

## Steps

1. **List orders** — call `listOrders` (`GET /order/`) with your credentials.
   Page with `limit`/`offset`; read `meta.total_count`.
2. **Get one order** — call `getOrder` (`GET /order/{id}/`) for a single order.
3. **List order items** — call `listOrderItems` (`GET /orderitem/`) to enumerate
   line items across orders; each item references its order and product.

## Conventions

- Same Tastypie limit/offset pagination and `resource_uri` self-links as the
  product resource.
- Handle 401 by re-checking the `api_key`/`username` pair; there is no token
  refresh (static API key).
