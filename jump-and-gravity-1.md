# Duck Jump Game

## Introduction @showdialog
Create a game where a duck jumps over obstacles!

In this tutorial you will:
- Create a player sprite
- Make it fall with gravity
- Jump using the Up button
- Move left and right

## Step 1: Set the Scene
From ``||scene:Scene||``, drag out a ``||scene:set background color||`` block and choose a colour you like.
```blocks
scene.setBackgroundColor(9)
```

## Step 2: Create Your Player
From ``||sprites:Sprites||``, drag ``||variables:set mySprite to||`` into ``||loops:on start||``. Click the grey box to open the sprite editor and draw your character. Change the kind to ``||sprites:Player||``.
```blocks
let myPlayer: Sprite = null
scene.setBackgroundColor(9)
myPlayer = sprites.create(img`
    . . . . . . . . . . . . . . . . 
    . . . . . . . . . . . . . . . . 
    . . . . . . . . . b 5 5 b . . . 
    . . . . . . b b b b b b . . . . 
    . . . . . b b 5 5 5 5 5 b . . . 
    . b b b b b 5 5 5 5 5 5 5 b . . 
    . b d 5 b 5 5 5 5 5 5 5 5 b . . 
    . . b 5 5 b 5 d 1 f 5 d 4 f . . 
    . . b d 5 5 b 1 f f 5 4 4 c . . 
    b b d b 5 5 5 d f b 4 4 4 4 b . 
    b d d c d 5 5 b 5 4 4 4 4 4 4 b 
    c d d d c c b 5 5 5 5 5 5 5 b . 
    c b d d d d d 5 5 5 5 5 5 5 b . 
    . c d d d d d d 5 5 5 5 5 d b . 
    . . c b d d d d d 5 5 5 b b . . 
    . . . c c c c c c c c b b . . . 
    `, SpriteKind.Player)
```

## Step 3: Position Your Player
From ``||sprites:Sprites||``, drag ``||sprites:set mySprite position to x y||`` and change it to ``||variables:myPlayer||``. Set x to **20** and y to **60**.
```blocks
let myPlayer: Sprite = null
myPlayer = sprites.create(img`.`, SpriteKind.Player)
myPlayer.setPosition(20, 60)
```

## Step 4: Add Gravity
We use ``||sprites:ay||`` (acceleration in the y direction) to make the player fall downward. From ``||sprites:Sprites||``, find ``||sprites:set mySprite ax to||``, change it to ``||variables:myPlayer||``, switch **ax** to **ay**, and set the value to **500**.

A higher number means faster falling!
```blocks
let myPlayer: Sprite = null
myPlayer = sprites.create(img`.`, SpriteKind.Player)
myPlayer.setPosition(20, 60)
myPlayer.ay = 500
```

## Step 5: Add Left and Right Movement
From ``||controller:Controller||``, drag ``||controller:move mySprite with buttons||`` and change it to ``||variables:myPlayer||``. Set **vx** to **100** and **vy** to **0** — this lets the player move left and right only.
```blocks
let myPlayer: Sprite = null
myPlayer = sprites.create(img`.`, SpriteKind.Player)
myPlayer.setPosition(20, 60)
myPlayer.ay = 500
controller.moveSprite(myPlayer, 100, 0)
```

## Step 6: Make the Player Jump
From ``||controller:Controller||``, drag ``||controller:on up button pressed||`` into your workspace.

Inside it, set ``||variables:myPlayer||`` **vy** to **-150**. The negative number makes the player shoot upward.

``||sprites:vy||`` is the vertical speed. Negative = up, positive = down.
```blocks
let myPlayer: Sprite = null
controller.up.onEvent(ControllerButtonEvent.Pressed, function () {
    myPlayer.vy = -150
})
```

## Step 7: Create the Floor
Now we need something to stop the player falling forever! From ``||loops:Loops||``, drag a ``||loops:forever||`` block into your workspace.

Inside it, add an ``||logic:if then||`` block from ``||logic:Logic||``. Set the condition to check if ``||variables:myPlayer||`` **y** is greater than or equal to **110**.
```blocks
let myPlayer: Sprite = null
forever(function () {
    if (myPlayer.y >= 110) {
    	
    }
})
```

## Step 8: Stop Falling at the Floor
Inside the **if** block, we need two things:

1. Set ``||variables:myPlayer||`` **vy** to **0** to stop downward movement
2. Set ``||variables:myPlayer||`` **y** to **110** to snap to the floor

This acts like a solid ground at y position 110.
```blocks
let myPlayer: Sprite = null
forever(function () {
    if (myPlayer.y >= 110) {
        myPlayer.vy = 0
        myPlayer.y = 110
    }
})
```

## Complete! @showdialog
Your duck can now jump and move left and right!

**Try these challenges:**
- Change **vy** in the jump to **-200** — what happens?
- Change **ay** to **200** — what does that feel like?
- Add a food sprite and make a score when you collect it

Can you add obstacles to dodge?
