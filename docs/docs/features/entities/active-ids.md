# Active ID(s)

This feature requires the `withEntities` to be used in the `Store`. It lets you hold one or more IDs indicating the entities that are currently active. It is often useful
for monitoring which entities the user is interacting with.

## Active Id

To use this feature, provides the `withActiveId` props factory function to `createState`:

```ts
import { createState, Store } from '@ngneat/elf';
import { withEntities, withActiveId } from '@ngneat/elf-entities';

interface Todo {
  id: number;
  label: string;
}

const { state, config } = createState(withEntities<Todo>(), withActiveId());

const todosStore = new Store({ name: 'todos', state, config });
```

This will allow you to use the following ready-made mutations and queries:

### Queries

#### `selectActiveEntity`

Select the active entity:

```ts
import { selectActiveEntity } from '@ngneat/elf-entities';

const active$ = todosStore.pipe(selectActiveEntity());
```

#### `selectActiveId`

Select the active id:

```ts
import { selectActiveId } from '@ngneat/elf-entities';

const activeId$ = todosStore.pipe(selectActiveId());
```

#### `getActiveId`

Get the active id:

```ts
import { getActiveId } from '@ngneat/elf-entities';

const active = todosStore.query(getActiveId);
```

### Mutations

#### `setActiveId`

Set the active id:

```ts
import { setActiveId } from '@ngneat/elf-entities';

todosStore.reduce(setActiveId(id));
```

## Active Ids

To use this feature, provides the `withActiveIds` props factory function to `createState`:

```ts
import { createState, Store } from '@ngneat/elf';
import { withEntities, withActiveIds } from '@ngneat/elf-entities';

interface Todo {
  id: number;
  label: string;
}

const { state, config } = createState(withEntities<Todo>(), withActiveIds());

const todosStore = new Store({ name: 'todos', state, config });
```

This will allow you to use the following ready-made mutations and queries:

### Queries

#### `selectActiveEntities`

Select the active entities:

```ts
import { selectActiveEntities } from '@ngneat/elf-entities';

const actives$ = todosStore.pipe(selectActiveEntities());
```

#### `selectActiveIds`

Select the active ids:

```ts
import { selectActiveIds } from '@ngneat/elf-entities';

const activeIds$ = todosStore.pipe(selectActiveIds());
```

#### `getActiveIds`

Get active ids:

```ts
import { getActiveIds } from '@ngneat/elf-entities';

const actives = todosStore.query(getActiveIds);
```

### Mutations

#### `setActiveIds`

Set the active ids:

```ts
import { setActiveIds } from '@ngneat/elf-entities';

todosStore.reduce(setActiveIds([id, id]));
```

#### `addActiveIds`

Add active ids:

```ts
import { addActiveIds } from '@ngneat/elf-entities';

todosStore.reduce(addActiveIds([id, id]));
```

#### `toggleActiveIds`

Toggle active ids:

```ts
import { toggleActiveIds } from '@ngneat/elf-entities';

todosStore.reduce(toggleActiveIds([id, id]));
```

#### `removeActiveIds`

Remove active ids:

```ts
import { removeActiveIds } from '@ngneat/elf-entities';

todosStore.reduce(removeActiveIds([id, id]));
```