# Falling Apple Saver

## Part 1 Introduction @showdialog
Create a game where you catch falling apples to prevent food waste!

## Step 1: Set the Scene
From ``||scene:Scene||``, drag out a ``||scene:set background color||`` block and choose blue (color 9).
```blocks
scene.setBackgroundColor(9)
```

## Step 2: Show the Problem 
From ``||game:Game||``, add a ``||game:show long text||`` block to tell players about food waste at school.
```blocks
scene.setBackgroundColor(9)
game.showLongText("Teachers reported fruit to be the number one food they see most commonly wasted at school, with half eaten fruit a regular feature in the playground.", DialogLayout.Full)
```

## Step 3: Explain the Mission
Add another ``||game:show long text||`` block from ``||game:Game||`` to explain the player's mission.
```blocks
game.showLongText("Your mission is to catch the falling apples, to increase your score and avoid food waste!", DialogLayout.Full)
```

## Step 4: Set Starting Lives
From ``||info:Info||``, drag out ``||info:set life to||`` and change the value to 3.
```blocks
info.setLife(3)
```

## Step 5: Create the Ground
From ``||sprites:Sprites||``, drag ``||variables:set mySprite to||`` into ``||loops:on start||``. Rename it to ``||variables:ground||``. Click the grey box and choose the Ground image. Then drag ``||sprites:set mySprite y to||`` below it and change it to 112.
```blocks
let ground = sprites.create(assets.image`Ground`, SpriteKind.Player)
ground.y = 112
```

## Step 6: Create New Sprite Kind
At the very top of your workspace, add a ``||sprites:SpriteKind||`` block (found under Advanced). Inside it, create a new kind called ``||sprites:Ground||``. Then go back to your ground sprite and change its kind from Player to Ground.
```blocks
namespace SpriteKind {
    export const Ground = SpriteKind.create()
}
let ground = sprites.create(assets.image`Ground`, SpriteKind.Ground)
ground.y = 112
```

## Step 7: Create the Player
From ``||sprites:Sprites||``, drag another ``||variables:set mySprite to||`` block. Rename it to ``||variables:myPlayer||``. Click the grey box and choose the Player image.
```blocks
let myPlayer: Sprite = null
myPlayer = sprites.create(assets.image`Player`, SpriteKind.Player)
```

## Step 8: Position the Player
From ``||sprites:Sprites||``, add ``||sprites:set mySprite position to x y||``. Change mySprite to ``||variables:myPlayer||``, set x to 80 and y to 99.
```blocks
let myPlayer: Sprite = null
myPlayer = sprites.create(assets.image`Player`, SpriteKind.Player)
myPlayer.setPosition(80, 99)
```

## Step 9: Add Player Controls
From ``||controller:Controller||``, drag ``||controller:move mySprite with buttons||`` and change it to ``||variables:myPlayer||``. Set vx to 100 and vy to 0 so the player only moves left and right.
```blocks
let myPlayer: Sprite = null
myPlayer = sprites.create(assets.image`Player`, SpriteKind.Player)
myPlayer.setPosition(80, 99)
controller.moveSprite(myPlayer, 100, 0)
```

## Step 10: Start the Countdown
From ``||info:Info||``, drag ``||info:start countdown||`` and set it to 10 seconds.
```blocks
info.startCountdown(10)
```

## Step 11: Spawn Falling Apples
From ``||game:Game||``, drag ``||game:on game update every 500 ms||`` into your workspace. Change 500 to 1000. Inside it, create a new sprite called ``||variables:apple||`` using the Apple image. Change the sprite kind to ``||sprites:Food||``.
```blocks
let apple: Sprite = null
game.onUpdateInterval(1000, function () {
    apple = sprites.create(assets.image`Apple`, SpriteKind.Food)
})
```

## Step 12: Make Apples Fall
From ``||sprites:Sprites||``, drag ``||sprites:set mySprite velocity||`` into the game update. Change it to ``||variables:apple||`` and set vx to 0 and vy to 50 (positive means downward).
```blocks
let apple: Sprite = null
game.onUpdateInterval(1000, function () {
    apple = sprites.create(assets.image`Apple`, SpriteKind.Food)
    apple.setVelocity(0, 50)
})
```

## Step 13: Random Apple Position
From ``||sprites:Sprites||``, add ``||sprites:set mySprite position to x y||``. Change it to ``||variables:apple||``. For x, use ``||math:pick random 0 to 10||`` from ``||math:Math||`` and set it to 10 to 150. Set y to -10 so apples start above the screen.
```blocks
let apple: Sprite = null
game.onUpdateInterval(1000, function () {
    apple = sprites.create(assets.image`Apple`, SpriteKind.Food)
    apple.setVelocity(0, 50)
    apple.setPosition(randint(10, 150), -10)
})
```

## Step 14: Catch Apples for Points
From ``||sprites:Sprites||``, drag ``||sprites:on sprite of kind Player overlaps otherSprite of kind Player||`` into your workspace. Change the second kind to ``||sprites:Food||``. Inside, add ``||info:change score by 1||`` from ``||info:Info||`` and ``||sprites:destroy otherSprite||`` from ``||sprites:Sprites||``.
```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    info.changeScoreBy(1)
    sprites.destroy(otherSprite)
})
```

## Step 15: Penalty for Missed Apples
Drag another ``||sprites:on sprite overlaps||`` block. Set the first kind to ``||sprites:Ground||`` and second to ``||sprites:Food||``. Inside, add ``||sprites:destroy otherSprite||`` and ``||info:change life by -1||`` from ``||info:Info||``.
```blocks
sprites.onOverlap(SpriteKind.Ground, SpriteKind.Food, function (sprite, otherSprite) {
    sprites.destroy(otherSprite)
    info.changeLifeBy(-1)
})
```

## Step 16: Game Over - No Lives
From ``||info:Info||``, drag ``||info:on life zero||`` into your workspace. Inside, add ``||game:game over||`` from ``||game:Game||`` and set it to LOSE (the sad face).
```blocks
info.onLifeZero(function () {
    game.gameOver(false)
})
```

## Step 17: Game Over - Time's Up
From ``||info:Info||``, drag ``||info:on countdown end||`` into your workspace. Inside, add ``||game:game over||`` and set it to WIN (the happy face).
```blocks
info.onCountdownEnd(function () {
    game.gameOver(true)
})
```

## Complete! 
Great job! You've created an apple catching game. Try to catch as many apples as possible before time runs out!

Now try Part 2 to add knife throwing and apple slicing!



## Part 2 Introduction @showdialog
Add knife throwing to slice apples and share the fruit! This prevents even more food waste.

## Step 1: Show Slicing Instructions
In ``||loops:on start||``, add another ``||game:show long text||`` block from ``||game:Game||`` after your existing messages to explain the knife throwing mechanic.
```blocks
game.showLongText("You can also throw slicing knives at apples by pressing A, to share half your fruit and save even more food!", DialogLayout.Full)
```

## Step 2: Create Throws Variable
From ``||variables:Variables||``, click "Make a Variable" and name it ``||variables:throwsRemaining||``. In ``||loops:on start||``, drag ``||variables:set throwsRemaining to||`` and set it to 1.
```blocks
let throwsRemaining = 0
throwsRemaining = 1
```

## Step 3: Create Sliced Food Kind
At the top of your workspace, in your existing ``||sprites:SpriteKind||`` block, create another kind called ``||sprites:SlicedFood||`` for the apple halves.
```blocks
namespace SpriteKind {
    export const SlicedFood = SpriteKind.create()
    export const Ground = SpriteKind.create()
}
```

## Step 4: Throw Knife on A Button
From ``||controller:Controller||``, drag ``||controller:on A button pressed||`` into your workspace. Inside, add an ``||logic:if then||`` block from ``||logic:Logic||``. For the condition, use a ``||logic:comparison||`` block set to ``||variables:throwsRemaining||`` ``||logic:> 0||``.
```blocks
let throwsRemaining = 0
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    if (throwsRemaining > 0) {
    	
    }
})
```

## Step 5: Use a Throw
From ``||variables:Variables||``, drag ``||variables:change throwsRemaining by||`` inside the if statement and set it to -1.
```blocks
let throwsRemaining = 0
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    if (throwsRemaining > 0) {
        throwsRemaining += -1
    }
})
```

## Step 6: Create the Knife
Create a new variable called ``||variables:knife||``. From ``||sprites:Sprites||``, drag ``||variables:set mySprite to||`` inside the if statement. Change it to ``||variables:knife||``, choose the Knife image, and change the kind to ``||sprites:Projectile||``.
```blocks
let knife: Sprite = null
let throwsRemaining = 0
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    if (throwsRemaining > 0) {
        throwsRemaining += -1
        knife = sprites.create(assets.image`Knife`, SpriteKind.Projectile)
    }
})
```

## Step 7: Position the Knife
From ``||sprites:Sprites||``, drag ``||sprites:set mySprite position to x y||``. Change it to ``||variables:knife||``. For both x and y, drag the ``||variables:myPlayer x||`` and ``||variables:myPlayer y||`` value blocks from ``||variables:Variables||``.
```blocks
let myPlayer: Sprite = null
let knife: Sprite = null
let throwsRemaining = 0
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    if (throwsRemaining > 0) {
        throwsRemaining += -1
        knife = sprites.create(assets.image`Knife`, SpriteKind.Projectile)
        knife.setPosition(myPlayer.x, myPlayer.y)
    }
})
```

## Step 8: Knife Flies Upward
From ``||sprites:Sprites||``, drag ``||sprites:set mySprite velocity||`` and change it to ``||variables:knife||``. Set vx to 0 and vy to -150 (negative means upward).
```blocks
let myPlayer: Sprite = null
let knife: Sprite = null
let throwsRemaining = 0
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    if (throwsRemaining > 0) {
        throwsRemaining += -1
        knife = sprites.create(assets.image`Knife`, SpriteKind.Projectile)
        knife.setPosition(myPlayer.x, myPlayer.y)
        knife.setVelocity(0, -150)
    }
})
```

## Step 9: Knife Hits Apple
From ``||sprites:Sprites||``, drag ``||sprites:on sprite overlaps||`` into your workspace. Set the first kind to ``||sprites:Projectile||`` and the second to ``||sprites:Food||``.
```blocks
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Food, function (sprite, otherSprite) {
	
})
```

## Step 10: Create Left Apple Half
Create a new variable called ``||variables:appleLeft||``. Inside the overlap block, drag ``||variables:set mySprite to||`` from ``||sprites:Sprites||``, change it to ``||variables:appleLeft||``, choose the AppleLeft image, and set the kind to ``||sprites:SlicedFood||``.
```blocks
let appleLeft: Sprite = null
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Food, function (sprite, otherSprite) {
    appleLeft = sprites.create(assets.image`AppleLeft`, SpriteKind.SlicedFood)
})
```

## Step 11: Create Right Apple Half
Create a new variable called ``||variables:appleRight||``. Add another ``||variables:set mySprite to||`` block, change it to ``||variables:appleRight||``, choose the AppleRight image with kind ``||sprites:SlicedFood||``.
```blocks
let appleRight: Sprite = null
let appleLeft: Sprite = null
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Food, function (sprite, otherSprite) {
    appleLeft = sprites.create(assets.image`AppleLeft`, SpriteKind.SlicedFood)
    appleRight = sprites.create(assets.image`AppleRight`, SpriteKind.SlicedFood)
})
```

## Step 12: Apple Halves Fly Apart
From ``||sprites:Sprites||``, add two ``||sprites:set mySprite velocity||`` blocks. Set ``||variables:appleLeft||`` to vx: -10, vy: 50 and ``||variables:appleRight||`` to vx: 10, vy: 50 so they fly in opposite directions.
```blocks
let appleRight: Sprite = null
let appleLeft: Sprite = null
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Food, function (sprite, otherSprite) {
    appleLeft = sprites.create(assets.image`AppleLeft`, SpriteKind.SlicedFood)
    appleRight = sprites.create(assets.image`AppleRight`, SpriteKind.SlicedFood)
    appleLeft.setVelocity(-10, 50)
    appleRight.setVelocity(10, 50)
})
```

## Step 13: Position Apple Halves
From ``||sprites:Sprites||``, add ``||sprites:set mySprite position to x y||``. Change it to ``||variables:appleLeft||``. For x, use a ``||math:subtraction||`` block from ``||math:Math||`` with ``||variables:otherSprite x||`` minus 8. For y, use ``||variables:otherSprite y||``.
```blocks
let appleRight: Sprite = null
let appleLeft: Sprite = null
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Food, function (sprite, otherSprite) {
    appleLeft = sprites.create(assets.image`AppleLeft`, SpriteKind.SlicedFood)
    appleRight = sprites.create(assets.image`AppleRight`, SpriteKind.SlicedFood)
    appleLeft.setVelocity(-10, 50)
    appleRight.setVelocity(10, 50)
    appleLeft.setPosition(otherSprite.x - 8, otherSprite.y)
})
```

## Step 14: Position Right Half
Add another ``||sprites:set mySprite position to x y||`` block for ``||variables:appleRight||``. For x, use ``||math:addition||`` with ``||variables:otherSprite x||`` plus 8. For y, use ``||variables:otherSprite y||``.
```blocks
let appleRight: Sprite = null
let appleLeft: Sprite = null
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Food, function (sprite, otherSprite) {
    appleLeft = sprites.create(assets.image`AppleLeft`, SpriteKind.SlicedFood)
    appleRight = sprites.create(assets.image`AppleRight`, SpriteKind.SlicedFood)
    appleLeft.setVelocity(-10, 50)
    appleRight.setVelocity(10, 50)
    appleLeft.setPosition(otherSprite.x - 8, otherSprite.y)
    appleRight.setPosition(otherSprite.x + 8, otherSprite.y)
})
```

## Step 15: Remove Original Apple
From ``||sprites:Sprites||``, drag ``||sprites:destroy mySprite||`` to the end of the overlap block and change it to ``||variables:otherSprite||`` to remove the whole apple.
```blocks
let appleRight: Sprite = null
let appleLeft: Sprite = null
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Food, function (sprite, otherSprite) {
    appleLeft = sprites.create(assets.image`AppleLeft`, SpriteKind.SlicedFood)
    appleRight = sprites.create(assets.image`AppleRight`, SpriteKind.SlicedFood)
    appleLeft.setVelocity(-10, 50)
    appleRight.setVelocity(10, 50)
    appleLeft.setPosition(otherSprite.x - 8, otherSprite.y)
    appleRight.setPosition(otherSprite.x + 8, otherSprite.y)
    sprites.destroy(otherSprite)
})
```

## Step 16: Catch Sliced Apples
From ``||sprites:Sprites||``, drag ``||sprites:on sprite overlaps||`` into your workspace. Set first kind to ``||sprites:Player||`` and second to ``||sprites:SlicedFood||``. Inside, add ``||info:change score by 1||`` and ``||sprites:destroy otherSprite||``.
```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.SlicedFood, function (sprite, otherSprite) {
    info.changeScoreBy(1)
    sprites.destroy(otherSprite)
})
```

## Step 17: Penalty for Missed Slices
Drag another ``||sprites:on sprite overlaps||`` block. Set first kind to ``||sprites:Ground||`` and second to ``||sprites:SlicedFood||``. Add ``||sprites:destroy otherSprite||`` and ``||info:change life by -1||``.
```blocks
sprites.onOverlap(SpriteKind.Ground, SpriteKind.SlicedFood, function (sprite, otherSprite) {
    sprites.destroy(otherSprite)
    info.changeLifeBy(-1)
})
```

## Step 18: Clean Up Old Knives
Find your existing ``||game:on game update every 1000 ms||`` block where apples spawn. At the end, add ``||sprites:destroy mySprite||`` from ``||sprites:Sprites||`` and change it to ``||variables:knife||``.
```blocks
let knife: Sprite = null
let apple: Sprite = null
game.onUpdateInterval(1000, function () {
    apple = sprites.create(assets.image`Apple`, SpriteKind.Food)
    apple.setVelocity(0, 50)
    apple.setPosition(randint(10, 150), -10)
    sprites.destroy(knife)
})
```

## Step 19: Regenerate Throws
From ``||game:Game||``, drag a new ``||game:on game update every 500 ms||`` and change it to 1000. Inside, add an ``||logic:if then||`` from ``||logic:Logic||``. Set the condition to ``||variables:throwsRemaining||`` ``||logic:= 0||``. Inside the if, add ``||variables:change throwsRemaining by 1||``.
```blocks
let throwsRemaining = 0
game.onUpdateInterval(1000, function () {
    if (throwsRemaining == 0) {
        throwsRemaining += 1
    }
})
```

## Complete! @showdialog
Awesome! Now you can slice apples to share the fruit and earn even more points. Try to get a high score by catching whole apples AND sliced pieces!