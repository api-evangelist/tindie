---
name: Browse Tindie products
description: Search and retrieve public product listings from a Tindie store, including pre-order status and pricing.
api: openapi/tindie-openapi.yml
operations: [listProducts, getProduct]
---

# Browse Tindie products

Use the public Tindie product resource — no authentication required.

## Steps

1. **List products** — call `listProducts` (`GET /product/`). Filter with `id`
   (or `id__in=1,2,3`) and `pre_order=true`; page with `limit` (default 20) and
   `offset`. Read `meta.total_count` and `meta.next` to paginate.
2. **Read a listing** — for each object use `title`, `unit_price` (decimal
   string), `state`, `category`, `store_username`, and `url`. `pre_order`,
   `pre_order_percentage`, and `amount_raised` describe crowd-funded listings.
3. **Fetch one product** — call `getProduct` (`GET /product/{id}/`) using the
   `id` (or resolve `resource_uri`) for full detail.

## Conventions

- Pagination is Tastypie limit/offset; `meta` holds `total_count`/`next`/`previous`.
- Every object carries a `resource_uri` self-link.
- Errors return `{ "error_message": ... }` with the HTTP status (see
  errors/tindie-problem-types.yml).
