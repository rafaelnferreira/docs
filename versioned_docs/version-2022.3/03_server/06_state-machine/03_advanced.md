---
title: 'State Machine - advanced'
sidebar_label: 'Advanced'
id: advanced
keywords: [server, state machine, advanced]
tags:
  - server
  - state machine
  - advanced
---

The state machine can be injected to the Event Handler script or API.

## StateMachineBuilder

You can build state machine using this interface by providing following:
- Entity of the state machine. In below example it is called Trade.
- State of entity field to manage, this field needs to be ENUM field. In the below example it is called TradeStatus
- The side effect of a state change, is something you can subscribe to when the state changes. In below example it is called TradeEffect.

```kotlin
sealed class TradeEffect {
    object New : TradeEffect()
    object Allocated : TradeEffect()
    object Cancelled : TradeEffect()
}
```

It has got following functions:

### readState
`fun readState(init: T.() -> S)`
Specifies which state to read from table.

### state
`fun state(state: S, stateHandler: StateBuilder<T, S, E>.() -> Unit)`
This is the method where you define how to handle the state of the table. Handling of the state is managed by StateBuilder, which is explained in detail below.

#### StateBuilder

|| Signature    | Description |
|--------------|-------------|---|
| isMutable    | `var isMutable: Boolean` | When set to false, any modification to the  entity while in this state will be rejected|
| initialState | `fun initialState(sideEffect: E, transitionBuilder: TransitionBuilderInit<T>? = null)` | The state machine will accept the specified state on creation |
| initialState | `fun initialState(sideEffect: E,priority: Int,transitionBuilder: TransitionBuilderInit<T>? = null)` | The state machine will accept the specified state on creation and you can specify priority for this transition |
| initialStateWithContext | `fun <C : Any> initialStateWithContext(sideEffect: E,transitionBuilder: ContextTransitionBuilder<T, C>.() -> Unit,)` | The state machine will accept the current state on creation. The validation will share a context. |
| initialStateWithContext | `fun <C : Any> initialStateWithContext(sideEffect: E,priority: Int,transitionBuilder: ContextTransitionBuilder<T, C>.() -> Unit,)` | The state machine will accept the current state on creation and you can specify priority for this transition. The validation will share a context. |
| transition | `fun transition(newState: S,sideEffect: E,transitionBuilder: TransitionBuilderInit<T>? = null,)` | The state machine will a transition from the current state to [newState] |
| transition | `fun transition(newState: S,sideEffect: E,priority: Int,transitionBuilder: TransitionBuilderInit<T>? = null,)` | The state machine will a transition from the current state to [newState]  and you can specify priority for this transition|
| transitionWithContext | `fun <C : Any> transitionWithContext(newState: S,sideEffect: E,transitionBuilder: ContextTransitionBuilder<T, C>.() -> Unit,) ` | The state machine will a transition from the current state to [newState] |
| transitionWithContext | `fun <C : Any> transitionWithContext(newState: S,sideEffect: E,priority: Int,transitionBuilder: ContextTransitionBuilder<T, C>.() -> Unit,)` | The state machine will a transition from the current state to [newState] and you can specify priority for this transition. The validation will share a context|


State machine creation is explained with the example below.

```kotlin
@Module
class TradeStateMachine @Inject constructor(
    db: AsyncEntityDb
) {
    private val internalState: StateMachine<Trade, TradeStatus, TradeEffect> = db.stateMachineBuilder {
        // Read TRADE_STATUS from Trade table
        readState { tradeStatus }

        // Defines how the status NEW is handled
        state(TradeStatus.NEW) {
            // Allows the status to change
            isMutable = true

            // State machine will accept the specified state on creation of trade
            initialState(TradeEffect.New) {
                onValidate { trade ->
                    if (trade.isTradeIdInitialised && trade.tradeId.isNotEmpty()) {
                        verify {
                            db hasNoEntry Trade.ById(trade.tradeId)
                        }
                    }
                }
            }

            onCommit { trade ->
                if (trade.enteredBy == "TestUser") {
                    trade.price = 10.0
                }
            }

            // Allowed transitions are from NEW to ALLOCATED
            transition(TradeStatus.ALLOCATED, TradeEffect.Allocated)
            // Allowed transitions are from NEW to CANCELLED
            transition(TradeStatus.CANCELLED, TradeEffect.Cancelled)
        }

        // Defines how the status ALLOCATED is handled
        state(TradeStatus.ALLOCATED) {
            // Doesn't allow the status to change
            isMutable = false

            transition(TradeStatus.NEW, TradeEffect.New)
            transition(TradeStatus.CANCELLED, TradeEffect.Cancelled)
        }

        // Defines how the status CANCELLED is handled
        state(TradeStatus.CANCELLED) {
            // Doesn't allow the status to change
            isMutable = false
        }
    }
}
```

## StateMachine

State machine properties and functions:

|                           | Signature                                                                                                                                                                                     | Description                                                                                                                                                                                                                                                                          |
|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| sideEffects               | `val sideEffects: Set<E>`                                                                                                                                                                     | Provides all possible side effects                                                                                                                                                                                                                                                   |
| subscribe                 | `fun subscribe(): Flow<Transition<T, S, E>>`                                                                                                                                                  | Subscribers will be notified of state transitions                                                                                                                                                                                                                                    |
| highestPriorityTransition | `suspend fun highestPriorityTransition(value: T,): ValidationResult<S>?`                                                                                                                      | Given the table name, it gives the highest priority transition of the table if present or null                                                                                                                                                                                       |
| currentState              | `suspend fun currentState(value: T): S?`                                                                                                                                                      | Reads the current state [S] of [value] [T] from the database                                                                                                                                                                                                                         |
| create                    | `suspend fun create(value: T): Transition<T, S, E>`                                                                                                                                           | Creates a new entity in the database.                                                                                                                                                                                                                                                |
| update                    | `suspend fun update(value: T): Transition<T, S, E>?`                                                                                                                                          | Will validate and write [value] to the database. Returns a [Transition] if the update caused a transition, else null and throws IllegalArgumentException if the value is not valid                                                                                                   |
| update                    | `suspend fun update(uniqueEntityIndex: UniqueEntityIndex<T, *>,updateEntity: suspend (entity: T, transaction: AsyncMultiEntityReadWriteGenericSupport) -> Unit,): Transition<T, S, E>?`       | Accepts a [UniqueEntityIndex] and a update lambda and validates and writes [value] to the database. Returns a [Transition] if the update caused a transition, else null and throws IllegalArgumentException if the value is not valid, or if the item doesn't exist in the database. |
| updateIfExists            | `suspend fun updateIfExists(uniqueEntityIndex: UniqueEntityIndex<T, *>,updateEntity: suspend (entity: T, transaction: AsyncMultiEntityReadWriteGenericSupport) -> Unit,): Transition<T, S, E>?` | Accepts a [UniqueEntityIndex] and a update lambda and validates and writes [value] to the database. Returns a [Transition] if the update caused a transition, else null and throws IllegalArgumentException if the value is not valid                                                |
| validate                  | `suspend fun validate(value: T,newState: S,): ValidationResult<S>`                                                                                                                            | Validates if [value] can successfully transition to [newState]                                                                                                                                                                                                                       |
| withTransaction | `suspend fun <O : Any?> withTransaction(transaction: AsyncMultiEntityReadWriteGenericSupport,handling: suspend StateMachine<T, S, E>.() -> O,): O` | Will take a transaction and will handle all state machine calls within [handling] within the provided transaction  |
| withTransaction | `suspend fun <O : Any?> withTransaction(handling: suspend StateMachine<T, S, E>.() -> O,): O` | Will create a transaction and will handle all state machine calls within [handling] within the provided transaction |

Example for above state machine usage:

```kotlin
suspend fun insert(trade: Trade): Transition<Trade, TradeStatus, TradeEffect> = internalState.create(trade)

suspend fun modify(tradeId: String, modify: suspend (Trade) -> Unit): Transition<Trade, TradeStatus, TradeEffect>? =
        internalState.update(Trade.ById(tradeId)) { trade, _ -> modify(trade) }

suspend fun modify(trade: Trade): Transition<Trade, TradeStatus, TradeEffect>? = internalState.update(trade)
```

## Inject state machine

### Inject state machine in [Event Handler](../../../server/event-handler/basics) file

```kotlin
eventHandler {
    val stateMachine = inject<TradeStateMachine>()

    eventHandler<Trade>(name = "TRADE_INSERT", transactional = true) {
        permissioning {
            permissionCodes = listOf("TRADER")
            auth(mapName = "ENTITY_VISIBILITY") {
                field { counterpartyId }
            }
        }
        onValidate { event ->
            val message = event.details
            verify {
                entityDb hasEntry Counterparty.ById(message.counterpartyId)
                entityDb hasEntry Instrument.ById(message.instrumentId)
            }
            ack()
        }
        onCommit { event ->
            val trade = event.details
            trade.enteredBy = event.userName
            stateMachine.insert(entityDb, trade)
            ack()
        }
    }
}
```

You can also see a state machine being created in practice in our [tutorial](../../../getting-started/developer-training/training-content-day4/#state-management).

### Inject state machine in event handler [API](../../../database/api-reference/event-handler-api/)

```kotlin
@Module
class EventCompanyHandlerAsync @Inject constructor(
  private val entityDb: AsyncEntityDb,
  private val tradeMachine: TradeStateMachine
) : AsyncEventHandler<Company, EventReply> {
  override suspend fun process(message: Event<Company>): EventReply {
    val company = message.details
    // custom code block..
    return EventReply.EventAck()
  }
}
```
