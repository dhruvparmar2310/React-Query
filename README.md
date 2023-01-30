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

## Overview:
In overview, you will learn what is **Server State**, what are the issues after knowing Server State, pros and cons of React Query, etc.

### What is Server State ?
In order to know what is Server State, you must know the basics knownledge of Server States. In Server side state management, all the information or data is stored **in memory**. Server side state management is **more secure** than Client side state management. Where-else in client side state management, the data or information will be stored directly on **client-side**. This information can be from **cookies, query string,** etc.

Server states are totally different from client state. Initially, you must be aware of few things related to Server states:
- It requires asynchronous Api for fetching and updating Api calls.
- It can be changed by other peoples without our knowledge.
- It can become "out of date" in your application, if you don't take a proper care of it.

After knowning what is server states, there are some challenges which will occurs/arise as you move further:
- Caching: the most difficult challenging part in programming.
- Deduping(**process of removing same data from two or more datasets.**) multiple requests for the same data into a single request.
- updating "out of date" data in **background**.
- to know **when** the data is "out of date".
- to reflect updated data **as quick as** possible on the screen.
- performance optimization such as **pagination** and **lazy loading** data.
- to **memorize the query result** in structured sharing.
- to manage memory & garbage collection(**automatically free up memory space that has been allocated to objects no longer needed by the program**) of server state data.

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

> *You can see something like this example in react query*

```javascript
function Todos() {
  const { isLoading, isError, data, error } = useQuery({
    queryKey: ['todos'],
    queryFn: fetchTodoList,
  })

  if (isLoading) {
    return <span>Loading...</span>
  }

  if (isError) {
    return <span>Error: {error.message}</span>
  }

  // We can assume by this point that `isSuccess === true`
  return (
    <ul>
      {data.map((todo) => (
        <li key={todo.id}>{todo.title}</li>
      ))}
    </ul>
  )
}
```

In addition to `status` field, there is also one other object field importances (i.e.: `result`). Just like the `status` field, `fetchStatus` has the same situations.

- `fetchStatus === fetching`
- `fetchStatus === paused`
- `fetchStatus === idle`

## Why two status states required ?
- `status` state gives an information about `data`, it tells weather the data is available or not ?
- `fetchStatus` state gives an information about `queryFn`, it tells weather the `queryFn` is running or not.


### 2. Mutations:
Mutations are used to **create/update/delete data** or perform **server side modifications**. `useMutation()` hook is used for Mutations. It excepts one parameter, that is `mutationFn`:
```javascript
function App() {
  const mutation = useMutation({
    mutationFn: (newTodo) => {
      return axios.post('/todos', newTodo)
    },
  })

  return (
    <div>
      {mutation.isLoading ? (
        'Adding todo...'
      ) : (
        <>
          {mutation.isError ? (
            <div>An error occurred: {mutation.error.message}</div>
          ) : null}

          {mutation.isSuccess ? <div>Todo added!</div> : null}

          <button
            onClick={() => {
              mutation.mutate({ id: new Date(), title: 'Do Laundry' })
            }}
          >
            Create Todo
          </button>
        </>
      )}
    </div>
  )
}
```

Here, you can see `mutate` accepts the variable or object. The mutate function is an **asynchronous function**, which means you cannot use it directly in an event callback in React 16 and earlier. If you wanna access the event in **onSubmit** you need to wrap mutate in another function. This is due to React **event pooling**.

```javascript
const CreateTodo = () => {
  const mutation = useMutation({
    mutationFn: (formData) => {
      return fetch('/api', formData)
    },
  })
  const onSubmit = (event) => {
    event.preventDefault()
    mutation.mutate(new FormData(event.target))
  }

  return <form onSubmit={onSubmit}>...</form>
}
```
