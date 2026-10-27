### @title Battle Bot 2: Arcade Controller

### @description Swap the micro:bit remote for an Arcade controller - more buttons, more moves.

### @preferredEditor blocks

### @explicitHints true

# Battle Bot 2: Arcade Controller

```package
radio
```

```template
let channel = ""
// CHANGE THIS: the SAME icon name as your robot, e.g. duck
channel = "duck"
// CHANGE THIS: the SAME group number as your robot
radio.setGroup(101)
scene.setBackgroundColor(15)
```

## Introduction @showdialog
Your micro:bit remote only had **two buttons**, so it could only send **three** commands.

An Arcade controller has a D-pad, **A**, **B** and **Menu**. Today you'll use it to drive your robot with all five moves.

**Your robot code doesn't change at all.** Keep the robot micro:bit from Battle Bot 1 in the Move. Only the remote is new.

## Step 1: Match Your Robot
Your template has two lines to change. Both must **match your robot exactly**:
- ``||radio:radio set group||`` — your team's group number
- ``||variables:set channel to||`` — your robot's icon name, e.g. **duck**

Remember the protocol from Battle Bot 1:

| Number | Move |
|---|---|
| 0 | Spin left |
| 1 | Spin right |
| 2 | Stop |
| 3 | Forward |
| 4 | Reverse |

```blocks
let channel = ""
channel = "duck"
radio.setGroup(101)
scene.setBackgroundColor(15)
```

## Step 2: Show Your Bot on Screen
From ``||sprites:Sprites||``, drag ``||variables:set mySprite to sprite of kind Player||`` into ``||loops:on start||``. Rename the variable **bot** and draw your robot in the image editor.

```blocks
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
```

## Step 3: Up to Go Forward
From ``||controller:Controller||``, drag ``||controller:on up button pressed||``. Inside it:
- ``||radio:radio send value||`` ``||variables:channel||`` = **3**
- ``||sprites:bot say||`` **"forward"**

```blocks
controller.up.onEvent(ControllerButtonEvent.Pressed, function () {
    radio.sendValue(channel, 3)
    bot.sayText("forward")
})
```

## Step 4: Let Go to Stop
This is the big change from your micro:bit remote.

Drag another ``||controller:on up button pressed||`` and change **pressed** to **released**. Inside it:
- ``||radio:radio send value||`` ``||variables:channel||`` = **2**
- ``||sprites:bot say||`` **"stop"**

Now you **hold** to drive and **let go** to stop — no more pressing A+B!

```blocks
controller.up.onEvent(ControllerButtonEvent.Released, function () {
    radio.sendValue(channel, 2)
    bot.sayText("stop")
})
```

## Step 5: The Other Three Directions
Do the same for the rest of the D-pad. Each one needs a **pressed** block and a **released** block:

- ``||controller:down||`` pressed → **4** (reverse)
- ``||controller:left||`` pressed → **0** (spin left)
- ``||controller:right||`` pressed → **1** (spin right)
- Every **released** → **2** (stop)

Tip: right-click a block and choose **Duplicate** to save time.

```blocks
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

## Step 6: Test in the Simulator
The simulator can't reach your real robot, but you can check your buttons.

Use the arrow keys on your keyboard. The bot should say the right move when you press, and **"stop"** when you let go.

## Step 7: Download to Your Controller
Click **Download** and choose your **micro:bit V2** Arcade hardware. Flash it to the micro:bit in your Arcade controller.

Switch on your robot (still running Battle Bot 1), then your controller. Drive!

If the robot doesn't respond, check the **group** and **name** match exactly — spelling and capitals count.

## Step 8: Play and Notice
Play a game of soccer. Then think about this:

Radio messages can sometimes get **lost**. What would happen if the **"stop"** message got lost when you let go of a button?

Try it: drive forward, then switch the controller **off** while holding up. What does the robot do?

## Complete! @showdialog
You swapped the remote — and didn't change the robot at all. That works because both use the same **protocol**: the same numbers mean the same moves.

But you've also found a problem: if a message is lost, your robot can run away. In **Battle Bot 3** you'll add a **safety stop** so that can never happen. Start with the robot:

https://makecode.microbit.org/#tutorial:github:cggs-matthew-pham/cggs-kitronik-move-tutorials/stem-battlebot-3
