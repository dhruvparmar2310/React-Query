# Learn React-Query with Dhruv Parmar
Hello Guys, I am **Dhruv Parmar**. Let's learn React Query together. If you like my content than plese give a **star** to this repository and also share with your friends.

## What is React Query ?
React query is a very efficient query caching client for the front-end which can replace traditional methods of fetching data on the mounting stage of the component and global state management like Redux in some use cases. React Query is also known as **missing data-fetching library** for React. React Query does the data **fetching, caching, synchroning** and **updating server state** in React. React Query is the best library to manage **server state** data.

I recommend you all to read the official [docs](https://tanstack.com/query/v4/docs/react/overview) of React Query.

React Query gives us **caching of server data** out of the box with cache invalidation and request deduping. 
> *Refer [this blog](https://alto.com/blog/post/react-query-for-managing-server-state) why all shift's to React Query ?*

## How do you handle errors in the React Query ?
There are mainly three ways to handle the errors in the React Query :
- By using useQuery(): error property returned from useQuery().
- onError callback
- by using Error Boundaries

> *Refer [this blog](https://tkdodo.eu/blog/react-query-error-handling) for better understanding.*

## Can we replace Redux with React Query ?
No, we cannot replace React Query and context api with Redux, because they are not the same thing.

## Where is React Query data stored like Redux ?
React Query stores the cached data **in memory**. If you wanna store some additionally sync data somewhere else, than watch this [plugin](https://tanstack.com/query/latest/docs/react/plugins/persistQueryClient?from=reactQueryV3&original=https%3A%2F%2Freact-query-v3.tanstack.com%2Fplugins%2FpersistQueryClient).

## Get Started:
There are mainly three core concepts in React Query:
- [Queries](https://tanstack.com/query/v4/docs/react/guides/queries)
- Muatations
- Query Invalidation

### 1. Queries:
A query can be used with any Promise based method (**including GET and POST methods**) to fetch data from a server. If your method **modifies data** on the server, we recommend using **Mutations** instead.

To subscribe queries in your components, `useQuery()` is used. It has two parameter's:
- a unique key and
- a function retuning promises.

> *For example*

```javascript
import { useQuery } from '@tanstack/react-query'

function App() {
  const info = useQuery({ queryKey: ['todos'], queryFn: fetchTodoList })
}
```

The **unique key** is used for refetching, caching, and sharing your queries with your application. A query can only be in one of the following states at any given moment:
- `isLoading` or `status === loading`
- `isError` or `status === error`
- `isSuccess` or `status === success`

The query mostly depends on two states:
- `data`: If the query is in `success` state, than the data is available through `data` property.
- `error`: If the query is in `isError` state, than the errors are available through `error` property.
