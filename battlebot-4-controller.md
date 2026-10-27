### @title Battle Bot 4: Battle Upgrades (Controller)

### @description Add curving, turbo and attack buttons to your Arcade controller, ready for sumo.

### @preferredEditor blocks

### @explicitHints true

# Battle Bot 4: Battle Upgrades (Controller)

```package
radio
```

```template
let command = 0
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

## Introduction @showdialog
Your robot now knows three new things: **curves**, **turbo** and **attack**. Time to give the driver buttons for them.

| Buttons | Number | Move |
|---|---|---|
| Up + Left | 5 | Curve left |
| Up + Right | 6 | Curve right |
| Hold B | +10 | Turbo |
| Press A | 99 | Attack! |

Your template is your code from Battle Bot 3. Check the **group** and **name** still match your robot.

## Step 1: Combine Buttons to Curve
A micro:bit can't easily tell you "up **and** left". An Arcade controller can.

Inside the **up** branch, under ``||variables:set command to 3||``, add another ``||logic:if||``:
- If ``||controller:is left button pressed||`` → **5**
- Else if ``||controller:is right button pressed||`` → **6**

This is a **nested if** — a decision inside a decision. The robot only curves if up is **also** held.

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

## Step 2: Hold B for Turbo
After the big ``||logic:if||`` block, but **before** sending, add:
- If ``||controller:is B button pressed||`` → ``||variables:change command by 10||``

So **B** + **up** sends **13**. Your robot knows that anything 10 or more means turbo — and it works with **every** move, without adding a single new move block.

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

## Step 3: Press A to Attack (Optional)
Only needed if your robot has a servo arm.

An attack happens **once** per press, not over and over — so it gets its own event block, not the update loop.

From ``||controller:Controller||``, drag ``||controller:on A button pressed||``. Inside it:
- ``||radio:radio send value||`` ``||variables:channel||`` = **99**
- ``||scene:camera shake by 4 pixels for 200 ms||`` — feedback for the driver!

```blocks
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    radio.sendValue(channel, 99)
    scene.cameraShake(4, 200)
})
```

## Step 4: Test in the Simulator
Use the arrow keys, **Z** (A) and **X** (B). Check the number above your bot:
- Up + Left = **5**, Up + Right = **6**
- Up + B = **13**, nothing pressed = **2**
- Z makes the screen shake

## Step 5: Download and Battle
Download to your Arcade controller. Your robot should be running **Battle Bot 4: Battle Upgrades (Robot)**.

Check everything works, then head to the sumo ring!

## Complete! @showdialog
You've built a complete battle bot system, one upgrade at a time:
1. A remote control robot
2. A better controller — same robot code
3. A safety stop
4. Battle upgrades

The big idea running through all of it is the **protocol**: controller and robot agree on what each number means. Adding new moves was just agreeing on new numbers.

**Challenge:** use the **Menu** button to switch between three speed settings, and show the current setting on screen.
