### @title Remember the Player's Name

### @description Ask for the player’s name once, save it using settings, and greet them every time.

### @preferredEditor blocks

### @explicitHints true

  
# Remember the Player's Name
## Step 1: Add the Settings extension

We need the Settings extension so the game can remember data between runs.

  

- Click **Extensions**  

- Search for **settings**  

- Add the **settings-blocks** extension  

  

**NOTE** that for this tutorial, the **settings-block** extension has already been included

  

## Step 2: Create a variable for the player’s name

Create a variable called name and set it to an empty string.

  

- Open Variables → Make a variable → call it name

- Drag set name to into the workspace

- Open Advanced → Text

- Drag the empty text block "" into the value slot

  

```blocks

let name = ""

```

  

## Step 3: Check if a name is already saved

Use an if / else block to check if the setting "name" exists.

  

- Open Logic

- Add an if / else block

- Open Advanced → Settings

- Use exists "name" as the condition

  

In the next steps, we will:

- Read the name from settings if it exists

- Ask the player for their name if it does not

  

```blocks

let name = ""

if (blockSettings.exists("name")) {

  

} else {

  

}

```

  

## Step 4: Read the saved name

Inside the if block, read the saved name from settings.

  

```blocks

let name = ""

name = ""

if (blockSettings.exists("name")) {

    name = blockSettings.readString("name")

} else {

  

}

```

  

## Step 5: Ask for the name and save it

Inside the else block, ask the player for their name and save it.

  

```blocks

let name = ""

name = ""

if (blockSettings.exists("name")) {

    name = blockSettings.readString("name")

} else {

    name = game.askForString("What is your name?")

    blockSettings.writeString("name", name)

}

```

  

## Step 6: Greet the player

After the if block, display a greeting using the name variable.

  

```blocks

let name = ""

name = ""

if (blockSettings.exists("name")) {

    name = blockSettings.readString("name")

} else {

    name = game.askForString("What is your name?")

    blockSettings.writeString("name", name)

}

game.splash("Hello, " + name + "!")

```

  

## Step 7: Test the game

The first time the game runs, it asks for the player’s name.  

Every time after that, the name is remembered automatically.

  

## Step 8: Create a function for the name code

Now we will put the name and settings logic into a function so the main program stays clean.

  

- Open **Advanced → Functions**

- Click **Make a Function**

- Name it `getAndDisplayPlayerName`

- Click **Done**

  

You should now see a new block called:

- **function getAndDisplayPlayerName do**

  

```blocks

function getAndDisplayPlayerName () {

  

}

```

  

## Step 9: Move the name logic into the function

Move the code from Steps 2–6 into the function.

  

- Drag the **if / else** block into the function

- Drag the **game.splash("Hello, " + name + "!")** block into the function

- Leave **let name = ""** outside the function

  

```blocks

  

function getAndDisplayPlayerName () {

    let name = ""

    name = ""

    if (blockSettings.exists("name")) {

        name = blockSettings.readString("name")

    } else {

        name = game.askForString("What is your name?")

        blockSettings.writeString("name", name)

    }

    game.splash("Hello, " + name + "!")

}

```

  

## Step 10: Call the function

The function will not run unless we call it.

  

- Drag **call getAndDisplayPlayerName** into the workspace

- Place it inside **on start**

  

```blocks

function getAndDisplayPlayerName () {

    let name = ""

    name = ""

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

  

## Step 11: Test again

Test the game to make sure it still works.

  

- First run: the game should ask for your name

- Next runs: the game should remember your name automatically

  
  

  
```package

settings-blocks=github:microsoft/pxt-settings-blocks

```