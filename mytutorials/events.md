# Events

Events are very useful in forge, because they allow you to both
1. Run code when something happens
2. Cancel something happening

To register events in forge, you need to use the event bus.

## Making an event

To start out, make a new class, and call it whatever. For this example, I will use `Events`.
> Note: in this tutorial I will not be including imports. Imports are usually easy to find using your ide, and pretty self expalnitory.

```java
public class Events {

}
```

The next step is to actually find the event we want, and to make a function for it. In this case, the `TickEvent`. All event functions need to have the `@SubscribeEvent` decorator. This tells forge they are an event and they should be treated as one.

```java
public class Events {
    @SubscribeEvent
    public void onTick(ClientTickEvent event) {
        // This code will run every tick that happens on the client, hence the "ClientTickEvent"
    }
}
```

How you specify the event is in the arguments of your function. You should have an argument named `event` and typed to whatever event you want to use. Pretty simple.

## Registering the event

All events should be registered in the `init` function of your main class. Here is how you register them (using my event class names):

```java
MinecraftForge.EVENT_BUS.register(new Events());
```

Since you register them as a class, you can have as many event functions in the class as you want, and all of them will work fine. You can also organize them however you want, as long as
1. The actual functions are decorated with `@SubscribeEvent`
2. An instance of the class is passed to `MinecraftForge.EVENT_BUS.register`

## Cancelling events

Canceling events can allow you to do many things, like stopping a player from rendering, which is what I will show in this example.
> Note: In here I use the `RenderPlayerEvent.Pre` event. Events have have different states, `Event.Pre` (happens before the event), `Event` (happens during the event), `Event.Post` (happens after the event). When cancelling, it is usually best to use `Pre`

```java
public class Events {
    @SubscribeEvent
    public void onRenderPlayerEventPre(RenderPlayerEvent.Pre event) {
        if (event.isCancelable()) {
            event.setCanceled(true);
        }
    }
}
```

In this code you see two things.
1. `event.isCancelable()`
2. `event.setCanceled(true);`

The first one is self explanitory, checks if the event CAN be canceled.
The second one is the actual code that cancels the event.
