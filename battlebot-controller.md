### @title Battle Bot: The Controller

### @description Use an Arcade controller to drive a Kitronik Move robot over radio.

### @preferredEditor blocks

### @explicitHints true

# Battle Bot: The Controller

```package
radio
```

```template
let command = 2
let channel = ""
// CHANGE THIS: the SAME name as your robot
channel = "roger"
// CHANGE THIS: the SAME group number as your robot
radio.setGroup(101)
scene.setBackgroundColor(15)
```

## Introduction @showdialog
Your robot is listening. Now build the **controller** that drives it.

A micro:bit only has two buttons. An Arcade controller has **eight** — a D-pad, **A**, **B** and **Menu** — which is exactly what a battle bot driver needs.

Your controller will check which buttons are held, turn them into **one number**, and send it to your robot 10 times every second — using the same numbers as the soccer demo:

| Number | Move |
|---|---|
| 0 | Spin left |
| 1 | Spin right |
| 2 | Stop |
| 3 | Forward |
| 4 | Reverse |
| 5 | Curve left |
| 6 | Curve right |
| +10 | Turbo |
| 99 | Attack! |

## Step 1: Match Your Robot
Your template has two lines to change. Both must **match your robot exactly**:
- ``||radio:radio set group||`` — your team's group number
- ``||variables:set channel to||`` — your robot's name

```blocks
let command = 2
let channel = ""
channel = "roger"
radio.setGroup(101)
scene.setBackgroundColor(15)
```

## Step 2: Show Your Bot on Screen
From ``||sprites:Sprites||``, drag ``||variables:set mySprite to sprite of kind Player||`` into ``||loops:on start||``. Rename the variable **bot** and draw your battle bot in the image editor.

Your controller has a screen — use it! We'll show the driver what the robot is being told to do.

```blocks
let command = 2
let channel = ""
channel = "roger"
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
```

## Step 3: Send a Command 10 Times a Second
From ``||game:Game||``, drag ``||game:on game update every 100 ms||`` into the workspace.

Inside it:
- ``||variables:set command to 2||`` — assume "stop" unless a button is held
- ``||logic:if||`` ``||controller:is up button pressed||`` then ``||variables:set command to 3||``
- ``||radio:radio send value||`` ``||variables:channel||`` = ``||variables:command||``
- ``||sprites:bot say||`` ``||variables:command||``

In the demo, the remote only sent a message when you **pressed** a button. Why send all the time now? Your robot has a **safety stop** — if it doesn't hear from you for half a second, it stops. Sending constantly keeps it alive.

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

## Step 4: Add Reverse and Spins
Click **+** on your ``||logic:if||`` to add ``||logic:else if||`` branches:

- ``||controller:down||`` → **4**
- ``||controller:left||`` → **0**
- ``||controller:right||`` → **1**

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

## Step 5: Combine Buttons to Curve
A micro:bit can't easily tell you "up **and** left". An Arcade controller can.

Inside the **up** branch, add another ``||logic:if||``:
- If ``||controller:left||`` is also pressed → **5** (curve left)
- Else if ``||controller:right||`` is also pressed → **6** (curve right)

This is a **nested if** — a decision inside a decision.

```blocks
game.onUpdateInterval(100, function () {
    command = 2
    if (controller.up.isPressed()) {
        command = 3
        if (controller.left.isPressed()) {
            command = 5
        } else if (controller.right.isPressed()) {
            command = 6
        }
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

## Step 6: Hold B for Turbo
After the big ``||logic:if||`` block (but before sending), add:
- If ``||controller:is B button pressed||`` → ``||variables:change command by 10||``

So holding **B** + **up** sends **13**. Your robot already knows that anything 10 or more means turbo.

```blocks
game.onUpdateInterval(100, function () {
    command = 2
    if (controller.up.isPressed()) {
        command = 3
        if (controller.left.isPressed()) {
            command = 5
        } else if (controller.right.isPressed()) {
            command = 6
        }
    } else if (controller.down.isPressed()) {
        command = 4
    } else if (controller.left.isPressed()) {
        command = 0
    } else if (controller.right.isPressed()) {
        command = 1
    }
    if (controller.B.isPressed()) {
        command += 10
    }
    radio.sendValue(channel, command)
    bot.sayText(command)
})
```

## Step 7: Press A to Attack (Optional)
Only needed if your robot has a servo arm for **flag knock** battles.

An attack happens **once** per press, not continuously — so it gets its own event.

From ``||controller:Controller||``, drag ``||controller:on A button pressed||``. Inside it:
- ``||radio:radio send value||`` ``||variables:channel||`` = **99**
- ``||scene:camera shake by 4 pixels for 200 ms||`` — some feedback for the driver!

```blocks
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    radio.sendValue(channel, 99)
    scene.cameraShake(4, 200)
})
```

## Step 8: Test in the Simulator
The simulator can't reach your real robot, but you can still check your logic.

Use the arrow keys, **Z** (A) and **X** (B) on your keyboard. Check the number above your bot:
- Nothing pressed = 2
- Up = 3, Up + Left = 5, Up + B = 13

## Step 9: Download to Your Controller
Click **Download** and choose your **micro:bit V2** Arcade hardware. Flash the file to the micro:bit in your Arcade controller.

Switch on your robot, then the controller. Drive!

If the robot doesn't respond, check:
- Same **group number** on both
- Same **name** on both (spelling and capitals count!)
- The robot shows its name and a small square when switched on

## Complete! @showdialog
You've built a custom controller for a real robot — ready for sumo, soccer or flag knock.

The big idea is **encoding**: eight buttons get squashed into one number, sent over radio, and decoded back into moves on the robot. Both programs have to agree on what every number means — that agreement is called a **protocol**.

**Challenge:** use the **Menu** button to cycle through three speed settings, and show the current setting on screen.
