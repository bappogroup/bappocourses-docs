---
description: This article shows you how to interact with the backend in Bappo coding.
---

# DB Query API in Bappo Coding

There are two ways to send requests to the backend: RPC based and GraphQL based.

## RPC $models

{% embed url="https://bappogroup.github.io/bappo-developer-docs/docs/custom-view-models.html" %}

**Performance boost approaches:**

1. Avoid nested `include`. Three levels have proven to slows down the server significantly.
2. Use `Promise.all` to fetch records in parallel.
3. You don't need to fetch all the data before showing the page to a user - incremental loading \(loading unnecessary stuff silently in the background, and when the results come back, update the display\).

Load data when a component mounts:

```text
import React from "react";

/**
 * Example to show how to load data when a component mounts
 */
export default function Rpc({ $models }) {
  const [records, setRecords] = React.useState([]);

  React.useEffect(() => {
    getRecords();
  }, []);

  async function getRecords() {
    const { data } = await $models.Company.findAll({
      where: {
        name: "Apple"
      },
      include: [
        {
          as: "customers",
          where: {
            name: "John"
          }
        }
      ]
    });
    // store the data to the state
    setRecords(data);
  }

  return <button onClick={getRecords}>Hello World</button>;
}

```

## GraphQL

The below example shows how to use GraphQL to perform `findOne` , findAll and createOne in Bappo coding. 

We follow the same pattern used by the famous [Apollo Client](https://www.apollographql.com/docs/react/get-started/). 

```text
import React from "react";
import { gql, useQuery, useMutation } from "@bappo/sdk";

const FIND_CUSTOMERS = gql`
  query {
    Customer_all {
      id
      name
    }
  }
`;

const FIND_CUSTOMER = gql`
  query($id: ID!) {
    Customer(id: $id) {
      id
      name
      company {
        name
      }
    }
  }
`;

export default function Hello() {
  const { loading, error, data } = useQuery(FIND_CUSTOMER, {
    variables: {
      id: "1"
    }
  });

  console.log(loading, error, data);

  return <div>Hello World</div>;
}

// const CREATE_CUSTOMER = gql`
//   mutation createInvoice($name: String!) {
//     createCustomer(input: { name: $name }) {
//       id
//       name
//     }
//   }
// `;

// export default function Hello() {
//   const [createCustomer, result] = useMutation(CREATE_CUSTOMER);

//   console.log(result);

//   return (
//     <button
//       onClick={() => {
//         createCustomer({
//           variables: {
//             name: "Test Customer"
//           }
//         });
//       }}
//     >
//       Create Customer
//     </button>
//   );
// }

```

For the detailed syntax of all supported queries and mutations, see [https://docs.google.com/spreadsheets/d/1urtCUHlaC\_GDN7bEXztw7K6GS5ThB77Q-CBxUdQ-9Aw/edit\#gid=0](https://docs.google.com/spreadsheets/d/1urtCUHlaC_GDN7bEXztw7K6GS5ThB77Q-CBxUdQ-9Aw/edit#gid=0)

