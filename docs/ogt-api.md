---
sidebar_position: 11
---

# OG Tracker API 

This documentation provides a complete guide to help you use the OGTracker API. It covers all endpoints, query parameters, and includes react-based examples to help integrate the API into your project seamlessly.

---

## Base URL
The API base URL is:
```
https://api.ogtracker.io/rest/v1/
```

---

## Authentication
Every request requires an API key. Include the following public anon-key to your header in all requests:
```plaintext
apikey: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InV6dHh2aGpieHRscGxzcGpmZW90Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3MzAxMzEwOTIsImV4cCI6MjA0NTcwNzA5Mn0.dBovj6wnDvWbuK-D0GCtsdJA8Fuik3JjGZrTPB1a6No
```

---

## Operators
```
https://docs.postgrest.org/en/v12/references/api/tables_views.html#operators
```

---

## Endpoints and Query Parameters

### 1. **Fetch all proposals**

**Endpoint:**  
```
GET /proposals
```

### Query Parameters

| Parameter      | Description                               | Example Values                                |
|----------------|-------------------------------------------|----------------------------------------------|
| `id`           | Proposal ID                              | `1`, `2`, `3` , `4`, `...`                    |
| `refnum`       | Referendum number                        | `334`, `634`, `168`                           |
| `status`       | Proposal status                          | `Delivered`, `InProgress`, `Flagged`          |
| `proposeradd`  | Proposer's address                       | `152WqfwdjHDwJBKfe85wXHtRsSxhcqGw4Qn3LmTa1ix1mSXY` |
| `benadd`       | Beneficiary's address                    | `152WqfwdjHDwJBKfe85wXHtRsSxhcqGw4Qn3LmTa1ix1mSXY` |
| `track`        | Track                                    | `smallSpender`, `mediumSpender`, `bigSpender`|
| `category`     | Category                                 | `Development`, `Outreach`, `Operations` , `Research`, `Economy`|
| `select`       | Fields to select                         | `*`                                          |


**Example Queries:**
- Fetch proposal by `refnum`:
  ```
  https://api.ogtracker.io/rest/v1/proposals?refnum=eq.118&select=*
  ```
- Fetch proposals with `status=Delivered`:
  ```
  https://api.ogtracker.io/rest/v1/proposals?status=eq.Delivered&select=*
  ```

**Example Response:**
```json
{
    "id": 49,
    "refnum": "77",
    "status": "Delivered",
    "proposer": "SmolDot Development",
    "proposeradd": "15kgSF6oSMFeaN7xYAykihoyQFZLRu1cF5FaBdiSDHJ233H5",
    "palink": "https://polkadot.polkassembly.io/referenda/77",
    "sublink": "https://polkadot.subsquare.io/referenda/77",
    "reqdot": "15,139",
    "benadd": "15kgSF6oSMFeaN7xYAykihoyQFZLRu1cF5FaBdiSDHJ233H5",
    "scanlink": "https://polkadot.subscan.io/account/15kgSF6oSMFeaN7xYAykihoyQFZLRu1cF5FaBdiSDHJ233H5",
    "ptitle": "Smoldot development financing Q3/2023",
    "track": "mediumSpender",
    "category": "Development",
    "fdate": "2023-08-21",
    "ldate": "2023-10-31",
    "proplink": "https://docs.google.com/document/d/1hXWsYPyvsF5KjU320hXseaoY4qxZ6TJLeZKt3WzcGEw/edit",
    "summary": "This proposal aims to enhance smoldot light client functionality and reliability within the Polkadot ecosystem...",
    "twitter": "-",
    "github": "https://github.com/smol-dot/smoldot/",
    "youtube": "-",
    "website": "-",
    "articles": "-"
}
```

---

### 2. **Fetch all tasks**

**Endpoint:**  
```
GET /tasks
```

**Query Parameters:**
- `proposal_id`: ID of the associated proposal (e.g., `1`, `2`, `3`)
- `select`: Fields to select (e.g., `*`)

**Example Queries:**
- Fetch tasks for proposal with `proposal_id=1`:
  ```
  https://api.ogtracker.io/rest/v1/tasks?proposal_id=eq.1&select=*
  ```

**Example Response:**
```json
[
    {
        "id": 1,
        "proposal_id": 1,
        "title": "Reward 22 high quality nomination pools with 250DOT each and reward Polkagate with 250 DOT as well for developing the tool",
        "status": "A",
        "code": null
    },
    {
        "id": 2,
        "proposal_id": 2,
        "title": "Cover the costs for 38 parachains with RPC API provision by allocating $620.",
        "status": "A",
        "code": null
    }
]
```

**Task Statuses:**

Each task can take one of the following values:

- `A`: **Delivered** – This means the task is delivered.
- `B`: **In Progress** – This means the task is still in progress.
- `C`: **Flagged** – This means it has not been delivered.
- `D`: **Remodel** – This means there were modifications to the task.

For more information regarding the statuses of tasks, please refer [**here**](/category/badging-system-on-tasks-).


---

### 3. **Fetch all Proof of Work (PoW)**

PoW entries are stored in the `proposals_report` table.  
Each PoW entry represents a report, document, or external link that proves work delivered for either:

- A **full proposal** (`task_id = null`)
- A **specific task** (`task_id = task_id`)

**Endpoint:**  
```
GET /proposals
```

**Query Parameters:**
- `proposal_id`: ID of the associated proposal (e.g., `933`, `934`, `944`)
- `task_id`: ID of the associated task (e.g., `12`, `45`)
- `select`: Fields to select (e.g., `*`)

---

**Example Queries:**

- Fetch PoW for a proposal with `proposal_id=100`:
  ```
  https://api.ogtracker.io/rest/v1/tasks?proposal_id=eq.100&select=*
  ```

---

**Example Response:**
```json
[
  {
    "id": 1472,
    "proposal_id": 100,
    "task_id": null,
    "content": "https://docs.google.com/document/d/1qlxxxxxxxxxxxxxxxxxxxx/edit",
    "created_at": "2025-10-24T17:48:16.020847+00:00"
  },
  {
    "id": 1464,
    "proposal_id": 100,
    "task_id": null,
    "content": "https://docs.google.com/document/d/1OExxxxxxxxxxxxxxxxxxxx/edit",
    "created_at": "2025-09-30T13:40:02.780693+00:00"
  }
]


## React Examples

### 1. Fetch All Proposals
```javascript
const fetchProposals = async () => {
  try {
    const response = await axios.get(`${API_BASE_URL}proposals`, {
      headers: { apikey: API_KEY },
      params: { select: "*" },
    });
    console.log(response.data); // Log all proposals
  } catch (error) {
    console.error("Error fetching proposals:", error);
  }
};
```

### 2. Fetch Proposals with Filters
```javascript
const fetchDeliveredProposals = async () => {
  try {
    const response = await axios.get(`${API_BASE_URL}proposals`, {
      headers: { apikey: API_KEY },
      params: { status: "eq.Delivered", select: "*" },
    });
    console.log(response.data); // Log delivered proposals
  } catch (error) {
    console.error("Error fetching delivered proposals:", error);
  }
};

```

### 3. Fetch Tasks for a Specific Proposal
```javascript
const fetchTasksByProposalId = async (proposalId) => {
  try {
    const response = await axios.get(`${API_BASE_URL}tasks`, {
      headers: { apikey: API_KEY },
      params: { proposal_id: `eq.${proposalId}`, select: "*" },
    });
    console.log(response.data); // Log tasks for the proposal
  } catch (error) {
    console.error("Error fetching tasks:", error);
  }
};

```
### 4. Fetch Tasks with Filters
```javascript
const fetchFilteredTasks = async (status) => {
  try {
    const response = await axios.get(`${API_BASE_URL}tasks`, {
      headers: { apikey: API_KEY },
      params: { status: `eq.${status}`, select: "*" },
    });
    console.log(response.data); // Log tasks with specific status
  } catch (error) {
    console.error("Error fetching filtered tasks:", error);
  }
};


```

### 5. Fetch Proposals with Pagination
```javascript
const fetchPaginatedProposals = async (limit, offset) => {
  try {
    const response = await axios.get(`${API_BASE_URL}proposals`, {
      headers: { apikey: API_KEY },
      params: { select: "*", limit, offset },
    });
    console.log(response.data); // Log paginated proposals
  } catch (error) {
    console.error("Error fetching paginated proposals:", error);
  }
};

```
### 6. Fetch PoW for a Specific Proposal
```javascript
const fetchPowByProposalId = async (proposalId) => {
  try {
    const response = await axios.get(`${API_BASE_URL}proposals_report`, {
      headers: { apikey: API_KEY },
      params: { proposal_id: `eq.${proposalId}`, select: "*" },
    });
    console.log(response.data); // Log PoW for the proposal
  } catch (error) {
    console.error("Error fetching PoW:", error);
  }
};

```

### 7. Fetch PoW for a Specific Task
```javascript
const fetchPowByTaskId = async (taskId) => {
  try {
    const response = await axios.get(`${API_BASE_URL}proposals_report`, {
      headers: { apikey: API_KEY },
      params: { task_id: `eq.${taskId}`, select: "*" },
    });
    console.log(response.data); // Log PoW for the task
  } catch (error) {
    console.error("Error fetching task PoW:", error);
  }
};


```

### 8. Fetch PoW with Pagination
```javascript
const fetchPaginatedPow = async (limit, offset) => {
  try {
    const response = await axios.get(`${API_BASE_URL}proposals_report`, {
      headers: { apikey: API_KEY },
      params: { select: "*", limit, offset },
    });
    console.log(response.data); // Log paginated PoW
  } catch (error) {
    console.error("Error fetching paginated PoW:", error);
  }
};

```

## Full Example
Below is an example of how to fetch proposals and tasks using React with Axios:

```javascript
import React, { useState, useEffect } from "react";
import axios from "axios";

const API_BASE_URL = "https://api.ogtracker.io/rest/v1/";
const API_KEY = "YOUR_API_KEY";

const fetchData = async (endpoint, params = {}) => {
  try {
    const response = await axios.get(`${API_BASE_URL}${endpoint}`, {
      headers: { apikey: API_KEY },
      params,
    });
    return response.data;
  } catch (error) {
    console.error("Error fetching data:", error);
    return [];
  }
};

const App = () => {
  const [proposals, setProposals] = useState([]);
  const [tasks, setTasks] = useState([]);

  useEffect(() => {
    fetchData("proposals", { status: "eq.Delivered", select: "*" }).then((data) =>
      setProposals(data)
    );

    fetchData("tasks", { select: "*" }).then((data) => setTasks(data));
  }, []);

  return (
    <div>
      <h1>OGTracker Data</h1>
      <h2>Proposals</h2>
      <ul>
        {proposals.map((proposal) => (
          <li key={proposal.id}>{proposal.ptitle}</li>
        ))}
      </ul>
      <h2>Tasks</h2>
      <ul>
        {tasks.map((task) => (
          <li key={task.id}>{task.title}</li>
        ))}
      </ul>
    </div>
  );
};

export default App;
```

---

## Notes
- The `select` parameter allows specifying which fields to return in the response.
- Use the `limit` and `offset` parameters for pagination:
  - `?limit=10&offset=10`
