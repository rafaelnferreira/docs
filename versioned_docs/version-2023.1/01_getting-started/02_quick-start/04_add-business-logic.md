---
title: 'Quick start - add business logic'
sidebar_label: 'Add business logic'
id: add-business-logic
keywords: [getting started, quick start, dataserver, event handler, business logic]
tags:
    - getting started
    - quick start
    - dataserver
    - event handler
    - business logic
---

So far, you have a table; now we want to be able to see its content and create new entries.

## Data Server
A [Data Server](../../../server/data-server/introduction/) provides real-time data to the front end. You must define the Data Server in the file **alpha-dataserver.kts**.

```kotlin title='alpha-dataserver.kts'
dataServer {
    query("ALL_TRADES", TRADE)
}
```

## Event Handler
Next, we want to be able to insert rows into our table. For this, you need to define an [Event Handler](../../../server/event-handler/introduction/) in the file **alpha-eventhandler.kts**.

```kotlin title='alpha-eventhandler.kts'
eventHandler {

    eventHandler<Trade>(name = "TRADE_INSERT") {
        schemaValidation = false
        onCommit { event ->
            entityDb.insert(event.details)
            ack()
        }
    }

}
```
