# Retrieve a customer

Retrieves the details of an existing customer using the customer's unique ID.

## Endpoint

`GET /api/v1/customers/{customer_id}`

## Authentication

This endpoint requires API key authentication.

Include your API key in the request header:

`Authorization: Bearer <API_KEY>`

For more information, see [Authentication](authentication.md).

## Path parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `customer_id` | String | Yes | The unique identifier of the customer. |

## Request headers

| Header | Required | Description |
|---|---|---|
| `Authorization` | Yes | Bearer token used to authenticate the request. |
| `Accept` | No | Specifies the response format. The default is `application/json`. |

## Request example

The following example retrieves the details of customer `CUST-1001`.

```bash
curl -X GET \
  "https://api.pulsedesk.example.com/api/v1/customers/CUST-1001" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Accept: application/json"
```

## Response

A successful request returns HTTP status code `200 OK` and the customer details.

### Sample response

```json
{
  "id": "CUST-1001",
  "name": "John Smith",
  "email": "john.smith@example.com",
  "status": "active",
  "created_at": "2026-10-15T10:30:00Z"
}
```

### Response fields

| Field | Type | Description |
|---|---|---|
| `id` | String | Unique customer identifier. |
| `name` | String | Full name of the customer. |
| `email` | String | Customer's email address. |
| `status` | String | Customer account status. Possible values: `active`, `inactive`. |
| `created_at` | String | Date and time when the customer account was created, in ISO 8601 format. |

## Error responses

The API returns an error response when a request cannot be completed.

| HTTP status code | Error | Description |
|---|---|---|
| `400` | Bad Request | The request contains invalid parameters. |
| `401` | Unauthorized | The API key is missing or invalid. |
| `404` | Not Found | No customer exists with the specified ID. |
| `429` | Too Many Requests | The API request limit has been exceeded. |
| `500` | Internal Server Error | An unexpected server error occurred. |

### Sample error response

```json
{
  "error": {
    "code": "CUSTOMER_NOT_FOUND",
    "message": "No customer found with ID CUST-9999."
  }
}
```

## Rate limits

The endpoint supports a maximum of 100 requests per minute per API key.

If you exceed this limit, the API returns HTTP status code `429 Too Many Requests`.

Wait before retrying the request.

## Related topics

- [Authentication](authentication.md)
- [Create a customer](create-customer.md)
- [Update a customer](update-customer.md)
- [Delete a customer](delete-customer.md)