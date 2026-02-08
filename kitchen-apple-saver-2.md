# Kitchen Apple Saver

## Part 1: Collect Fresh Apples @showdialog
Stop food waste by collecting apples before time runs out! In Australia, 7.6 million tonnes of food is wasted each year. Every apple saved counts!

## Step 1: Set the Background
From ``||scene:Scene||``, drag ``||scene:set background image||`` into ``||loops:on start||``. Click the grey box and draw a kitchen or garden background.
```blocks
scene.setBackgroundImage(img`
    `)
```

## Step 2: Create the Player
From ``||sprites:Sprites||``, drag ``||variables:set mySprite to||`` and rename it to ``||variables:mySprite||``. Click the grey box and draw your character (or use the default person sprite).
```blocks
let mySprite: Sprite = null
mySprite = sprites.create(img`
    `, SpriteKind.Player)
```

## Step 3: Add Movement Controls
From ``||controller:Controller||``, drag ``||controller:move mySprite with buttons||``. Change to ``||variables:mySprite||`` with vx: 100 and vy: 100 for full directional movement.
```blocks
let mySprite: Sprite = null
mySprite = sprites.create(img`
    `, SpriteKind.Player)
controller.moveSprite(mySprite, 100, 100)
```

## Step 4: Set Up Score
From ``||info:Info||``, drag ``||info:set score to 0||``.
```blocks
info.setScore(0)
```

## Step 5: Start the Timer
From ``||info:Info||``, drag ``||info:start countdown||`` and set it to 30 seconds. This gives players time to collect apples!
```blocks
info.startCountdown(30)
```

## Step 6: Spawn Fresh Apples
From ``||game:Game||``, drag ``||game:on game update every 1000 ms||`` (every 1 second). Create a variable ``||variables:apple||`` and make a sprite with a fresh apple image and kind ``||sprites:Food||``.
```blocks
let apple: Sprite = null
game.onUpdateInterval(1000, function () {
    apple = sprites.create(img`
        `, SpriteKind.Food)
})
```

## Step 7: Position Apples Randomly
From ``||sprites:Sprites||``, add ``||sprites:set mySprite position||``. Change to ``||variables:apple||``. For x, use ``||math:pick random 10 to 150||`` from ``||math:Math||``. For y, use ``||math:pick random 10 to 110||``.
```blocks
let apple: Sprite = null
game.onUpdateInterval(1000, function () {
    apple = sprites.create(img`
        `, SpriteKind.Food)
    apple.setPosition(randint(10, 150), randint(10, 110))
})
```

## Step 8: Collect Apples for Points
From ``||sprites:Sprites||``, drag ``||sprites:on sprite overlaps||``. Set first kind to ``||sprites:Player||`` and second to ``||sprites:Food||``. Inside, add ``||info:change score by 1||`` and ``||sprites:destroy otherSprite||``.
```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    info.changeScoreBy(1)
    sprites.destroy(otherSprite)
})
```

## Step 9: Game Over When Time Runs Out
From ``||info:Info||``, drag ``||info:on countdown end||`` into your workspace. Inside, add ``||game:game over WIN||`` from ``||game:Game||``.
```blocks
info.onCountdownEnd(function () {
    game.gameOver(true)
})
```

## Complete! 
Great job! You've created a simple apple collecting game. Move around to collect as many apples as possible before time runs out!

**Did you know?** Fresh apples can last 1-2 months when properly refrigerated, but only 1-2 weeks at room temperature!

Ready for more challenge? Try Part 2 to add mouldy apples, spray weapons, and power-ups!

## Part 2: Battle the Mould @showdialog
Time to level up! Add mouldy apples that chase you, a cleaning spray weapon, and refrigerator power-ups. Can you survive the mould invasion?

## Step 1: Create PowerUp Sprite Kind
At the top of your workspace, add a ``||sprites:SpriteKind||`` block (found in Sprites > Advanced). Inside, create a new kind called ``||sprites:PowerUp||``.
```blocks
namespace SpriteKind {
    export const PowerUp = SpriteKind.create()
}
```

## Step 2: Add Lives
In ``||loops:on start||``, add ``||info:set life to 3||`` from ``||info:Info||``. Now you can take damage from mould!
```blocks
info.setLife(3)
```

## Step 3: Create Spray Flag Variable
From ``||variables:Variables||``, click "Make a Variable" and name it ``||variables:sprayFlag||``. In ``||loops:on start||``, set ``||variables:sprayFlag to 1||``. This tracks if you can spray.
```blocks
let sprayFlag = 0
sprayFlag = 1
```

## Step 4: Add Random Chance for Mouldy Apples
Find your existing ``||game:on game update every 1000 ms||`` block where apples spawn. Before creating the apple, add an ``||logic:if then else||`` from ``||logic:Logic||``.
```blocks
game.onUpdateInterval(1000, function () {
    if (true) {
    	
    } else {
    	
    }
})
```

## Step 5: Set Mouldy Apple Chance
From ``||math:Math||``, drag ``||math:pick random true with 50% chance||`` into the if condition. Click the dropdown and change to ``||math:30% chance||``.
```blocks
game.onUpdateInterval(1000, function () {
    if (Math.percentChance(30)) {
    	
    } else {
    	
    }
})
```

## Step 6: Create Mouldy Apple Sprite
Create a variable ``||variables:mouldyApple||``. In the ``||logic:if||`` section (30% chance), create a sprite with a brown/grey mouldy apple image and kind ``||sprites:Enemy||``.
```blocks
let mouldyApple: Sprite = null
game.onUpdateInterval(1000, function () {
    if (Math.percentChance(30)) {
        mouldyApple = sprites.create(img`
            `, SpriteKind.Enemy)
    } else {
    	
    }
})
```

## Step 7: Position Mouldy Apple
Add ``||sprites:set mySprite position||`` for ``||variables:mouldyApple||`` with random x (10 to 150) and y (10 to 110).
```blocks
let mouldyApple: Sprite = null
game.onUpdateInterval(1000, function () {
    if (Math.percentChance(30)) {
        mouldyApple = sprites.create(img`
            `, SpriteKind.Enemy)
        mouldyApple.setPosition(randint(10, 150), randint(10, 110))
    } else {
    	
    }
})
```

## Step 8: Make Mouldy Apple Chase Player
From ``||sprites:Sprites||``, drag ``||sprites:set mySprite follow||``. Change to ``||variables:mouldyApple||`` following ``||variables:mySprite||`` at speed 10.
```blocks
let mySprite: Sprite = null
let mouldyApple: Sprite = null
game.onUpdateInterval(1000, function () {
    if (Math.percentChance(30)) {
        mouldyApple = sprites.create(img`
            `, SpriteKind.Enemy)
        mouldyApple.setPosition(randint(10, 150), randint(10, 110))
        mouldyApple.follow(mySprite, 10)
    } else {
    	
    }
})
```

## Step 9: Move Fresh Apple to Else
Take your existing ``||variables:apple||`` sprite creation code and move it into the ``||logic:else||`` section. Now 70% spawn fresh apples, 30% spawn mouldy!
```blocks
let apple: Sprite = null
let mouldyApple: Sprite = null
game.onUpdateInterval(1000, function () {
    if (Math.percentChance(30)) {
        mouldyApple = sprites.create(img`
            `, SpriteKind.Enemy)
        mouldyApple.setPosition(randint(10, 150), randint(10, 110))
        mouldyApple.follow(mySprite, 10)
    } else {
        apple = sprites.create(img`
            `, SpriteKind.Food)
        apple.setPosition(randint(10, 150), randint(10, 110))
    }
})
```

## Step 10: Regenerate Spray
At the very end of your spawn interval (after the if/else), add ``||variables:set sprayFlag to 1||``. This gives you a new spray every second.
```blocks
let sprayFlag = 0
let apple: Sprite = null
let mouldyApple: Sprite = null
game.onUpdateInterval(1000, function () {
    if (Math.percentChance(30)) {
        mouldyApple = sprites.create(img`
            `, SpriteKind.Enemy)
        mouldyApple.setPosition(randint(10, 150), randint(10, 110))
        mouldyApple.follow(mySprite, 10)
    } else {
        apple = sprites.create(img`
            `, SpriteKind.Food)
        apple.setPosition(randint(10, 150), randint(10, 110))
    }
    sprayFlag = 1
})
```

## Step 11: Shoot Spray on A Button
From ``||controller:Controller||``, drag ``||controller:on A button pressed||`` into your workspace. Inside, add an ``||logic:if then||`` checking if ``||variables:sprayFlag > 0||``.
```blocks
let sprayFlag = 0
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    if (sprayFlag > 0) {
    	
    }
})
```

## Step 12: Create Spray Projectile
Create a variable ``||variables:projectile||``. From ``||sprites:Sprites||``, drag ``||sprites:set projectile to projectile from mySprite||``. Draw a small spray/water droplet. Set vx to 50 (fires right) and vy to 0.
```blocks
let mySprite: Sprite = null
let projectile: Sprite = null
let sprayFlag = 0
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    if (sprayFlag > 0) {
        projectile = sprites.createProjectileFromSprite(img`
            `, mySprite, 50, 0)
    }
})
```

## Step 13: Use Up Spray
Add ``||variables:set sprayFlag to 0||`` after creating the projectile so you can't spam spray.
```blocks
let mySprite: Sprite = null
let projectile: Sprite = null
let sprayFlag = 0
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    if (sprayFlag > 0) {
        projectile = sprites.createProjectileFromSprite(img`
            `, mySprite, 50, 0)
        sprayFlag = 0
    }
})
```

## Step 14: Spray Destroys Mould
From ``||sprites:Sprites||``, drag ``||sprites:on sprite overlaps||`` into your workspace. Set first kind to ``||sprites:Projectile||`` and second to ``||sprites:Enemy||``. Destroy both the mould and the spray.
```blocks
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Enemy, function (sprite, otherSprite) {
    sprites.destroy(otherSprite)
    sprites.destroy(sprite)
})
```

## Step 15: Mould Damages Player
Drag another ``||sprites:on sprite overlaps||``. Set first kind to ``||sprites:Player||`` and second to ``||sprites:Enemy||``. Add ``||info:change life by -1||`` and ``||sprites:destroy otherSprite||``.
```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (sprite, otherSprite) {
    info.changeLifeBy(-1)
    sprites.destroy(otherSprite)
})
```

## Step 16: Game Over on No Lives
From ``||info:Info||``, drag ``||info:on life zero||`` into your workspace. Add ``||game:game over LOSE||``.
```blocks
info.onLifeZero(function () {
    game.gameOver(false)
})
```

## Step 17: Spawn Fridge Power-Up
From ``||game:Game||``, drag a new ``||game:on game update every 5000 ms||`` (every 5 seconds). Create a ``||variables:fridge||`` sprite with a refrigerator image and kind ``||sprites:PowerUp||``.
```blocks
let fridge: Sprite = null
game.onUpdateInterval(5000, function () {
    fridge = sprites.create(img`
        `, SpriteKind.PowerUp)
})
```

## Step 18: Position Fridge
Add ``||sprites:set mySprite position||`` for ``||variables:fridge||`` with random x and y values.
```blocks
let fridge: Sprite = null
game.onUpdateInterval(5000, function () {
    fridge = sprites.create(img`
        `, SpriteKind.PowerUp)
    fridge.setPosition(randint(10, 150), randint(10, 110))
})
```

## Step 19: Collect Fridge for Extra Life
Drag ``||sprites:on sprite overlaps||``. Set first kind to ``||sprites:Player||`` and second to ``||sprites:PowerUp||``. Add ``||sprites:destroy otherSprite||`` and ``||info:change life by 1||``.
```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.PowerUp, function (sprite, otherSprite) {
    sprites.destroy(otherSprite)
    info.changeLifeBy(1)
})
```

## Complete! @showdialog
Excellent work! Now your game has real challenge. Dodge mouldy apples, use your spray wisely, and grab fridges to survive!

**Did you know?** Proper refrigeration is one of the most effective ways to prevent food waste. It can extend food life by up to 5-7 days!

**Extension Ideas:**
- Make mould move faster over time
- Add visual effects when sprites are destroyed
- Add food waste facts when collecting power-ups
- Make spray shoot in the direction you're moving
