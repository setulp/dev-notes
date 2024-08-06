---
title: TypeScript and Angular
---


## Typescript

Came from "LiveScript".
Runs on browser, isolated from RAM or CPU, can do client based things like validation in order to prevent a request to the server every time something like validation is needed.

Coupling - "Strength of relationships between code modules"
Cohesion - "How well does it all go together - is it 'close at hand'".

Service:
    - code that owns sone specific
      state and state process


Angular and Apps go through firewall/proxy to connect to services on server side.

Dr. Alan Kay - (Smalltalk creator): OOP is "local retention of state and hiding of state and state process"


Make all your data global.
    - global, but immutable. nobody can change that data.
    - have a single source of truth for this stuff, a single place that NEVER
        changes the data, but you can ask it to consider creating a new version of the data.



## Angular



State Management: State management is the process of managing the states of user controls. It helps developers build large-scale applications with heavy data communications while sustaining high application performance.

- Large team - You can split development tasks between people easily if you have chosen CQRS architecture. Your top people can work on domain logic leaving usual stuff to less skilled developers.
- Difficult business logic - CQRS forces you to avoid mixing domain logic and infrastructural operations.
- Scalability matters - With CQRS you can achieve great read and write performance, command handling can be scaled out on multiple nodes and as queries are read-only operations they can be optimized to do fast read operations.

Services, Signals: Organize and share business logic, models, or data and functions with different components. This allows us to create an object that can handle a bunch of things related to the "service".

Entities: Objects that are in lists of things that are compared using an ID.

```typescript

export class SignalService<T> {
  state = signal({} as T);

  constructor() {}

}

// or

element.addEventListener('click', () => setCounter(counter + 1))
```



A service we used:

```typescript

import { patchState, signalStore, withComputed, withMethods } from '@ngrx/signals';
import { addEntity, updateEntity, withEntities } from '@ngrx/signals/entities';
import { TodoListItem, TodoListSummary } from '../todo-list/models';
import { computed } from '@angular/core';

export const TodosStore = signalStore(
  { providedIn: 'root' },
  withEntities<TodoListItem>(),
  withComputed(({entities}) => {
    
    return {
        
        getSummary: computed(() => {
            return {
                totalItems: entities().length,
                incompleteItems: entities().filter(t => t.completed === false).length,
                completeItems: entities().filter(t => t.completed === true).length
            }  as TodoListSummary
        })
    }
  }),
  withMethods((state) => {
    return {
      markTodoComplete(item: TodoListItem) {
        patchState(state, updateEntity({id: item.id, changes: {
         
          completed: true}}))
      },

      addTodoItem(description: string) {
        const newItem: TodoListItem = {
          id: crypto.randomUUID(),
          description,
          completed: false,
        };
        patchState(state, addEntity(newItem));
      },
    };
  })
);


```
