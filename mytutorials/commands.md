# Commands

> Note: these commands I am showing here are 100% client side

## Making a command

Commands are also very useful, as they can be used to allow the user to trigger something in your mod. All commands must be a class, and extend `CommandBase`.

```java
class ExampleCommand extends CommandBase {

}
```

If you add this code, you will likely notice that your ide says you need to implement the CommandBase methods. Here is how you do that.

### getCommandName

This is pretty simple, tells forge what the name of your command is. (What they put after the `/` to run your command)

```java
@Override
public String getCommandName() {
    return "examplecommand";
}
```

### getCommandUsage

Tells forge what the "usage" of your command is, or how it is used.

```java
@Override
public String getCommandUsage(ICommandSender iCommandSender) {
    return "examplecommand <requiredArg1> [optionalArg2]";
}
```

### canCommandSenderUseCommand

Exactly what it sounds like, tells forge if the sender (person who ran the command) should be able to do it. Usually this should be hardcoded as `true`, unless you need to add extra logic to it.


```java
@Override
public boolean canCommandSenderUseCommand(ICommandSender sender)
{
    return true;
}
```

### processCommand

The main function of your command, is run whenever your command is called.

```java
@Override
public void processCommand(ICommandSender sender, String[] args) {
    // Run when the player does `/examplecommand`, replaced with your specified command name of course
}
```

This function takes two arguments:
1. `ICommandSender sender`, the player who ran the command
2. `String[] args`, the arguments ran with the command, for example: `/examplecommand foo bar` -> `args[0]`: `foo`, `args[1]`: `bar`

## Registering the command

You should also register the command in the `init` function of your main class, just like events.

```java
ClientCommandHandler.instance.registerCommand(new ExampleCommand());
```
