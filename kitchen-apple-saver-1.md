# Kitchen Apple Saver

## Part 1: Collect Fresh Apples @showdialog
Stop food waste by collecting apples before time runs out! In Australia, 7.6 million tonnes of food is wasted each year. Every apple saved counts!

## Step 1: Set the Background
From ``||scene:Scene||``, drag ``||scene:set background image||`` into ``||loops:on start||``. Follow these steps to display kitchen tiles as the background image:
- Open the Agora file with the kitchen background code (kitchen-background.txt)
- Copy the code (Ctrl+A + Ctrl+C OR Cmd+A + Cmd+C)
- Click on the grey box in MakeCode
- Paste the code you copied into the sprite editor
  
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
