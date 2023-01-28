# Learn React-Query with Dhruv Parmar
Hello Guys, I am **Dhruv Parmar**. Let's learn React Query together. If you like my content than plese give a **star** to this repository and also share with your friends.

## What is React Query ?
React query is a very efficient query caching client for the front-end which can replace traditional methods of fetching data on the mounting stage of the component and global state management like Redux in some use cases. React Query is also known as **missing data-fetching library** for React. React Query does the data **fetching, caching, synchroning** and **updating server state** in React.

I recommend you all to read the official [docs](https://tanstack.com/query/v4/docs/react/overview) of React Query.

React Query gives us **caching of server data** out of the box with cache invalidation and request deduping. 
> *Refer [this blog](https://alto.com/blog/post/react-query-for-managing-server-state) why all shift's to React Query ?*

## How do you handle errors in the React Query ?
There are mainly three ways to handle the errors in the React Query :
1) By using useQuery(): error property returned from useQuery().
2) onError callback
3) by using Error Boundaries

> *Refer [this blog](https://tkdodo.eu/blog/react-query-error-handling) for better understanding.*

## Can we replace Redux with React Query ?
No, we cannot replace React Query and context api with Redux, because they are on the same thing.

## Where is React Query data stored like Redux ?
React Query stores the cached data **in memory**. If you wanna store some additionally sync data somewhere else, than watch this [plugin](https://tanstack.com/query/latest/docs/react/plugins/persistQueryClient?from=reactQueryV3&original=https%3A%2F%2Freact-query-v3.tanstack.com%2Fplugins%2FpersistQueryClient).
