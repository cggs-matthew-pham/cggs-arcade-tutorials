### @title Battle Bot: The Controller

### @description Use an Arcade controller to drive a Kitronik Move robot over radio.

### @preferredEditor blocks

### @explicitHints true

# Battle Bot: The Controller

```package
radio
```

```template
let command = 0
radio.setGroup(1)
scene.setBackgroundColor(15)
```

## Introduction @showdialog
Your robot is listening. Now build the **controller** that drives it.

A micro:bit only has two buttons. An Arcade controller has **eight** — a D-pad, **A**, **B** and **Menu** — which is exactly what a battle bot driver needs.

Your controller will check which buttons are held, turn them into **one number**, and send that number to the robot 10 times every second.

## Step 1: Match Your Radio Group
Your template has ``||radio:radio set group 1||``. Change **1** to the **same group number** you used on your robot.

```blocks
let command = 0
radio.setGroup(1)
scene.setBackgroundColor(15)
```

## Step 2: Show Your Bot on Screen
From ``||sprites:Sprites||``, drag ``||variables:set mySprite to sprite of kind Player||`` into ``||loops:on start||``. Rename the variable **bot** and draw your battle bot in the image editor.

Your controller now has a screen — use it! We'll show the driver what the robot is doing.

```blocks
let command = 0
radio.setGroup(1)
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
- ``||variables:set command to 0||`` — assume "stop" unless a button is held
- ``||logic:if||`` ``||controller:is up button pressed||`` then ``||variables:set command to 1||``
- ``||radio:radio send number||`` ``||variables:command||``
- ``||sprites:bot say||`` ``||variables:command||``

Why send all the time, even when nothing is pressed? Your robot has a **safety stop** — if it doesn't hear from you for half a second, it stops. Sending constantly keeps it alive.

```blocks
game.onUpdateInterval(100, function () {
    command = 0
    if (controller.up.isPressed()) {
        command = 1
    }
    radio.sendNumber(command)
    bot.sayText(command)
})
```

## Step 4: Add Reverse and Spins
Click **+** on your ``||logic:if||`` to add ``||logic:else if||`` branches:

- ``||controller:down||`` → **2**
- ``||controller:left||`` → **3**
- ``||controller:right||`` → **4**

```blocks
game.onUpdateInterval(100, function () {
    command = 0
    if (controller.up.isPressed()) {
        command = 1
    } else if (controller.down.isPressed()) {
        command = 2
    } else if (controller.left.isPressed()) {
        command = 3
    } else if (controller.right.isPressed()) {
        command = 4
    }
    radio.sendNumber(command)
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
    command = 0
    if (controller.up.isPressed()) {
        command = 1
        if (controller.left.isPressed()) {
            command = 5
        } else if (controller.right.isPressed()) {
            command = 6
        }
    } else if (controller.down.isPressed()) {
        command = 2
    } else if (controller.left.isPressed()) {
        command = 3
    } else if (controller.right.isPressed()) {
        command = 4
    }
    radio.sendNumber(command)
    bot.sayText(command)
})
```

## Step 6: Hold B for Turbo
After the big ``||logic:if||`` block (but before sending), add:
- If ``||controller:is B button pressed||`` → ``||variables:change command by 10||``

So holding **B** + **up** sends **11**. Your robot already knows that anything 10 or more means turbo.

```blocks
game.onUpdateInterval(100, function () {
    command = 0
    if (controller.up.isPressed()) {
        command = 1
        if (controller.left.isPressed()) {
            command = 5
        } else if (controller.right.isPressed()) {
            command = 6
        }
    } else if (controller.down.isPressed()) {
        command = 2
    } else if (controller.left.isPressed()) {
        command = 3
    } else if (controller.right.isPressed()) {
        command = 4
    }
    if (controller.B.isPressed()) {
        command += 10
    }
    radio.sendNumber(command)
    bot.sayText(command)
})
```

## Step 7: Press A to Attack
An attack happens **once** per press, not continuously — so it gets its own event.

From ``||controller:Controller||``, drag ``||controller:on A button pressed||``. Inside it:
- ``||radio:radio send number 99||``
- ``||scene:camera shake by 4 pixels for 200 ms||`` — some feedback for the driver!

```blocks
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    radio.sendNumber(99)
    scene.cameraShake(4, 200)
})
```

## Step 8: Test in the Simulator
The simulator can't reach your real robot, but you can still check your logic.

Use the arrow keys, **Z** (A) and **X** (B) on your keyboard. Check the number above your bot:
- Up = 1, Up + Left = 5, Up + B = 11
- Nothing pressed = 0

## Step 9: Download to Your Controller
Click **Download** and choose your **micro:bit V2** Arcade hardware. Flash the file to the micro:bit in your Arcade controller.

Switch on your robot, then the controller. Drive!

If the robot doesn't respond: check both use the same radio group, and that the robot code is running (small square showing).

## Complete! @showdialog
You've built a custom controller for a real robot.

The big idea is **encoding**: eight buttons get squashed into one number, sent over radio, and decoded back into moves on the robot. Both programs have to agree on what every number means — that agreement is called a **protocol**.

**Challenge:** use the **Menu** button to cycle through three speed settings, and show the current setting on screen.
