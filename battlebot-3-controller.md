### @title Battle Bot 3: Safety Stop (Controller)

### @description Make your Arcade controller send commands continuously so your robot's safety stop works.

### @preferredEditor blocks

### @explicitHints true

# Battle Bot 3: Safety Stop (Controller)

```package
radio
```

```template
let channel = ""
channel = "duck"
radio.setGroup(101)
scene.setBackgroundColor(15)
let bot = sprites.create(img`
    . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . .
    . . . 2 2 2 2 2 2 2 2 2 2 . . .
    . . . 2 2 2 2 2 2 2 2 2 2 . . .
    . . . 2 2 f 2 2 2 2 f 2 2 . . .
    . . . 2 2 2 2 2 2 2 2 2 2 . . .
    . f f 2 2 2 2 2 2 2 2 2 2 f f .
    . f f 2 2 2 2 2 2 2 2 2 2 f f .
    . f f 2 2 2 2 2 2 2 2 2 2 f f .
    . f f 2 2 2 2 2 2 2 2 2 2 f f .
    . . . 2 2 2 2 2 2 2 2 2 2 . . .
    . . . 2 2 2 2 2 2 2 2 2 2 . . .
    . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . .
    `, SpriteKind.Player)
controller.up.onEvent(ControllerButtonEvent.Pressed, function () {
    radio.sendValue(channel, 3)
    bot.sayText("forward")
})
controller.up.onEvent(ControllerButtonEvent.Released, function () {
    radio.sendValue(channel, 2)
    bot.sayText("stop")
})
controller.down.onEvent(ControllerButtonEvent.Pressed, function () {
    radio.sendValue(channel, 4)
    bot.sayText("reverse")
})
controller.down.onEvent(ControllerButtonEvent.Released, function () {
    radio.sendValue(channel, 2)
    bot.sayText("stop")
})
controller.left.onEvent(ControllerButtonEvent.Pressed, function () {
    radio.sendValue(channel, 0)
    bot.sayText("spin left")
})
controller.left.onEvent(ControllerButtonEvent.Released, function () {
    radio.sendValue(channel, 2)
    bot.sayText("stop")
})
controller.right.onEvent(ControllerButtonEvent.Pressed, function () {
    radio.sendValue(channel, 1)
    bot.sayText("spin right")
})
controller.right.onEvent(ControllerButtonEvent.Released, function () {
    radio.sendValue(channel, 2)
    bot.sayText("stop")
})
```

## Introduction @showdialog
Your robot now has a **safety stop**: if it doesn't hear from you for half a second, it stops.

But your controller only sends a message when a button is **pressed** or **released**. While you hold a button, it sends nothing — so the robot stops.

The fix: a controller that **keeps talking** — sending the current move 10 times every second, whether anything changed or not.

Your template is your code from Battle Bot 2. Check the **group** and **name** still match your robot.

## Step 1: Remove the Button Events
Delete all eight ``||controller:on button pressed||`` and ``||controller:on button released||`` blocks.

You'll replace them with **one** block that checks every button, every tenth of a second.

## Step 2: A Command Variable
From ``||variables:Variables||``, make a variable called **command**.

```blocks
let command = 0
let channel = ""
channel = "duck"
radio.setGroup(101)
scene.setBackgroundColor(15)
```

## Step 3: Check the Buttons 10 Times a Second
From ``||game:Game||``, drag ``||game:on game update every 100 ms||``.

Inside it:
- ``||variables:set command to 2||`` — start by assuming **stop**
- ``||logic:if||`` ``||controller:is up button pressed||`` → ``||variables:set command to 3||``
- ``||radio:radio send value||`` ``||variables:channel||`` = ``||variables:command||``
- ``||sprites:bot say||`` ``||variables:command||``

Notice the question changed. Before it was *"did a button just change?"* Now it's *"which button is being held right now?"*

```blocks
game.onUpdateInterval(100, function () {
    command = 2
    if (controller.up.isPressed()) {
        command = 3
    }
    radio.sendValue(channel, command)
    bot.sayText(command)
})
```

## Step 4: The Other Directions
Click **+** on your ``||logic:if||`` to add ``||logic:else if||`` branches:

- ``||controller:is down button pressed||`` → **4**
- ``||controller:is left button pressed||`` → **0**
- ``||controller:is right button pressed||`` → **1**

If nothing is held, ``||variables:command||`` stays at **2**, so letting go still means stop.

```blocks
game.onUpdateInterval(100, function () {
    command = 2
    if (controller.up.isPressed()) {
        command = 3
    } else if (controller.down.isPressed()) {
        command = 4
    } else if (controller.left.isPressed()) {
        command = 0
    } else if (controller.right.isPressed()) {
        command = 1
    }
    radio.sendValue(channel, command)
    bot.sayText(command)
})
```

## Step 5: Test in the Simulator
Use the arrow keys. The number above your bot should be:
- **2** with nothing pressed
- **3** up, **4** down, **0** left, **1** right

## Step 6: Download and Test the Safety Stop
Download to your Arcade controller. Your robot should be running **Battle Bot 3: Safety Stop (Robot)**.

Test:
1. Hold up — the robot drives and **keeps driving** while you hold
2. Let go — it stops
3. Hold up, then switch the controller **off** — the robot should stop within half a second

That last one is the safety stop working.

## Complete! @showdialog
Your controller and robot now **keep in touch** all the time. If the messages stop, the robot stops — no more runaway robots.

In **Battle Bot 4** you'll use the extra buttons for **curving**, **turbo** and an **attack**, ready for sumo. Start with the robot:

https://makecode.microbit.org/#tutorial:github:cggs-matthew-pham/cggs-kitronik-move-tutorials/stem-battlebot-4
