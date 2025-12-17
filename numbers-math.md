# Numbers and Math

## Introduction @showdialog
Learn to use numbers, math operations, and check player answers in your game!

## Step 1: Initialize Score
From ``||info:Info||``, drag ``||info:set score to 0||`` into ``||loops:on start||``.
```blocks
info.setScore(0)
```

## Step 2: Create a Math Function
From ``||functions:Functions||`` (under Advanced), click "Make a Function". Name it exactly **calculateNumberOfHungryStudents** (or create your own name) and click Done.
```blocks
function calculateNumberOfHungryStudents () {
    
}
```

## Step 3: Call the Function
From ``||functions:Functions||``, drag ``||functions:call calculateNumberOfHungryStudents||`` into ``||loops:on start||`` after setting the score.
```blocks
info.setScore(0)
calculateNumberOfHungryStudents()
```

## Step 4: Show an Intro Message
From ``||game:Game||``, drag ``||game:show long text||`` into your function. Type exactly: **"1 in 9 people don't have enough to eat."** (or create your own fact).
```blocks
function calculateNumberOfHungryStudents () {
    game.showLongText("1 in 9 people don't have enough to eat.", DialogLayout.Bottom)
}
```

## Step 5: Explain the Math Problem
Add two more ``||game:show long text||`` blocks. Type these exactly (or create your own):
- **"How many hungry students would there be if 1 in 9 didn't have food?"**
- **"HINT: Divide the number by 9 and round down."**
```blocks
function calculateNumberOfHungryStudents () {
    game.showLongText("1 in 9 people don't have enough to eat.", DialogLayout.Bottom)
    game.showLongText("How many hungry students would there be if 1 in 9 didn't have food?", DialogLayout.Bottom)
    game.showLongText("HINT: Divide the number by 9 and round down.", DialogLayout.Bottom)
}
```

## Step 6: Ask for Number of Students
From ``||game:Game||``, drag ``||game:ask for number||``. Create a variable ``||variables:numStudents||`` to store the answer. Type the prompt exactly: **"How many students are there in this class?"** (or create your own). Set the default number to **2**.
```blocks
function calculateNumberOfHungryStudents () {
    game.showLongText("1 in 9 people don't have enough to eat.", DialogLayout.Bottom)
    game.showLongText("How many hungry students would there be if 1 in 9 didn't have food?", DialogLayout.Bottom)
    game.showLongText("HINT: Divide the number by 9 and round down.", DialogLayout.Bottom)
    let numStudents = game.askForNumber("How many students are there in this class?", 2)
}
```

## Step 7: Ask for Player's Answer
Add another ``||game:ask for number||`` and store it in a new variable ``||variables:playerAnswer||``. Type the prompt exactly: **"Now divide by 9 and round down."** (or create your own). Set the default to **1**.
```blocks
function calculateNumberOfHungryStudents () {
    game.showLongText("1 in 9 people don't have enough to eat.", DialogLayout.Bottom)
    game.showLongText("How many hungry students would there be if 1 in 9 didn't have food?", DialogLayout.Bottom)
    game.showLongText("HINT: Divide the number by 9 and round down.", DialogLayout.Bottom)
    let numStudents = game.askForNumber("How many students are there in this class?", 2)
    let playerAnswer = game.askForNumber("Now divide by 9 and round down.", 1)
}
```

## Step 8: Calculate the Correct Answer
From ``||math:Math||`` (under Advanced), use ``||math:Math.floor||`` to divide ``||variables:numStudents||`` by **9** and round down. Store it in a new variable ``||variables:numHungryStudents||``.
```blocks
function calculateNumberOfHungryStudents () {
    game.showLongText("1 in 9 people don't have enough to eat.", DialogLayout.Bottom)
    game.showLongText("How many hungry students would there be if 1 in 9 didn't have food?", DialogLayout.Bottom)
    game.showLongText("HINT: Divide the number by 9 and round down.", DialogLayout.Bottom)
    let numStudents = game.askForNumber("How many students are there in this class?", 2)
    let playerAnswer = game.askForNumber("Now divide by 9 and round down.", 1)
    let numHungryStudents = Math.floor(numStudents / 9)
}
```

## Step 9: Check if Answer is Correct
From ``||logic:Logic||``, add an ``||logic:if then else||`` block. Use a comparison (``||logic:=||``) to check if ``||variables:playerAnswer||`` equals ``||variables:numHungryStudents||``.
```blocks
function calculateNumberOfHungryStudents () {
    game.showLongText("1 in 9 people don't have enough to eat.", DialogLayout.Bottom)
    game.showLongText("How many hungry students would there be if 1 in 9 didn't have food?", DialogLayout.Bottom)
    game.showLongText("HINT: Divide the number by 9 and round down.", DialogLayout.Bottom)
    let numStudents = game.askForNumber("How many students are there in this class?", 2)
    let playerAnswer = game.askForNumber("Now divide by 9 and round down.", 1)
    let numHungryStudents = Math.floor(numStudents / 9)
    
    if (playerAnswer == numHungryStudents) {
        
    } else {
        
    }
}
```

## Step 10: Add Feedback for Correct Answer
In the ``||logic:if||`` section, add ``||info:change score by 1||`` from ``||info:Info||``. Then add ``||game:show long text||``. Use ``||text:join||`` from ``||text:Text||`` (under Advanced) to combine: **"Correct! There would be "** + ``||variables:numHungryStudents||`` + **" hungry students in this class!"** (or create your own message).
```blocks
function calculateNumberOfHungryStudents () {
    game.showLongText("1 in 9 people don't have enough to eat.", DialogLayout.Bottom)
    game.showLongText("How many hungry students would there be if 1 in 9 didn't have food?", DialogLayout.Bottom)
    game.showLongText("HINT: Divide the number by 9 and round down.", DialogLayout.Bottom)
    let numStudents = game.askForNumber("How many students are there in this class?", 2)
    let playerAnswer = game.askForNumber("Now divide by 9 and round down.", 1)
    let numHungryStudents = Math.floor(numStudents / 9)
    
    if (playerAnswer == numHungryStudents) {
        info.changeScoreBy(1)
        game.showLongText("Correct! There would be " + numHungryStudents + " hungry students in this class!", DialogLayout.Bottom)
    } else {
        
    }
}
```

## Step 11: Add Feedback for Incorrect Answer
In the ``||logic:else||`` section, add ``||game:show long text||``. Use ``||text:join||`` to combine: **"No, actually there would be "** + ``||variables:numHungryStudents||`` + **" hungry students in this class!"** (or create your own message).
```blocks
function calculateNumberOfHungryStudents () {
    game.showLongText("1 in 9 people don't have enough to eat.", DialogLayout.Bottom)
    game.showLongText("How many hungry students would there be if 1 in 9 didn't have food?", DialogLayout.Bottom)
    game.showLongText("HINT: Divide the number by 9 and round down.", DialogLayout.Bottom)
    let numStudents = game.askForNumber("How many students are there in this class?", 2)
    let playerAnswer = game.askForNumber("Now divide by 9 and round down.", 1)
    let numHungryStudents = Math.floor(numStudents / 9)
    
    if (playerAnswer == numHungryStudents) {
        info.changeScoreBy(1)
        game.showLongText("Correct! There would be " + numHungryStudents + " hungry students in this class!", DialogLayout.Bottom)
    } else {
        game.showLongText("No, actually there would be " + numHungryStudents + " hungry students in this class!", DialogLayout.Bottom)
    }
}
```

## Step 12: Add a Reflection Question
Add a final ``||game:show long text||`` block after the if/else. Type exactly: **"What can we do to make sure EVERYONE has enough to eat?"** (or create your own reflection question).
```blocks
function calculateNumberOfHungryStudents () {
    game.showLongText("1 in 9 people don't have enough to eat.", DialogLayout.Bottom)
    game.showLongText("How many hungry students would there be if 1 in 9 didn't have food?", DialogLayout.Bottom)
    game.showLongText("HINT: Divide the number by 9 and round down.", DialogLayout.Bottom)
    let numStudents = game.askForNumber("How many students are there in this class?", 2)
    let playerAnswer = game.askForNumber("Now divide by 9 and round down.", 1)
    let numHungryStudents = Math.floor(numStudents / 9)
    
    if (playerAnswer == numHungryStudents) {
        info.changeScoreBy(1)
        game.showLongText("Correct! There would be " + numHungryStudents + " hungry students in this class!", DialogLayout.Bottom)
    } else {
        game.showLongText("No, actually there would be " + numHungryStudents + " hungry students in this class!", DialogLayout.Bottom)
    }
    
    game.showLongText("What can we do to make sure EVERYONE has enough to eat?", DialogLayout.Bottom)
}
```

## Complete! @showdialog
Excellent work! You've created an interactive math activity that makes players think about real-world problems using division and rounding.

**Extension Ideas:**
- Add more math questions with different operations
- Calculate percentages instead of fractions
- Create a quiz with multiple calculation questions
- Customize all text to match your own topic