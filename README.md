# Integration Manual – Domain Resolution

This document explains how to use the **Domain Resolution** API, which allows you to transform a domain or subdomain name into technical information such as the destination address and derivation path.

---

## 📌 Endpoint

**GET** `/domain/resolve/{domainName}`

Resolves domains and subdomains, returning information such as:
- Second-level domain
- Top-level domain
- Subdomain
- Target value (address)
- Derivation path

**Base URL**:  
```
https://api.address.services
```

Full documentation:  
[Swagger UI](https://api.address.services/swagger/static/index.html)

---

## 🔹 Parameters

| Name         | Type   | Location | Required | Description                                |
|--------------|--------|----------|----------|--------------------------------------------|
| domainName   | string | path     | Yes      | Domain or subdomain name to be resolved    |

---

## 🔹 Request Example

```http
GET /domain/resolve/mydomain.btc
Host: api.address.services
Accept: application/json
```

---

## 🔹 Responses

### **200 - Success**
```json
{
  "secondLevelDomain": "mydomain",
  "topLevelDomain": "btc",
  "targetValue": "walletAddress | xpub | anotherValue",
  "derivationPath": "m/44'/0'/0'/0/0"
}
```

### **400 - Bad Request**
```json
{
  "statusCode": "400",
  "error": "Bad Request",
  "message": "Invalid domain"
}
```

### **503 - Service Unavailable**
```json
{
  "statusCode": "503",
  "error": "Service Unavailable",
  "message": "Service temporarily unavailable"
}
```

---

## 🔹 How to Use

1. Send a **GET** request to the endpoint, providing the domain in the path (`{domainName}`).
2. Check the response code:
   - **200**: Success – use the returned data to process the address.
   - **400**: Request error – check the provided domain.
   - **503**: Service temporarily unavailable – try again later.
3. Use `targetValue` as the destination address and, if necessary, `derivationPath` to generate keys or addresses.

---

## 🔹 Best Practices

- **Validation**: Always validate the domain format before making the request.
- **Error handling**: Implement handling for `400` and `503` status codes.
- **Performance**: Consider caching recurring results to reduce repeated calls.

---

## 📄 Notes

- The API supports domain and subdomain resolution.
- The `derivationPath` is useful for wallets or systems that need to generate addresses from the domain.
- The response may vary depending on the domain configuration.
