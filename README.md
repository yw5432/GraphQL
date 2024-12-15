
# GraphQL Chat Service API

## Introduction

The **GraphQL Chat Service API** allows users to query chat history, user information, and friend lists, all through a single GraphQL endpoint.

## Getting Started

### Prerequisites
- Python 3.9+
- GraphQL client (e.g., Postman, Apollo Client, or GraphiQL)

### Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/your-repo-name.git
   cd your-repo-name
   ```

2. Install dependencies:
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   pip install -r requirements.txt
   ```
3.Integrate GraphQL routing into the FastAPI main.py file:
```Add heading
from graphql.schema import schema
```Add GraphQL routes
graphql_app = GraphQL(schema)
app.add_route("/graphql", graphql_app)
app.add_websocket_route("/graphql", graphql_app)


3. Start the service:
   ```bash
   uvicorn main:app --reload
   ```
   The GraphQL endpoint will be available at:
   ```
   http://127.0.0.1:8000/graphql
   ```

---

## Example Queries

Use a GraphQL client to send the following queries to the API:

### Fetch User by ID
```graphql
query {
  getUserById(userId: 1) {
    id
    email
    username
  }
}
```

### Fetch Chat History
```graphql
query {
  getChatHistory(senderId: 1, recipientId: 2) {
    senderId
    recipientId
    message
    timestamp
  }
}
```

### Fetch Friend List
```graphql
query {
  fetchFriendList(userId: 1) {
    friendId
    username
    email
  }
}
```

---

## Integration

### With Postman
1. Set the endpoint to `http://127.0.0.1:8000/graphql`.
2. Use the `POST` method.
3. Add your GraphQL query in the request body. Example:
   ```json
   {
     "query": "query { getUserById(userId: 1) { id username email } }"
   }
   ```

### With Apollo Client
Install Apollo Client:
```bash
npm install @apollo/client graphql
```

Example integration:
```javascript
import { ApolloClient, InMemoryCache, gql } from '@apollo/client';

const client = new ApolloClient({
  uri: 'http://127.0.0.1:8000/graphql',
  cache: new InMemoryCache(),
});

client.query({
  query: gql`
    query {
      getUserById(userId: 1) {
        id
        username
        email
      }
    }
  `
}).then(response => console.log(response.data));
```

---

## Troubleshooting

### Common Issues
1. **Server Not Reachable**: Ensure the service is running and accessible at the correct host and port.
2. **Invalid Query**: Verify query syntax matches the API schema.
3. **CORS Error**: Adjust `allow_origins` in `CORSMiddleware`.

---

This simplified version focuses on essentials while staying concise. Adjust it further if you want even less detail.
