# Remember the Player's Name

## Introduction @showdialog
Learn how to save and remember the player's name between game sessions using the Settings extension!

## Step 1: Add the Settings Extension
We need the Settings extension so the game can remember data between runs.

- Click **Extensions**
- Search for **settings**
- Add the **settings-blocks** extension

**NOTE:** For this tutorial, the **settings-blocks** extension has already been included.

## Step 2: Create a Name Variable
From ``||variables:Variables||``, click "Make a Variable" and name it ``||variables:name||``. Drag ``||variables:set name to||`` into ``||loops:on start||``. From ``||text:Text||`` (under Advanced), add an empty text block ``||text:""||``.
```blocks
let name = ""
```

## Step 3: Check if Name is Already Saved
From ``||logic:Logic||``, add an ``||logic:if then else||`` block. From ``||blockSettings:Settings||`` (under Advanced), drag ``||blockSettings:setting with "name" exists||`` into the condition.
```blocks
let name = ""
if (blockSettings.exists("name")) {
    
} else {
    
}
```

## Step 4: Read the Saved Name
From ``||blockSettings:Settings||``, drag ``||blockSettings:read string "name"||`` into the ``||logic:if||`` section and assign it to ``||variables:name||``.
```blocks
let name = ""
if (blockSettings.exists("name")) {
    name = blockSettings.readString("name")
} else {
    
}
```

## Step 5: Ask for Name and Save It
In the ``||logic:else||`` section, use ``||game:ask for string||`` from ``||game:Game||`` and save the result. Then use ``||blockSettings:write string||`` from ``||blockSettings:Settings||`` to save it.
```blocks
let name = ""
if (blockSettings.exists("name")) {
    name = blockSettings.readString("name")
} else {
    name = game.askForString("What is your name?")
    blockSettings.writeString("name", name)
}
```

## Step 6: Greet the Player
After the if block, add ``||game:splash||`` from ``||game:Game||``. Use ``||text:join||`` from ``||text:Text||`` to combine "Hello, ", ``||variables:name||``, and "!".
```blocks
let name = ""
if (blockSettings.exists("name")) {
    name = blockSettings.readString("name")
} else {
    name = game.askForString("What is your name?")
    blockSettings.writeString("name", name)
}
game.splash("Hello, " + name + "!")
```

## Step 7: Test the Game
Run your game! The first time it asks for your name. Every time after, it remembers automatically.

## Step 8: Create a Function
From ``||functions:Functions||`` (under Advanced), click "Make a Function". Name it ``||functions:getAndDisplayPlayerName||`` and click Done.
```blocks
function getAndDisplayPlayerName () {
    
}
```

## Step 9: Move Code into Function
Drag your if/else block and splash message into the function. Keep ``||variables:let name = ""||`` at the top of your workspace (outside the function).
```blocks
function getAndDisplayPlayerName () {
    let name = ""
    if (blockSettings.exists("name")) {
        name = blockSettings.readString("name")
    } else {
        name = game.askForString("What is your name?")
        blockSettings.writeString("name", name)
    }
    game.splash("Hello, " + name + "!")
}
```

## Step 10: Call the Function
From ``||functions:Functions||``, drag ``||functions:call getAndDisplayPlayerName||`` into ``||loops:on start||``.
```blocks
function getAndDisplayPlayerName () {
    let name = ""
    if (blockSettings.exists("name")) {
        name = blockSettings.readString("name")
    } else {
        name = game.askForString("What is your name?")
        blockSettings.writeString("name", name)
    }
    game.splash("Hello, " + name + "!")
}
getAndDisplayPlayerName()
```

## Complete! @showdialog
Great work! Your game now remembers the player's name between sessions. This is useful for creating personalized experiences!
```package
settings-blocks=github:microsoft/pxt-settings-blocks
```