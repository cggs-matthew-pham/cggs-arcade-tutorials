# Story, Quiz and Score

## Introduction @showdialog
Tell a short story, ask quiz questions, and track the player's score based on their answers using the Story extension!

## Step 1: Add the Story Extension
We need the Story extension so we can show multiple-choice questions.

- Click **Extensions**
- Search for **story**
- Add the **arcade-storytelling** extension

## Step 2: Create a Story Function
From ``||functions:Functions||`` (under Advanced), click "Make a Function". Name it ``||functions:welcomeToOzHarvest||`` and click Done.
```blocks
function welcomeToOzHarvest () {
    
}
```

## Step 3: Call the Function
From ``||functions:Functions||``, drag ``||functions:call welcomeToOzHarvest||`` into ``||loops:on start||``.
```blocks
function welcomeToOzHarvest () {
    
}

welcomeToOzHarvest()
```

## Step 4: Add the First Story Text
From ``||game:Game||``, drag ``||game:show long text||`` into your function. Type exactly: **"Welcome to OzHarvest!"** (or create your own message). Set the layout to **Bottom**.
```blocks
function welcomeToOzHarvest () {
    game.showLongText("Welcome to OzHarvest!", DialogLayout.Bottom)
}
```

## Step 5: Add More Story Text
Duplicate the ``||game:show long text||`` block twice (right-click → Duplicate). Type these messages exactly (or create your own):
- **"I am here to tell you about FEAST."**
- **"Food Sustainability and Education Training."**
```blocks
function welcomeToOzHarvest () {
    game.showLongText("Welcome to OzHarvest!", DialogLayout.Bottom)
    game.showLongText("I am here to tell you about FEAST.", DialogLayout.Bottom)
    game.showLongText("Food Sustainability and Education Training.", DialogLayout.Bottom)
}
```

## Step 6: Add the Quiz Question
Add another ``||game:show long text||`` block. Type exactly: **"How many uneaten sandwiches do Australian students throw away each year?"** (or create your own question).
```blocks
function welcomeToOzHarvest () {
    game.showLongText("Welcome to OzHarvest!", DialogLayout.Bottom)
    game.showLongText("I am here to tell you about FEAST.", DialogLayout.Bottom)
    game.showLongText("Food Sustainability and Education Training.", DialogLayout.Bottom)
    game.showLongText("How many uneaten sandwiches do Australian students throw away each year?", DialogLayout.Bottom)
}
```

## Step 7: Add Answer Choices
From ``||story:Story||``, drag ``||story:show player choices||``. Type these four options exactly (or create your own):
- **"0.5 million"**
- **"1 million"**
- **"2 million"**
- **"5 million"**
```blocks
function welcomeToOzHarvest () {
    game.showLongText("Welcome to OzHarvest!", DialogLayout.Bottom)
    game.showLongText("I am here to tell you about FEAST.", DialogLayout.Bottom)
    game.showLongText("Food Sustainability and Education Training.", DialogLayout.Bottom)
    game.showLongText("How many uneaten sandwiches do Australian students throw away each year?", DialogLayout.Bottom)
    story.showPlayerChoices("0.5 million", "1 million", "2 million", "5 million")
}
```

## Step 8: Initialize Score
From ``||info:Info||``, drag ``||info:set score to 0||`` into ``||loops:on start||`` before calling your function.
```blocks
function welcomeToOzHarvest () {
    game.showLongText("Welcome to OzHarvest!", DialogLayout.Bottom)
    game.showLongText("I am here to tell you about FEAST.", DialogLayout.Bottom)
    game.showLongText("Food Sustainability and Education Training.", DialogLayout.Bottom)
    game.showLongText("How many uneaten sandwiches do Australian students throw away each year?", DialogLayout.Bottom)
    story.showPlayerChoices("0.5 million", "1 million", "2 million", "5 million")
}

info.setScore(0)
welcomeToOzHarvest()
```

## Step 9: Check the Player's Answer
From ``||logic:Logic||``, add an ``||logic:if then else||`` block after the choices. From ``||story:Story||``, drag ``||story:check last answer||`` into the condition. Type the correct answer exactly: **"2 million"** (must match your choice exactly, or use your own correct answer).
```blocks
function welcomeToOzHarvest () {
    game.showLongText("Welcome to OzHarvest!", DialogLayout.Bottom)
    game.showLongText("I am here to tell you about FEAST.", DialogLayout.Bottom)
    game.showLongText("Food Sustainability and Education Training.", DialogLayout.Bottom)
    game.showLongText("How many uneaten sandwiches do Australian students throw away each year?", DialogLayout.Bottom)
    story.showPlayerChoices("0.5 million", "1 million", "2 million", "5 million")
    if (story.checkLastAnswer("2 million")) {
        
    } else {
        
    }
}
```

## Step 10: Add Feedback for Correct Answer
In the ``||logic:if||`` section, add ``||info:change score by 1||`` from ``||info:Info||``. Then add ``||game:show long text||`` and type exactly: **"That's correct!"** (or create your own message).
```blocks
function welcomeToOzHarvest () {
    game.showLongText("Welcome to OzHarvest!", DialogLayout.Bottom)
    game.showLongText("I am here to tell you about FEAST.", DialogLayout.Bottom)
    game.showLongText("Food Sustainability and Education Training.", DialogLayout.Bottom)
    game.showLongText("How many uneaten sandwiches do Australian students throw away each year?", DialogLayout.Bottom)
    story.showPlayerChoices("0.5 million", "1 million", "2 million", "5 million")
    if (story.checkLastAnswer("2 million")) {
        info.changeScoreBy(1)
        game.showLongText("That's correct!", DialogLayout.Bottom)
    } else {
        
    }
}
```

## Step 11: Add Feedback for Incorrect Answer
In the ``||logic:else||`` section, add ``||game:show long text||`` and type exactly: **"No, it's actually 2 million!"** (or create your own message with the correct answer).
```blocks
function welcomeToOzHarvest () {
    game.showLongText("Welcome to OzHarvest!", DialogLayout.Bottom)
    game.showLongText("I am here to tell you about FEAST.", DialogLayout.Bottom)
    game.showLongText("Food Sustainability and Education Training.", DialogLayout.Bottom)
    game.showLongText("How many uneaten sandwiches do Australian students throw away each year?", DialogLayout.Bottom)
    story.showPlayerChoices("0.5 million", "1 million", "2 million", "5 million")
    if (story.checkLastAnswer("2 million")) {
        info.changeScoreBy(1)
        game.showLongText("That's correct!", DialogLayout.Bottom)
    } else {
        game.showLongText("No, it's actually 2 million!", DialogLayout.Bottom)
    }
}
```

## Step 12: Add Wrap-Up Facts
Add two more ``||game:show long text||`` blocks after the if/else. Type these messages exactly (or create your own):
- **"In Australia we waste 7.6 million tonnes of food every year."**
- **"This costs over $36.6 billion dollars!"**
```blocks
function welcomeToOzHarvest () {
    game.showLongText("Welcome to OzHarvest!", DialogLayout.Bottom)
    game.showLongText("I am here to tell you about FEAST.", DialogLayout.Bottom)
    game.showLongText("Food Sustainability and Education Training.", DialogLayout.Bottom)
    game.showLongText("How many uneaten sandwiches do Australian students throw away each year?", DialogLayout.Bottom)
    story.showPlayerChoices("0.5 million", "1 million", "2 million", "5 million")
    if (story.checkLastAnswer("2 million")) {
        info.changeScoreBy(1)
        game.showLongText("That's correct!", DialogLayout.Bottom)
    } else {
        game.showLongText("No, it's actually 2 million!", DialogLayout.Bottom)
    }
    game.showLongText("In Australia we waste 7.6 million tonnes of food every year.", DialogLayout.Bottom)
    game.showLongText("This costs over $36.6 billion dollars!", DialogLayout.Bottom)
}
```

## Complete! @showdialog
Great work! You've created an interactive story with quiz questions and score tracking. Try adding more questions to test players' knowledge!

**Extension Ideas:**
- Add multiple quiz questions
- Create different story branches based on answers
- Show a final score summary at the end
- Customize all text to match your own topic