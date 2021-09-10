# Status

Using this feature, you can manage the status of API calls in your store. First, you need to install the package by using the CLI command or npm:

```bash
npm i @ngneat/elf-requests
```

To use this feature, provides the `withRequestsStatus` props factory function to `createState`:

```ts
import { createState, Store } from '@ngneat/elf';
import { withEntities } from '@ngneat/elf-entities';
import { withRequestsStatus } from '@ngneat/elf-requests';

interface Todo {
  id: number;
  label: string;
}

const { state, config } = createState(
  withEntities<Todo>(),
  withRequestsStatus()
);

const todosStore = new Store({ name: 'todos', state, config });
```

In your server call, you can use the `setRequestStatus` operator and pass a unique key to identify the request:

```ts
import { setRequestStatus } from '@ngneat/elf-requests';

http.get(todosUrl).pipe(
  tap((todos) => todosRepo.setEntities(todos)),
  setRequestStatus(todosRepo.store, 'todos')
);
```

This will ensure the `store` will have the `todos` call listed as `pending` in the store, until the call complete,
at which point it changes to either `success` or `error`.

You can monitor and change the request status for your APIs using the following queries and mutations:

### Queries

#### `selectRequestStatus`

Select the status of the provided request key:

```ts
import { selectRequestStatus } from '@ngneat/elf-requests';

todosStatus$ = store.pipe(selectRequestStatus('todos'));

// This will return success when either the `todos` key or the `todo-1` key is succeeded
todoStatus$ = store.pipe(selectRequestStatus('todo-1', { groupKey: 'todos' }));
```

#### `getRequestStatus`

Get the status of the provided request key:

```ts
import { getRequestStatus } from '@ngneat/elf-requests';

todosStatus = store.query(getRequestStatus('todos'));
```

#### `selectIsRequestPending`

Select whether the status of the provided request key is `pending`:

```ts
import { selectIsRequestPending } from '@ngneat/elf-requests';

pending$ = store.pipe(selectIsRequestPending('todos'));
```

### Mutations

#### `updateRequestStatus`

```ts
import { updateRequestCache } from '@ngneat/elf-requests';

store.reduce(updateRequestStatus('todos', { value: 'pending' }));
store.reduce(updateRequestStatus('todos', { value: 'success' }));
store.reduce(updateRequestStatus('todos', { value: 'error', error }));
```

And more:
`updateRequestsStatus`, `selectRequestsStatus`, `resetRequestsStatus`, `getRequestsStatus`, `setRequestsStatus`