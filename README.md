

# **Lattice: Massive Off-Chain Payment Protocol API Documentation**

This document provides a comprehensive guide to the **Lattice API**, detailing its structure, functionality, and implementation for developers. The API enables seamless interaction with the Lattice protocol for decentralized payments.

---

## **1. Introduction**

The **Lattice API** facilitates secure and efficient communication between client applications and the Lattice payment protocol. It offers capabilities such as:

- **Payment Initialization**: Automate peer-to-peer and merchant payments.
- **Transaction Status Monitoring**: Retrieve real-time updates on transactions.
- **Cross-Chain Functionality**: Support for multiple blockchain networks.
- **Identity Integration**: Use Decentralized Identifiers (DIDs) for authentication.

This API is RESTful and supports both synchronous and asynchronous operations.

---

## **2. Authentication**

### **2.1 API Key**
All requests to the Lattice API require an API key for authentication. To obtain an API key:
1. Sign up on the [Lattice Dashboard](https://dashboard.lattice.org).
2. Generate an API key under the "API Access" section.

Include the key in the request header:
```
Authorization: Bearer YOUR_API_KEY
```

---

## **3. API Endpoints**

### **3.1 Payment Initialization**
**Endpoint**: `/payments/initiate`  
**Method**: `POST`

**Description**: Creates a new payment request.

**Headers**:
```json
{
  "Authorization": "Bearer YOUR_API_KEY",
  "Content-Type": "application/json"
}
```

**Body Parameters**:
| Parameter      | Type    | Required | Description                                  |
|----------------|---------|----------|----------------------------------------------|
| `recipient`    | String  | Yes      | Blockchain address of the payment recipient.|
| `amount`       | Decimal | Yes      | Amount to transfer.                         |
| `currency`     | String  | Yes      | Currency to use (e.g., ETH, BTC).           |
| `metadata`     | Object  | No       | Custom metadata for the payment.            |

**Sample Request**:
```json

POST /payments/initiate
{
  "recipient": "0x1234567890abcdef",
  "amount": 10.5,
  "currency": "ETH",
  "metadata": {
    "orderId": "ORD12345",
    "note": "Payment for services"
  }
}
```

**Response**:
```json
{
  "status": "success",
  "transactionId": "tx_abcdef1234567890",
  "message": "Payment initiated successfully"
}
```

---

### **3.2 Retrieve Payment Status**
**Endpoint**: `/payments/{transactionId}/status`  
**Method**: `GET`

**Description**: Fetches the current status of a payment.

**Path Parameters**:
| Parameter        | Type   | Required | Description                           |
|------------------|--------|----------|---------------------------------------|
| `transactionId`  | String | Yes      | The unique ID of the transaction.    |

**Headers**:
```json
{
  "Authorization": "Bearer YOUR_API_KEY"
}
```

**Sample Request**:
```http
GET /payments/tx_abcdef1234567890/status
Authorization: Bearer YOUR_API_KEY
```

**Response**:
```json
{
  "transactionId": "tx_abcdef1234567890",
  "status": "completed",
  "blockchain": "Ethereum",
  "details": {
    "timestamp": "2024-12-31T12:34:56Z",
    "amount": 10.5,
    "currency": "ETH"
  }
}
```

---

### **3.3 Cancel a Payment**
**Endpoint**: `/payments/{transactionId}/cancel`  
**Method**: `POST`

**Description**: Cancels a pending payment.

**Path Parameters**:
| Parameter        | Type   | Required | Description                           |
|------------------|--------|----------|---------------------------------------|
| `transactionId`  | String | Yes      | The unique ID of the transaction.    |

**Headers**:
```json
{
  "Authorization": "Bearer YOUR_API_KEY"
}
```

**Sample Request**:
```http
POST /payments/tx_abcdef1234567890/cancel
Authorization: Bearer YOUR_API_KEY
```

**Response**:
```json
{
  "status": "success",
  "message": "Payment successfully canceled"
}
```

---

## **4. Error Handling**

API responses may include error codes and messages. Below is a list of common errors:

| Error Code | HTTP Status | Description                            |
|------------|-------------|----------------------------------------|
| `ERR401`   | 401         | Unauthorized. Invalid or missing API key. |
| `ERR404`   | 404         | Resource not found.                   |
| `ERR400`   | 400         | Bad request. Check input parameters.  |
| `ERR500`   | 500         | Internal server error.                |

---

## **5. Rate Limits**

The Lattice API enforces rate limits to ensure fair usage:
- **100 requests per minute per API key.**
- Exceeding this limit results in a `429 Too Many Requests` response.

---

## **6. SDK Integration**

For ease of integration, consider using the Lattice SDK. Visit the [SDK Documentation](https://sdk.lattice.org) for details.

---

## **7. Support**

For assistance:
- Visit our [FAQ](https://lattice.org/faq).
- Join our [Discord community](https://discord.gg/lattice).
- Contact support at [support@lattice.org](mailto:support@lattice.org).

---

Would you like additional sections or further refinements to this documentation?
