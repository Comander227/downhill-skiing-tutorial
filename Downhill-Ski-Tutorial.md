
# Downhill Ski Game Jam

## Part 1: Creating our Player Character
### In the first part we are going to set up our environment as well as the character our player is going to control. 

## Setting your background
### Set up your background to white for your snow
- :tree: Add a ``||scene:set background color to ()||`` block from the ``||scene:Scene||`` category to your ``||loops:on start||`` container.
	
	```blocks
	// @highlight 
	scene.setBackgroundColor(1)
	```


## Creating your Skier Sprite
### Setting the Player Sprite

- :paper plane: Next we are going to add our ``||sprites:set mySprite to sprite [] of kind Player||`` from our ``||sprites:Sprites||`` category to our ``||loops:on start||`` container. 
	
```blocks
		scene.setBackgroundColor(1); 
		// @highlight
		let mySprite = sprites.create(img``,SpriteKind.Player)
```

## Giving our Skier an image
### Adding the Skier asset 
- :paint brush: Click on the grey box in the ``||sprites:set mySprite to [] of kind Player||`` block. 
- :mouse pointer: Next select the **My Assets** tab and click on the **Skier** asset. 
- :mouse pointer: Then click **done**. 

```blocks
	scene.setBackgroundColor(1)

	let mySprite = sprites.create(assets.image`Skier`,SpriteKind.Player)
```

## Moving our Skier
### Assigning controllers to our sprite 
- :game: Now we are going to add our ``||controller:move mySprite with buttons||`` block from our ``||controller:Controller||`` category to our ``||loops:on start||`` container. 

```blocks
	scene.setBackgroundColor(1)
let mySprite = sprites.create(assets.image`Skier`, SpriteKind.Player)
// @highlight
controller.moveSprite(mySprite)
```
## Don't lose the Skier
### Keeping our Skier on screen 
- :paper plane: Add a ``||sprites:set mySprite stay in screen||`` block from the ``||sprites:Sprites||`` category to our ``||loops:on start||`` container. 

```blocks
scene.setBackgroundColor(1)
let mySprite = sprites.create(assets.image`Skier`, SpriteKind.Player)
controller.moveSprite(mySprite)
// @highlight
mySprite.setStayInScreen(true)
```

## Where should our skier start?
### Setting the Skier's position
- :paper plane: Add a ``||sprites: set mySprite position to x() y()||`` from the ``||sprites:Sprites||`` category to our ``||loops:on start||`` container.
- :mouse pointer: We want our Skier to start at the top of the screen so change the **x value** from **0** to **80** and the **y value** from **0** to **11** 

```blocks
scene.setBackgroundColor(1)
let mySprite = sprites.create(assets.image`Skier`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
// @highlight
mySprite.setPosition(80, 11)
```

## Part 2: Creating Obstacles
### A good game should contain some obstacles that our player needs to overcome in order to score points or win the game. 

## Creating our Rock Obstacle
### Setting up the container
- :circle: Grab an ``||game:on game update every 500 ms||`` container from the ``||game:Game||`` category. 

```blocks
// @highlight
game.onUpdateInterval(500, function () {
	
})
```

## Establishing our Rock
### Setting the Rock Sprite
- :paper plane: Add a ``||sprites:set mySprite to sprite [] of kind Player||`` block from the ``||sprites:Sprite||`` category to the ``||game:update game every 500 ms||`` container. 
- :paint brush: Click on the grey box to open the sprite editor. Open the **My Assets** tab. Select the **rock** image. 
- :mouse pointer: Change the sprite kind from **Player** and add a new kind called **Rock**

```blocks
	namespace SpriteKind {
    export const Rock = SpriteKind.create()
}

let Rocks: Sprite = null
	game.onUpdateInterval(500, function () {
    // @highlight
    Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
})
```
## Positioning the Rocks

- :paper plane: Grab a ``||sprites:set mySprite position to x() y()||`` from the ``||sprites:Sprites||`` category and place it in the ``||game:on game update every 500ms||`` container. 
- :mouse pointer: Change **mySprite** to **Rocks**

```blocks
	namespace SpriteKind {
    export const Rock = SpriteKind.create()
}
let Rocks: Sprite = null
	game.onUpdateInterval(500, function () {
    Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
    // @highlight
    Rocks.setPosition(0, 0)
})
```

## Starting the Rock Off Screen
- :tree: Add a ``||scene: screen height||`` circle from the ``||scene:Scene||`` category to the **y** value of ``||sprites: set Rocks position x() y()||``.


```blocks
	namespace SpriteKind {
    export const Rock = SpriteKind.create()
}
let Rocks: Sprite = null
	game.onUpdateInterval(500, function () {
    Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
    // @highlight
    Rocks.setPosition(0, scene.screenHeight())
})
```

## Randomizing the Rock's X Position

- :calculator: Add a ``||math: pick random () to ()||`` from the ``||math:Math||`` category to the **x** value of ``||sprites: set Rock position x() y||`` ``||scene:screen height||``.
- :tree: Add a ``||scene:screen width||`` circle from the ``||scene:Scene||`` category to the **max** value of the ``||math:pick random (0) to (0)||``.

```blocks
	namespace SpriteKind {
    export const Rock = SpriteKind.create()
}
	game.onUpdateInterval(500, function () {
   let Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
    // @highlight
    Rocks.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
})
```

## Setting the Rock's Velocity

- :paper plane: Grab a ``||sprites:set mySprite vx() vy()||`` block from the ``||sprites:Sprites||`` category and add it to the ``||game:on game update every 500ms||`` container. 
- :mouse pointer: Change ``||variables:mySprite||`` to ``||variables:Rocks||``.
- :mouse pointer: Set the **vx** value to **0**
- :mouse pointer: Set **vy** value to **-50**  

```blocks 
	namespace SpriteKind {
    export const Rock = SpriteKind.create()
}
	game.onUpdateInterval(500, function () {
    let Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
    Rocks.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
    // @highlight
    Rocks.setVelocity(0, -50)
})
```
## Destroying our Rocks when off screen

- :paper plane: Grab a ``||sprites:set mySprite auto destroy||`` block from the ``||sprites:Sprites||`` category and place it in the ``||game:on game update every 500ms||`` container. 
- :mouse pointer: Change ``||variables:mySprite||`` to ``||varaiables:Rocks||``.
- :mouse pointer: Set the value to **true**

```blocks
	namespace SpriteKind {
    export const Rock = SpriteKind.create()
}
game.onUpdateInterval(500, function () {
    let Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
    Rocks.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
    Rocks.setVelocity(0, -50)
   // @highlight
    Rocks.setFlag(SpriteFlag.AutoDestroy, true)
})
```

## Part 3: Let's Speed Things Up
### The game will get boring if nothing changes as the player progresses. Let's make the skier move faster the longer they are actively playing. 

## Creating a Skier Speed Variable
### Let's adjust the speed of this using a variable that we can manipulate. 

- :bars: Click on the ``||variables:variables||`` category. 
- :mouse pointer: Click on the button that says ``||variables:Make A Variable||``.
- :mouse pointer: Name the new variable ``||variables:SkierSpeed||``.
- :bars: Add a ``||variables:set SkierSpeed to 0||`` block to our ``||loops:on start||`` container. 
- :mouse pointer: Set the value to **-20**.

```blocks
	scene.setBackgroundColor(1)
let mySprite = sprites.create(assets.image`Skier`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
mySprite.setPosition(80, 11)
// @highlight
let SkierSpeed = -20

```

## Creating A Spawn Timer for the Rocks
### We are going to create a second variable and use it as a spawn timer for our obstacles. 

- :bars: Click on the ``||variables:variables||`` category. 
- :mouse pointer: Click on the button that says ``||variables:Make A Variable||``.
- :mouse pointer: Name the new variable ``||variables:RockSpawnTimer||``.
- :bars: Add a ``||variables:set RockSpawnTimer to 0||`` block to our ``||loops:on start||`` container. 
- :mouse pointer: Set the value to **2000**.

```blocks
	scene.setBackgroundColor(1)
let mySprite = sprites.create(assets.image`Skier`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
mySprite.setPosition(80, 11)
let SkierSpeed = -20
// @highlight
let RockSpawnTime = 2000
```

## Adjusting our Rocks Spawn Code
### To make this function work we need to change the way the spawn code for the rock works.

- :redo: Replace the ``||game:on game update every 500ms seconds||`` with a ``||loops: forever loop||`` from the ``||loops:Loops||`` section.

```blocks
	namespace SpriteKind {
    export const Rock = SpriteKind.create()
}

	// @highlight
	forever(function () {
    let Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
    Rocks.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
    Rocks.setVelocity(0, -50)
    Rocks.setFlag(SpriteFlag.AutoDestroy, true)
})
```

## Using the RockSpawn Time Variable

- :redo: Add a ``||loops: pause||`` block from the``||loops:Loops||``category to the bottom of the ``||loops: forever loop||``.
- :bars: Add a ``||variables:RockSpawnTime||`` value circle from the ``||variables:Variables||`` category to the value space in the ``||loops:pause||`` block.

```blocks 
	namespace SpriteKind {
    export const Rock = SpriteKind.create()
}

	forever(function () {
    let Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
    Rocks.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
    Rocks.setVelocity(0, -50)
    Rocks.setFlag(SpriteFlag.AutoDestroy, true)
    // @highlight
    pause(RockSpawnTime)
})
```
## Adding the Skier's Speed to the Rock 
- :bars: Add a ``||variables:SkierSpeed||`` value circle from the ``||variables:Variables||`` category to the **vy** value of our Rock. 

```blocks
	namespace SpriteKind {
    export const Rock = SpriteKind.create()
}
	forever(function () {
    let Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
    Rocks.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
    // @highlight
    Rocks.setVelocity(0, SkierSpeed)
    Rocks.setFlag(SpriteFlag.AutoDestroy, true)
    pause(RockSpawnTime)
})
```

## Adjusting The Speed as the Game is Played
### The skier's speed should increase as you play the game. Let's set up a container to take care of that process. 

- :circle: Add a new ``||game: on game update every 500ms||`` container from the ``||game:Game||`` category. 
- :mouse pointer: Change the value to **3000**.
 
```blocks
	// @highlight
	game.onUpdateInterval(3000, function () {
	
})
```

## Modifying the Skier Speed Value
- :bars: Add a ``||variables: change SkierSpeed by 0||`` block from the ``||variables:Variables||`` category to the ``||game:on game update every 3000ms||`` container. 
- :mouse pointer: set the value to **-5**.

```blocks
	game.onUpdateInterval(3000, function () {
   // @highlight
   SkierSpeed += -5
})
```

## Clamping the Skier's Speed value
- :bars: Add a ``||variables:set SkierSpeed to 0||`` block from the ``||variables:Variables||`` category under the ``||variables:change SkierSpeed by -5||`` 
- :calculator: Add a ``||math:max of 0 and 0||`` circle from the ``||math:Math||`` category to the ``||variables:set SkierSpeed to 0||`` value space. 
- :bars: Add a ``||variables:SkierSpeed||`` circle from the ``||variables:Variables||`` category to the first value space in the ``||math:max of 0 and 0||``.
- :mouse pointer: Change the second value in the ``||math:max of||`` ``||variables:SkierSpeed||`` ``||math: and 0||`` to **-100**.

```blocks
	game.onUpdateInterval(3000, function () {
    SkierSpeed += -5
    // @highlight
    SkierSpeed = Math.max(SkierSpeed, -100)
})

```

## Modifying the Rock's Spawn Timer
### The same concept can be used to adjust the RockSpawnTime speed. 

- :bars: Add another ``||variables:change RockSpawnTime||`` block from the ``||variables:Variables||`` category and place it under the ``||variables:set SkierSpeed||`` block.
- :mouse pointer: set the value to **-200** 


```blocks
	game.onUpdateInterval(3000, function () {
    SkierSpeed += -5
    SkierSpeed = Math.max(SkierSpeed, -100)
    // @highlight
    RockSpawnTime += -200
})
```
## Clamping the Rock Spawn Timer
- :bars: Grab a ``||variables:set RockSpawnTime to 0||`` block from the ``||variables:Variables||`` category and place it under the ``||variables:change RockSpawnTime by -200||``. 
- :calculator: Add a ``||math:max value of 0 and 0||`` circle from the ``||math:Math||`` category to the value space in the ``||variables:set RockSpawnTime||`` block. 
- :bars: Add a ``||variables:RockSpawnTime||`` circle from the ``||variables:Variables||`` category to the first value in the ``||math:max value of 0 and 0||`` circle. 
- :mouse pointer: Change the second value from **0** to **500**.	

```blocks
	game.onUpdateInterval(3000, function () {
    SkierSpeed += -5
    SkierSpeed = Math.max(SkierSpeed, -100)
    RockSpawnTime += -200
    // @highlight
    RockSpawnTime = Math.max(RockSpawnTime, 500)
})
```

## Part 4: Making An Impact
### In this part we are going to add collision code to have our sprites and obstacles interact. 


## Setting up the Collision Code
### MakeCode Arcade uses overlap containers to determine when object collide. 

- :paper plane: Grab an ``||sprites: on sprite of kind Player overlaps otherSprite of kind Player||`` container from the ``||sprites:Sprites||`` category and place it into the workspace.
- :mouse pointer: Change the ``||variables:otherSprite||`` kind from **Player** to **Rock**.

```blocks
	namespace SpriteKind {
    export const Rock = SpriteKind.create()
}
// @highlight
sprites.onOverlap(SpriteKind.Player, SpriteKind.Rock, function (sprite, otherSprite) {
	
})
```
## When Our Skier Crashes into a Rock
### If our skier crashes into a rock, we want them to lose a life and destroy the rock. Let do that in steps. 

### First let's destroy the rock if it runs into our player.

- :paper plane: Grab a ``||sprites:destroy mySprite||``block from the ``||sprites:Sprites||`` category and place it in the ``||sprites: on sprite of kind Player overlaps otherSprite of kind Rock||``. 
- :mouse pointer: Take the local variable of ``||variables:otherSprite||`` and replace the ``||variables:mySprite||`` circle in the ``||sprites:destroy||`` block. 
- :mouse pointer: Click on the **+** to add an effect to your ``||sprites:destroy||`` block.   
 
	![Grab the sprite value from the title bar of the outer container](/static/skillmap/assets/sprite-from-container.gif "This is how your block knows which sprite to use")

```blocks 
namespace SpriteKind {
    export const Rock = SpriteKind.create()
}
	sprites.onOverlap(SpriteKind.Player, SpriteKind.Rock, function (sprite, otherSprite) {
    // @highlight
    otherSprite.destroy(effects.blizzard, 100)
})
```
## Skier Should Lose a Life
### If the skier hits the rock they should lose a life.

- :id card: Grab a ``||info:change life by -1||`` block from the ``||info:Info||`` category and place it under the ``||sprites:destroy otherSprite||`` block. 

```blocks
namespace SpriteKind {
    export const Rock = SpriteKind.create()
}
	sprites.onOverlap(SpriteKind.Player, SpriteKind.Rock, function (sprite, otherSprite) {
    otherSprite.destroy(effects.blizzard, 100)
    // @highlight
    info.changeLifeBy(-1)
})
```
## What Happens When We Run Out of Lives?
### Since we make the player lose a life we need to tell the game what should happen when we run out of them. 

- :id card: Add an ``||info:on life zero||`` container from the ``||info:Info||`` category to the workspace.
- :circle: Add a ``||game:game over||`` block from the ``||game:Game||`` to the ``||info:on life zero||`` container. 

```blocks
	info.onLifeZero(function () {
    // @highlight
    game.over(false)
})
```

## Part 5: Scoring Points 
### In this part we are going to set up some code that will allow our player to score points and progress further in the game. 

## Giving Our Player Some Points
### Let's have our player score some points for every Rock that they avoid. 
	
- :paper plane: Grab the ``||sprites:on destroy sprite of kind Player||`` container from the ``||sprites:Sprites||`` category and place it in the workspace. 
- :mouse pointer: Change the kind from **Player** to **Rocks**.
- :id card: Add a ``||info:change score by 1||`` block from the ``||info:Info||`` category to the ``||sprites:on destroy sprite of kind Rock||`` container. 
	
```blocks 
namespace SpriteKind {
    export const Rock = SpriteKind.create()
}
	// @highlight
	sprites.onDestroyed(SpriteKind.Rock, function (sprite) {
    info.changeScoreBy(1)
})
```
## Adding Additional Incentives
### Let's create an additional objective for our player to collect as they play the game. 


- :bars: Create a new ``||variables:variable||`` by clicking the ``||variables:Make A Variable||`` button in the ``||variables:Variables||`` category.
- :mouse pointer: Name the variable ``||variables:PurpleGateTimer||``. 
- :bars: Grab a ``||variables:set PurpleGateTimer to 0||`` block from the ``||variables:Variables||`` category and add it to the ``||loops:on start||`` container. 
- :mouse pointer: Set the value to **5000**


```blocks
scene.setBackgroundColor(1)
let mySprite = sprites.create(assets.image`Skier`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
mySprite.setPosition(80, 11)
let SkierSpeed = -20
let RockSpawnTime = 2000
// @highlight
let PurpleGateTimer = 5000
```

## Spawning the Purple Gate
### First we need to set up a new container. 

- :redo: Grab a ``||loops:forever loop||`` container from the ``||loops:Loops||`` category. 

```blocks
	// @highlight
	forever(function () {
	
})
```

## Adding the Purple Gate Sprite
### Now to assign our Purple Gate Sprite.


- :paper plane: Add a ``||sprites:set mySprite2 to sprite [] of kind Player||`` block from the ``||sprites:Sprites||`` category and add it to the ``||loops:forever||`` container. 
- :bars: Rename the sprite by clicking on the name and selecting ``||variables:Rename variable||``
- :mouse pointer: Change ``||variables:mySprite2||`` to ``||variables:PurpleGate||``
- :mouse pointer: Change the kind from **Player** and add a new option called **PGate**. 

```blocks	
	namespace SpriteKind {
    export const PGate = SpriteKind.create()
}
let PurpleGate: Sprite = null
	forever(function () {
    // @highlight
    PurpleGate = sprites.create(img``, SpriteKind.PGate)
})
```
## Assigning the Purple Gate Asset

- :mouse pointer: Click on the grey box to open up the editor. Open the **My Assets** tab. 
- :mouse pointer: Click on the **Purple Gate** asset. 
- :mouse pointer: Click **done**.

```blocks	
	namespace SpriteKind {
    export const PGate = SpriteKind.create()
}
let PurpleGate: Sprite = null
	    forever (function (){
	    // @highlight
	    PurpleGate = sprites.create(assets.image`Purple Gate`, SpriteKind.PGate)
})
```

## Let's not reinvent the wheel
### We are going to use code that we already wrote to make this process a bit easier. 

- :mouse pointer: Duplicate the ``||sprites:set Rocks position||`` block from the Rock Spawn ``||loops:forever loop||``. This can be done by **right clicking** on the block you would like to copy and then selecting **Duplicate** from the menu. 
- :mouse pointer: Change ``||variables:Rocks||`` to ``||variables:PurpleGate||``.

```blocks
	namespace SpriteKind {
    export const PGate = SpriteKind.create()
}
let PurpleGate: Sprite = null

	forever(function () {
       PurpleGate = sprites.create(assets.image`Purple Gate`, SpriteKind.PGate)
    // @highlight
    PurpleGate.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
})
```


## Let's continue to not reinvent the wheel

- :mouse pointer: Duplicate the ``||sprites:set Rocks vx 0 and vy SkierSpeed||`` block from the Rock's ``||loops:forever loop||`` and add it to your new ``||loops:forever loop||``.

- :mouse pointer: Change ``||variables:Rocks||`` to ``||variables:PurpleGate||``. 

```blocks
	namespace SpriteKind {
    export const PGate = SpriteKind.create()
}
let PurpleGate: Sprite = null

	forever(function () {
    PurpleGate = sprites.create(assets.image`Purple Gate`, SpriteKind.PGate)
    PurpleGate.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
    // @highlight
    PurpleGate.setVelocity(0, SkierSpeed)
})
```

## Adding a timer to your Purple Gate Code
- :redo:Add a ``||loops:pause 100 ms||`` block from the ``||loops:Loops||`` category to the top of the ``||loops:forever loop||`` you just added.
- :bars: Grab the ``||variables:PurpleGateTimer||`` variable circle from the ``||variables:Variables||`` category and add it to the ``||loops:pause 100ms||`` block's value space. 

```blocks
	namespace SpriteKind {
    export const PGate = SpriteKind.create()
}
let PurpleGate: Sprite = null

forever(function () {
    PurpleGate = sprites.create(assets.image`Purple Gate`, SpriteKind.PGate)
    PurpleGate.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
    PurpleGate.setVelocity(0, SkierSpeed)
    // @highlight
    pause(PurpleGateTimer)
})
```
## What happens when our Skier hits a Purple Gate
### Let's make our purple gate do something
 
- :paper plane: Add an ``||sprites:on sprite of kind Player overlaps otherSprite of kind Player||`` container from the ``||sprites:Sprites||`` category onto the workspace.
- :mouse pointer: Change the ``||variables:otherSprite||`` kind from **Player** to **PGate**.

```blocks
	namespace SpriteKind {
    export const PGate = SpriteKind.create()
}
// @highlight
	sprites.onOverlap(SpriteKind.Player, SpriteKind.PGate, function (sprite, otherSprite) {
	
})
```
## Removing the Gate
### To properly set up our overlap code we need to remove the gate once our skier collides with it. 

- :paper plane: Add a ``||sprites:destroy mySprite||`` block from the ``||sprites:Sprites||`` category. 

- :mouse pointer: Grab the local ``||variables:otherSprite||`` circle from the ``||sprites:overlap||`` container and use it to replace ``||variables:mySprite||`` in the ``||sprites:destroy mySprite||`` block.  

![Grab the sprite value from the title bar of the outer container](/static/skillmap/assets/sprite-from-container.gif "This is how your block knows which sprite to use")

- :mouse pointer: Feel free to press the **+** button to add an effect for your gate. 	
	
```blocks
	namespace SpriteKind {
    export const PGate = SpriteKind.create()
}
	sprites.onOverlap(SpriteKind.Player, SpriteKind.PGate, function (sprite, otherSprite) {
    // @highlight
    otherSprite.destroy(effects.coolRadial, 200)
})
```
## Increasing the Skier's Speed 
### Let's use our Purple Gate to increase our Skier's speed

- :bars: Add a ``||variables:change SkierSpeed by 1||`` block from the ``||variables:Variables||`` category to the ``||sprites:PurpleGate overlap||`` container.
- :mouse pointer: Change the value to **-5**. 

```blocks
	namespace SpriteKind {
    export const PGate = SpriteKind.create()
}

	sprites.onOverlap(SpriteKind.Player, SpriteKind.PGate, function (sprite, otherSprite) {
    otherSprite.destroy(effects.coolRadial, 200)
    // @highlight
    SkierSpeed += -5
})
```
## Scoring Additional Points for our Skier
### When our Skier runs into the Purple Gate they should score extra points.

- :id card: Add a ``||info:change score by 1||`` block from the ``||info:Info||`` category to the ``||sprites:overlap||`` code.
- :mouse pointer: Change the value from **1** to **3**.

```blocks
	namespace SpriteKind {
    export const PGate = SpriteKind.create()
}

	sprites.onOverlap(SpriteKind.Player, SpriteKind.PGate, function (sprite, otherSprite) {
    otherSprite.destroy(effects.coolRadial, 200)
    SkierSpeed += -5
    // @highlight
    info.changeScoreBy(3)
})
```

## Part 6: Going the Distance
### Let's create a new variable to determine the total distance our player has gone. 

## Adding Distance values
### Set your variable in the on start container
- :bars: Create a new ``||variables:variable||``by clicking on the ``||variables:Make A Variable||`` button in the ``||variables:Variables||`` category. 
- :bars: Name the variable ``||variables:distance||``.
- :bars: Add a ``||variables:Set distance to 0||`` block to your ``||loops:on start||`` container. 	
	
```blocks
	let distance = 0
	scene.setBackgroundColor(1)
	let mySprite = sprites.create(assets.image`Skier`, SpriteKind.Player)
	controller.moveSprite(mySprite)
	mySprite.setStayInScreen(true)
	mySprite.setPosition(80, 11)
	let SkierSpeed = -20
	let RockSpawnTime = 2000
	let PurpleGateTimer = 5000
	// @highlight
	distance = 0
```
	
	
## Adjusting distance

### To adjust our distance variable we need to set up a forever loop to do so. 

- :redo: Add a ``||loops:forever loop||`` container from the ``||loops:Loops||`` category into the workspace.
- :redo: Add a ``||loops: pause||``block from the ``||loops:Loops||`` category to the ``||loops:forever||`` container. 

 ```blocks
	 // @highlight
	 forever(function () {
    pause(100)
})
```

## Going the Distance based off the Skier's Speed

### Now we will add blocks to increase our distance over time based off the Skier's Speed. 
	
- :bars: Grab a ``||variables:change distance by 1||`` block from the ``||variables:Variables||`` category and place it under the ``||loops:pause||`` block.
- :calculator: Add a ``||math:multiplication||`` circle (``||math: 0 * 0||``) from the ``||math:Math||`` category and use it to replace the value in the ``||variables: change distance by 1||`` block.
- :bars: Add a ``||variables:SkierSpeed||`` circle from the ``||variables:Variables||`` category and place it in the ``||math:multiplication||`` circle. 
- :mouse pointer: Change the second value from **0** to **-0.05**


```blocks
	forever(function () {
    pause(100)
    // @highlight
    distance += SkierSpeed * -0.05
})
```

## Showing the distance value

- :circle: Add a ``||game:show long text||`` block from the ``||game:Game||`` category to your ``||info:on life zero||`` container. 
- :mouse pointer: Be sure to add it **above** the game over block. 
- :mouse pointer: Set the text to appear in the **center** of the screen.
```blocks
	info.onLifeZero(function () {
    // @highlight
    game.showLongText("", DialogLayout.Center)
    game.over(false)
})
```
	
## Showing A Long Message

- :chevron down: Click on the **Advanced** category to gain access to the ``||text:Text||`` category. 
- :text width: Add a ``||text:join "Hello" "World" ||`` circle from the ``||text:Text||`` category.
- :mouse pointer: Add a third value space by clicking the **+** button on the ``||text:join "Hello" "World"||``circle. 
```blocks
	info.onLifeZero(function () {
    // @highlight
    game.showLongText("Hello" + "World" + "", DialogLayout.Center)
    game.over(false)
})
```

## Adding the Distance to our Message

- :calculator: Place a ``||math:round||`` circle from the ``||math:Math||`` category into the ``||text:middle text space||``.
- :bars: Add a ``||variables:distance||`` circle from the ``||variables:Variables||`` category. 
- :text width: Replace the other two text spaces so it reads ``||text:"you went"||`` ``||math:round||`` ``||variables:distance||`` ``||text:"feet"||``.

```blocks
	info.onLifeZero(function () {
    // @highlight
    game.showLongText("\"you went\"" + Math.round(distance) + "\"feet!\"", DialogLayout.Center)
    game.over(false)
})
```
## Giving the Player more points based off distance

### Let's give the player more points the longer they are able to stay alive. 

- :id card: Add a ``||info:change score by 1||`` block from the ``||info:Info||`` category.
- :calculator: Add a ``||math:round 0||`` circle from the ``||math:Math||`` category to the value space of the ``||info:change score by 1||`` block 
- :bars: Add a ``||variables:distance||`` circle from the ``||variables:Variables||`` category and place in the value space of the ``||math:round 0||`` circle.  


```blocks
	info.onLifeZero(function () {
    game.showLongText("\"you went\"" + Math.round(distance) + "\"feet!\"", DialogLayout.Center)
// @highlight
info.changeScoreBy(Math.round(distance))
    game.over(false)
})
```

## Part 7: Winning the Game
### Every good video game needs a way for the player to win the game. Let's code our win condition. 


## Creating a Win Condition
### Let's give our player a way to win the game. 
- :redo: Add a ``||forever loop||`` container from the ``||loop:Loops||`` category. 
- :random: Add an ``||logic: if true then||`` container from the ``||logic:Logic||`` category and add it too the ``||loops:forever||``container.

```blocks
	// @highlight
	forever(function () {
    if (true) {
    	
    }
})
```

## Deciding when to spawn the Win Condition
### We want the player to have to go a certain distance in order to have the chance to win the game.

- :random: Add a ``||logic:comparison||`` diamond (``||logic: 0 < 0||``) from the ``||logic:Logic||`` category to the **true** value of the ``||logic:if true then||`` container. 
- :mouse pointer: change **<** to **≥**. 
- :bars: Add a ``||variables:distance||`` circle from the ``||variables:Variables||`` category to the first value in our ``||logic:comparison||`` diamond. 
- :mouse pointer: change the second value of **0** to **500**.

```blocks
	forever(function () {
    // @highlight
    if (distance >= 500) {
    	
    }
})
```

## Adding the the checkered gate 

- :paper plane: Add a ``||sprites:set mySprite2 to sprite [] of kind Player||`` block from the ``||sprites:Sprites||`` category and add it to our ``||logic:if distance ≥ 500 then||`` container.
- :mouse pointer: Rename **mySprite2** to **CheckGate** by clicking on the name and choosing the ``||variables:Rename Variable||`` option.
- :mouse pointer: Change the kind from **Player** to a new kind called **CGate**.

 
```blocks
	namespace SpriteKind {
    export const Rock = SpriteKind.create()
    export const PGate = SpriteKind.create()
    export const CGate = SpriteKind.create()
}
	
	forever(function () {
    if (distance >= 500) {
        // @highlight
        CheckGate = sprites.create(img` `, SpriteKind.CGate)
    }
})
```

## Assigning the Checked Gate its asset 

- :mouse pointer: Click on the grey box and select the **checkered gate** from the my Assets section.
	
```blocks
namespace SpriteKind {
    export const Rock = SpriteKind.create()
    export const PGate = SpriteKind.create()
    export const CGate = SpriteKind.create()
}
	forever(function () {
    if (distance >= 500) {
        // @highlight
        CheckGate = sprites.create(assets.image`CheckGate`, SpriteKind.CGate)
    }
})
```

##Setting up a Checkered Gate Timer
### We need to create a new variable that will be used as a timer to spawn the Checkered Gate. 

- :bars: Create a new ``||variables: variable||`` by clicking the ``||variables: Make A Variable||`` button in the ``||variables:Variables||`` category. 
- :mouse pointer: name the new variable ``||variables:CGateTimer||``
- :bars: Add a ``||variables:set CGateTimer to 0||`` block to our ``||loops:on start||`` container.
- :mouse pointer: change the value from **0** to **7000**. 


```blocks
scene.setBackgroundColor(1)
let mySprite = sprites.create(assets.image`Skier`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
mySprite.setPosition(80, 11)
let distance = 0
let SkierSpeed = -20
let RockSpawnTime = 2000
let PurpleGateTimer = 5000
// @highlight
let CGateTimer = 7000
```

## Positioning the Checkered Gate

### We want the checkered gate to function in a similar way to the Purple Gate. To set this up we are going to copy blocks from the Purple Gate Spawn Code. 

- :mouse pointer: Copy the ``||sprites: set PurpleGate position to x||`` ``||math:pick random 0 to||`` ``||scene:screen width||`` ``||sprites: y||`` ``||scene: screen height||`` by **right clicking** on the block and selecting **duplicate**. 
- :mouse pointer: Add the duplicated block to the Checkered Gate ``||loops:forever loop||`` container. 
- :mouse pointer: Change ``||variables:PurpleGate||`` to ``||variables:CheckGate||``

 
```blocks
	namespace SpriteKind {
    export const Rock = SpriteKind.create()
    export const PGate = SpriteKind.create()
    export const CGate = SpriteKind.create()
}
	forever(function () {
    if (distance >= 500) {
        let CheckGate = sprites.create(assets.image`CheckGate`, SpriteKind.CGate)
        // @highlight
        CheckGate.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
    }
})
```

## Moving the Checkered Gate


### We want the checkered gate to move in a similar way to the Purple Gate. To set this up we are going to copy blocks from the Purple Gate Spawn Code. 

- :mouse pointer: Copy the ``||sprites:set PurpleGate vx 0 and vy SkierSpeed||``block by **right clicking** on the block and selecting the **duplicate** option.
- :mouse pointer: Add the copied block to the **CheckGate** ``||loops:forever loop||`` container. 
- :mouse pointer: change ``||variables:PurpleGate||`` to ``||variables:CheckGate||``.

```blocks
	namespace SpriteKind {
    export const Rock = SpriteKind.create()
    export const PGate = SpriteKind.create()
    export const CGate = SpriteKind.create()
}
	forever(function () {
    if (distance >= 500) {
        let CheckGate = sprites.create(assets.image`CheckGate`, SpriteKind.CGate)
        CheckGate.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
        // @highlight
        CheckGate.setVelocity(0, SkierSpeed)
    }
})
```

## Implementing our CheckGate Timer

- :redo: Add a ``||loops:pause 100ms||`` block from the ``||loops:Loops||`` category to the end of your Checkered Gate  ``||loops:forever loop||`` container so it is **outside** the ``||logic:if then||`` container.
- :bars: Add the ``||variables:CGateTimer||`` circle from the ``||variables:Variables||`` category and add it to the value space in the ``||loops:pause||`` block. 

```blocks
	namespace SpriteKind {
    export const Rock = SpriteKind.create()
    export const PGate = SpriteKind.create()
    export const CGate = SpriteKind.create()
}
	forever(function () {
    if (distance >= 500) {
        let CheckGate = sprites.create(assets.image`CheckGate`, SpriteKind.CGate)
        CheckGate.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
        CheckGate.setVelocity(0, SkierSpeed)
    }
    // @highlight
    pause(CGateTimer)
})
```

## Crossing the finish line
### We need to add code to make something happen once the player touches the Checkered Gate. Let's start by adding an overlap container.  
- :paper plane: Add an ``||sprites: on mySprite of kind Player overlaps otherSprite of kind Player||`` container to the workspace.
- :mouse pointer: Change the kind of ``||variables:otherSprite||`` from **Player** to **CGate**.
 
```blocks
	namespace SpriteKind {
    export const Rock = SpriteKind.create()
    export const PGate = SpriteKind.create()
    export const CGate = SpriteKind.create()
}
	// @highlight
	sprites.onOverlap(SpriteKind.Player, SpriteKind.CGate, function (sprite, otherSprite) {
	
})
```

## Adding the Score
### We want the player's score to include their distance if they win. To do this we will use the same text blocks that are in our game over code. 

- :mouse pointer: Copy the ``||game: long text||`` block from the ``||info:on life zero||`` container by **right clicking** on the block and selecting **duplicate** from the menu.
- :mouse pointer: Add the duplicated block to the ``||sprites:on overlap||`` container we just added.
- :mouse pointer: Copy the ``||info: change score by round distance||`` block from the ``||info: on life zero||`` container by **right clicking** on the block and selecting **duplicate** from the menu.
- :mouse pointer: Add the duplicated block to the ``||sprites:on overlap||`` container we just added. 

```blocks
	namespace SpriteKind {
    export const Rock = SpriteKind.create()
    export const PGate = SpriteKind.create()
    export const CGate = SpriteKind.create()
}
	sprites.onOverlap(SpriteKind.Player, SpriteKind.CGate, function (sprite, otherSprite) {
    // @highlight
    game.showLongText("\"you went\"" + Math.round(distance) + "\"feet!\"", DialogLayout.Center)
    info.changeScoreBy(Math.round(distance))
})
```

## Winning the game

- :circle: Add a ``||game:game over||`` block from the ``||game:Game||`` category to the ``||sprites: on overlap||`` container we just added.
- :mouse pointer: Change the value from **lose** to **win**.
- :mouse pointer: Feel free to add an effect by clicking on the **+** button. 

```blocks
	namespace SpriteKind {
    export const Rock = SpriteKind.create()
    export const PGate = SpriteKind.create()
    export const CGate = SpriteKind.create()
}
	sprites.onOverlap(SpriteKind.Player, SpriteKind.CGate, function (sprite, otherSprite) {
    game.showLongText("\"you went\"" + Math.round(distance) + "\"feet!\"", DialogLayout.Center)
    info.changeScoreBy(Math.round(distance))
    // @highlight
    game.over(true)
})
```


## Final Code
This is the final code for the game

```blocks
namespace SpriteKind {
    export const Rock = SpriteKind.create()
    export const PGate = SpriteKind.create()
    export const CGate = SpriteKind.create()
}
sprites.onOverlap(SpriteKind.Player, SpriteKind.PGate, function (sprite, otherSprite) {
    otherSprite.destroy(effects.coolRadial, 200)
    SkierSpeed += -5
    info.changeScoreBy(3)
})
sprites.onOverlap(SpriteKind.Player, SpriteKind.Rock, function (sprite, otherSprite) {
    otherSprite.destroy(effects.blizzard, 100)
    info.changeLifeBy(-1)
})
sprites.onDestroyed(SpriteKind.Rock, function (sprite) {
    info.changeScoreBy(1)
})
info.onLifeZero(function () {
    game.showLongText("\"you went\"" + Math.round(distance) + "\"feet!\"", DialogLayout.Center)
    info.changeScoreBy(Math.round(distance))
    game.over(false)
})
sprites.onOverlap(SpriteKind.Player, SpriteKind.CGate, function (sprite, otherSprite) {
    game.showLongText("\"you went\"" + Math.round(distance) + "\"feet!\"", DialogLayout.Center)
    info.changeScoreBy(Math.round(distance))
    game.over(true)
})
let CheckGate: Sprite = null
let PurpleGate: Sprite = null
let Rocks: Sprite = null
let distance = 0
scene.setBackgroundColor(1)
let mySprite = sprites.create(assets.image`Skier`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
mySprite.setPosition(80, 11)
distance = 0
let SkierSpeed = -20
let RockSpawnTime = 2000
let PurpleGateTimer = 5000
let CGateTimer = 7000
forever(function () {
    pause(100)
    distance += SkierSpeed * -0.05
})
forever(function () {
    Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
    Rocks.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
    Rocks.setVelocity(0, SkierSpeed)
    Rocks.setFlag(SpriteFlag.AutoDestroy, true)
    pause(RockSpawnTime)
})
forever(function () {
    PurpleGate = sprites.create(assets.image`Purple Gate`, SpriteKind.PGate)
    PurpleGate.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
    PurpleGate.setVelocity(0, SkierSpeed)
    pause(PurpleGateTimer)
})
forever(function () {
    if (distance >= 500) {
        CheckGate = sprites.create(assets.image`CheckGate`, SpriteKind.CGate)
        CheckGate.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
        CheckGate.setVelocity(0, SkierSpeed)
    }
    pause(CGateTimer)
})
game.onUpdateInterval(3000, function () {
    SkierSpeed += -5
    SkierSpeed = Math.max(SkierSpeed, -100)
    RockSpawnTime += -200
    RockSpawnTime = Math.max(RockSpawnTime, 500)
})
```


```assetjson
{
  "README.md": " ",
  "assets.json": "",
  "images.g.jres": "{\n    \"image2\": {\n        \"data\": \"hwQYACgAAAAAAAAAAAAAAAAAAADwDwD/AAAAAAAAAAAAAAAAAPD/AI////YAAAAAAAAAAAAAAAAAb4//iI9v9g8AAAAAAAAAAAAAAPBmiI/4/2ZoDwAAAAAAAAAA//D/b2Zo9v/4j2YPAAAAAAAAAPD4j/hohmb2j/j/Zv8AAAAAAACAj/iI/2ZmZoj4/2/2iA8AAAAAAGiI//+P+GiGiP/4b2j2DwAAAADwZmiP+I//Zmb2j/iPZv8PAP8AAI+GZoj//49mZviI/2iGaPj/7gCIZmaG+I/4/2iG/////49m/+7+gGZmZmb2iP+PZmaI+P//Zvbv7u6AZmZmZvj//2hmhoj//2hmhu/u/wCIZmaGiP///49m//j/b2aI+O7+AACPhmaP+P+PZmb2iP//aIj4/+4AAPBmaP//j/9mZoaP+GZm9g8A/wAAAGiIj/iP+GiG+P//b2j2DwAAAAAAgI/4iP9mZmaI/4hv9ogPAAAAAAAA8Pj//2iGZoj4j4hm/w8AAAAAAAAA/wD/j2Zo9v//j2YPAAAAAAAAAAAAAAAAaIb4j/hmaA8AAAAAAAAAAAAAAACA9oj/iG/2DwAAAAAAAAAAAAAAAAD/jw////YAAAAAAAAAAAAAAAAAAADwDwDwDwAAAAA=\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"displayName\": \"forestTree2\"\n    },\n    \"image4\": {\n        \"data\": \"hwQQABAAAAAAAAAAAAAAAAAiIiIiIiIiICIiIiIiIiIgIiIiIiIiIiAiIiIiIiIiICIiAAAAAAAgIiIAAAAAACAiIgAAAAAAICIiAAAAAAAgIiIAAAAAACAiIgAAAAAAICIiIiIiIiIgIiIiIiIiIiAiIiIiIiIiACIiIiIiIiIAAAAAAAAAAA==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"displayName\": \"Red Gate\"\n    },\n    \"image5\": {\n        \"data\": \"hwQQABAAAAAAAAAAAAAAAACIiIiIiIiIgIiIiIiIiIiAiIiIiIiIiICIiIiIiIiIgIiIAAAAAACAiIgAAAAAAICIiAAAAAAAgIiIAAAAAACAiIgAAAAAAICIiAAAAAAAgIiIiIiIiIiAiIiIiIiIiICIiIiIiIiIAIiIiIiIiIgAAAAAAAAAAA==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"displayName\": \"Blue Gate\"\n    },\n    \"image1\": {\n        \"data\": \"hwQYABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACgqqqqqqqqAKCqqqqqqqoKoKqqIqKqqgAAACAiIgAAAAAAICKCCAAAAAAgIoiIAAAAACAigggAAAAAICIiAAAAoKqqIqKqqgCgqqqqqqqqCqCqqqqqqqoAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA=\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"displayName\": \"Skier\"\n    },\n    \"image3\": {\n        \"data\": \"hwQQABAAAAAAAAAAAMDMzAAAAADMvMzMAAAAzL28y8wAAMzMG8vLzADAu80cy8zMAByx27zLzMzAEREbu8u8zMAR0Ru7zLzLHBHR3My7vLscEd3MzLy9uxwRvczdu727HBHNHBG9wbvMEcscEb3BvMDMzBwRzc3MAADMzNHLy8wAAADAzMzMzA==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"displayName\": \"mediumOceanRock\"\n    },\n    \"image6\": {\n        \"data\": \"hwQQABAAAAAAAAAAAAAAAACqqqqqqqqqoKqqqqqqqqqgqqqqqqqqqqBaqqqqqqqqoFWlAAAAAACgWqoAAAAAAKCqqgAAAAAAUFVaAAAAAABQWloAAAAAAFBaVQAAAAAAoKqqqqqqqqqgqqqqqqqqqqCqqqqqqqqqAKqqqqqqqqoAAAAAAAAAAA==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"displayName\": \"Purple Gate\"\n    },\n    \"image7\": {\n        \"data\": \"hwQQABAAAAAAAAAAAAAAAAB3d3d3d3d3cHd3d3d3d3fw8fF3d3d3dxAfH3d3d3d38PHxAAAAAAAQHx8AAAAAAPDx8QAAAAAAEB8fAAAAAADw8fEAAAAAABAfHwAAAAAA8PHxd3d3d3cQHx93d3d3d3B3d3d3d3d3AHd3d3d3d3cAAAAAAAAAAA==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"displayName\": \"CheckGate\"\n    },\n    \"*\": {\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"dataEncoding\": \"base64\",\n        \"namespace\": \"myImages\"\n    }\n}",
  "images.g.ts": "// Auto-generated code. Do not edit.\nnamespace myImages {\n\n    helpers._registerFactory(\"image\", function(name: string) {\n        switch(helpers.stringTrim(name)) {\n            case \"image2\":\n            case \"forestTree2\":return img`\n........................\n...........88...........\n..........8668..........\n..........8668..........\n.........f6666f.........\n........f866668f........\n.......8666666668.......\n......866866668668......\n......f8866666688f......\n.....f886686686688f.....\n....f88ff88688fff88f....\n....ffff88fff88f8fff....\n.....f8f8ff8ff8f88f.....\n....f88fff88fffff8f.....\n....f8ffff8fffffffff....\n....fff88ffffff88fff....\n....f868ffff8fff868f....\n...f666ff8f86f8ff668....\n..f6666866866f6686668...\n.f66686666666866668668..\n.ff8866666666666666866f.\n.f8866686686866686668ff.\n..ff668868f88f66888688f.\n..f8ff88fff88ff8f88ff88f\n.f88ff8ff8f8f88fff8fffff\nf88ff8ff88ffff88ffff8f..\nffff88f88ffffff8f8ff88f.\n.f8ffffffffffffff88ff8f.\n.ff6fffff8ff8ff6ff8f6ff.\n.f668f6686ff66f6668866ff\nf668666866f666868666866f\nfff666f6688666666f666ff.\n..ffff86f866688668ffff..\n.....f8ff66f888ff8f.....\n......fff8fff88ffff.....\n.........ffeeff.........\n.........feeeef.........\n.........feeeef.........\n........feeefeef........\n........fefeffef........\n`;\n            case \"image4\":\n            case \"Red Gate\":return img`\n. . . . . . . . . . . . . . . . \n. . 2 2 2 2 2 2 2 2 2 2 2 2 . . \n. 2 2 2 2 2 2 2 2 2 2 2 2 2 2 . \n. 2 2 2 2 2 2 2 2 2 2 2 2 2 2 . \n. 2 2 2 2 2 2 2 2 2 2 2 2 2 2 . \n. 2 2 2 2 2 2 2 2 2 2 2 2 2 2 . \n. 2 2 2 2 . . . . . . 2 2 2 2 . \n. 2 2 2 2 . . . . . . 2 2 2 2 . \n. 2 2 2 2 . . . . . . 2 2 2 2 . \n. 2 2 2 2 . . . . . . 2 2 2 2 . \n. 2 2 2 2 . . . . . . 2 2 2 2 . \n. 2 2 2 2 . . . . . . 2 2 2 2 . \n. 2 2 2 2 . . . . . . 2 2 2 2 . \n. 2 2 2 2 . . . . . . 2 2 2 2 . \n. 2 2 2 2 . . . . . . 2 2 2 2 . \n. 2 2 2 2 . . . . . . 2 2 2 2 . \n`;\n            case \"image5\":\n            case \"Blue Gate\":return img`\n. . . . . . . . . . . . . . . . \n. . 8 8 8 8 8 8 8 8 8 8 8 8 . . \n. 8 8 8 8 8 8 8 8 8 8 8 8 8 8 . \n. 8 8 8 8 8 8 8 8 8 8 8 8 8 8 . \n. 8 8 8 8 8 8 8 8 8 8 8 8 8 8 . \n. 8 8 8 8 8 8 8 8 8 8 8 8 8 8 . \n. 8 8 8 8 . . . . . . 8 8 8 8 . \n. 8 8 8 8 . . . . . . 8 8 8 8 . \n. 8 8 8 8 . . . . . . 8 8 8 8 . \n. 8 8 8 8 . . . . . . 8 8 8 8 . \n. 8 8 8 8 . . . . . . 8 8 8 8 . \n. 8 8 8 8 . . . . . . 8 8 8 8 . \n. 8 8 8 8 . . . . . . 8 8 8 8 . \n. 8 8 8 8 . . . . . . 8 8 8 8 . \n. 8 8 8 8 . . . . . . 8 8 8 8 . \n. 8 8 8 8 . . . . . . 8 8 8 8 . \n`;\n            case \"image1\":\n            case \"Skier\":return img`\n........................\n......aaa.....aaa.......\n......aaa.....aaa.......\n......aaa.....aaa.......\n......aaa.....aaa.......\n......aaa22222aaa.......\n......aa2222222aa.......\n......aa2222222aa.......\n......aa2228222aa.......\n......aaa28882aaa.......\n......aaa.888.aaa.......\n......aaa..8..aaa.......\n......aaa.....aaa.......\n......aaa.....aaa.......\n.......a.......a........\n........................\n`;\n            case \"image3\":\n            case \"mediumOceanRock\":return img`\n. . . . . . . . c c c c c . . . \n. . . . . . c c 1 1 1 1 c c . . \n. . . . . c 1 1 1 1 1 1 1 c . . \n. . . . c 1 1 1 1 1 1 1 1 c . . \n. . . c b 1 1 1 1 d d d b c c . \n. . . c b b 1 d d d b c c c c . \n. . c c d b b b c c c c c c c . \n. . c c c d 1 1 d c c 1 1 1 c c \n. c d b c c b b c c d 1 1 1 1 c \n. c b 1 1 b b b c c d 1 1 1 d c \n. c c b b b b c b c b d d d b c \nc b b c c c c c b b b b b c c c \nc c b b c c c c c d d 1 1 d b c \nc c c c c c b b b b b c c c c c \nc c c c c c c b b b b b c c c c \nc c c c c c c c b b b b b c c c \n`;\n            case \"image6\":\n            case \"Purple Gate\":return img`\n. . . . . . . . . . . . . . . . \n. . a a a a a a 5 5 5 a a a . . \n. a a a a 5 a a 5 a a a a a a . \n. a a a 5 5 5 a 5 5 5 a a a a . \n. a a a a 5 a a a a 5 a a a a . \n. a a a a a a a 5 5 5 a a a a . \n. a a a a . . . . . . a a a a . \n. a a a a . . . . . . a a a a . \n. a a a a . . . . . . a a a a . \n. a a a a . . . . . . a a a a . \n. a a a a . . . . . . a a a a . \n. a a a a . . . . . . a a a a . \n. a a a a . . . . . . a a a a . \n. a a a a . . . . . . a a a a . \n. a a a a . . . . . . a a a a . \n. a a a a . . . . . . a a a a . \n`;\n            case \"image7\":\n            case \"CheckGate\":return img`\n. . . . . . . . . . . . . . . . \n. . 7 f 1 f 1 f 1 f 1 f 1 7 . . \n. 7 7 1 f 1 f 1 f 1 f 1 f 7 7 . \n. 7 7 f 1 f 1 f 1 f 1 f 1 7 7 . \n. 7 7 1 f 1 f 1 f 1 f 1 f 7 7 . \n. 7 7 f 1 f 1 f 1 f 1 f 1 7 7 . \n. 7 7 7 7 . . . . . . 7 7 7 7 . \n. 7 7 7 7 . . . . . . 7 7 7 7 . \n. 7 7 7 7 . . . . . . 7 7 7 7 . \n. 7 7 7 7 . . . . . . 7 7 7 7 . \n. 7 7 7 7 . . . . . . 7 7 7 7 . \n. 7 7 7 7 . . . . . . 7 7 7 7 . \n. 7 7 7 7 . . . . . . 7 7 7 7 . \n. 7 7 7 7 . . . . . . 7 7 7 7 . \n. 7 7 7 7 . . . . . . 7 7 7 7 . \n. 7 7 7 7 . . . . . . 7 7 7 7 . \n`;\n        }\n        return null;\n    })\n\n    helpers._registerFactory(\"animation\", function(name: string) {\n        switch(helpers.stringTrim(name)) {\n\n        }\n        return null;\n    })\n\n}\n// Auto-generated code. Do not edit.\n",
  "main.blocks": "<xml xmlns=\"https://developers.google.com/blockly/xml\"><variables><variable type=\"KIND_SpriteKind\" id=\"}+j~0uB[O-Ev3Z/rS2BG\">Rock</variable><variable type=\"KIND_SpriteKind\" id=\"::e;HYn:y/jserwvp,H:\">PGate</variable><variable type=\"KIND_SpriteKind\" id=\"lH1qc?7aoMT9%o=IP~Jr\">CGate</variable><variable type=\"KIND_SpriteKind\" id=\"-x`lxxwc1,sOR*fqU0B3\">Player</variable><variable type=\"KIND_SpriteKind\" id=\"@BPd*p^7iAwQvi~z]kqN\">Projectile</variable><variable type=\"KIND_SpriteKind\" id=\".~ir,7495mjqV7I[30},\">Food</variable><variable type=\"KIND_SpriteKind\" id=\"MJw;nmMaaQ`P1F8cC%XM\">Enemy</variable><variable id=\"QW*jlKg?*{X!i~8`|Tkn\">SkierSpeed</variable><variable id=\"{[ZVq~o+-x%pAtt,+7pC\">distance</variable><variable id=\"~]kRoSSScwAFjk81qL2#\">Rocks</variable><variable id=\"!KVeyU1F8i~dua@9,4yQ\">RockSpawnTime</variable><variable id=\"(F;_}dB@k`MLkW=677o*\">PurpleGate</variable><variable id=\"`QSYU?Lu+Kk9oh_],e9,\">PurpleGateTimer</variable><variable id=\")9Ba?PQ7POy{j:QL,Bel\">CheckGate</variable><variable id=\"+1:;E.5VkMF:uUbJ]jiL\">mySprite</variable><variable id=\"BclbIm;{r]X-9C?gM*Y#\">CGateTimer</variable></variables><block type=\"pxt-on-start\" x=\"0\" y=\"0\"><statement name=\"HANDLER\"><block type=\"gamesetbackgroundcolor\"><value name=\"color\"><shadow type=\"colorindexpicker\"><field name=\"index\">1</field></shadow></value><next><block type=\"variables_set\"><field name=\"VAR\" id=\"+1:;E.5VkMF:uUbJ]jiL\">mySprite</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"spritescreate\"><value name=\"img\"><shadow type=\"screen_image_picker\"><field name=\"img\">assets.image`Skier`</field><data>{\"commentRefs\":[],\"fieldData\":{\"img\":\"myImages.image1\"}}</data></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Player</field></shadow></value></block></value><next><block type=\"game_control_sprite\"><mutation xmlns=\"http://www.w3.org/1999/xhtml\" _expanded=\"0\" _input_init=\"false\"></mutation><value name=\"sprite\"><shadow type=\"variables_get\"><field name=\"VAR\" id=\"+1:;E.5VkMF:uUbJ]jiL\">mySprite</field></shadow></value><next><block type=\"spritesetsetstayinscreen\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"+1:;E.5VkMF:uUbJ]jiL\">mySprite</field></block></value><value name=\"on\"><shadow type=\"toggleOnOff\"><field name=\"on\">true</field></shadow></value><next><block type=\"spritesetpos\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"+1:;E.5VkMF:uUbJ]jiL\">mySprite</field></block></value><value name=\"x\"><shadow type=\"positionPicker\"><field name=\"index\">80</field></shadow></value><value name=\"y\"><shadow type=\"positionPicker\"><field name=\"index\">11</field></shadow></value><next><block type=\"variables_set\"><field name=\"VAR\" id=\"{[ZVq~o+-x%pAtt,+7pC\">distance</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow></value><next><block type=\"variables_set\"><field name=\"VAR\" id=\"QW*jlKg?*{X!i~8`|Tkn\">SkierSpeed</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">-20</field></shadow></value><next><block type=\"variables_set\"><field name=\"VAR\" id=\"!KVeyU1F8i~dua@9,4yQ\">RockSpawnTime</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">2000</field></shadow></value><next><block type=\"variables_set\"><field name=\"VAR\" id=\"`QSYU?Lu+Kk9oh_],e9,\">PurpleGateTimer</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">5000</field></shadow></value><next><block type=\"variables_set\"><field name=\"VAR\" id=\"BclbIm;{r]X-9C?gM*Y#\">CGateTimer</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">7000</field></shadow></value></block></next></block></next></block></next></block></next></block></next></block></next></block></next></block></next></block></next></block></statement></block><block type=\"forever\" x=\"657\" y=\"0\"><statement name=\"HANDLER\"><block type=\"device_pause\"><value name=\"pause\"><shadow type=\"timePicker\"><field name=\"ms\">100</field></shadow></value><next><block type=\"variables_change\"><field name=\"VAR\" id=\"{[ZVq~o+-x%pAtt,+7pC\">distance</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"math_arithmetic\"><field name=\"OP\">MULTIPLY</field><value name=\"A\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"variables_get\"><field name=\"VAR\" id=\"QW*jlKg?*{X!i~8`|Tkn\">SkierSpeed</field></block></value><value name=\"B\"><shadow type=\"math_number\"><field name=\"NUM\">-0.05</field></shadow></value></block></value></block></next></block></statement></block><block type=\"forever\" x=\"1280\" y=\"0\"><statement name=\"HANDLER\"><block type=\"variables_set\"><field name=\"VAR\" id=\"~]kRoSSScwAFjk81qL2#\">Rocks</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"spritescreate\"><value name=\"img\"><shadow type=\"screen_image_picker\"><field name=\"img\">assets.image`mediumOceanRock`</field><data>{\"commentRefs\":[],\"fieldData\":{\"img\":\"myImages.image3\"}}</data></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Rock</field></shadow></value></block></value><next><block type=\"spritesetpos\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"~]kRoSSScwAFjk81qL2#\">Rocks</field></block></value><value name=\"x\"><shadow type=\"positionPicker\"></shadow><block type=\"device_random\"><value name=\"min\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow></value><value name=\"limit\"><block type=\"scenescreenwidth\"></block></value></block></value><value name=\"y\"><shadow type=\"positionPicker\"></shadow><block type=\"scenescreenheight\"></block></value><next><block type=\"spritesetvel\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"~]kRoSSScwAFjk81qL2#\">Rocks</field></block></value><value name=\"vx\"><shadow type=\"spriteSpeedPicker\"><field name=\"speed\">0</field></shadow></value><value name=\"vy\"><shadow type=\"spriteSpeedPicker\"></shadow><block type=\"variables_get\"><field name=\"VAR\" id=\"QW*jlKg?*{X!i~8`|Tkn\">SkierSpeed</field></block></value><next><block type=\"spritesetsetflag\"><field name=\"flag\">SpriteFlag.AutoDestroy</field><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"~]kRoSSScwAFjk81qL2#\">Rocks</field></block></value><value name=\"on\"><shadow type=\"toggleOnOff\"><field name=\"on\">true</field></shadow></value><next><block type=\"device_pause\"><value name=\"pause\"><shadow type=\"timePicker\"></shadow><block type=\"variables_get\"><field name=\"VAR\" id=\"!KVeyU1F8i~dua@9,4yQ\">RockSpawnTime</field></block></value></block></next></block></next></block></next></block></next></block></statement></block><block type=\"forever\" x=\"2200\" y=\"0\"><statement name=\"HANDLER\"><block type=\"variables_set\"><field name=\"VAR\" id=\"(F;_}dB@k`MLkW=677o*\">PurpleGate</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"spritescreate\"><value name=\"img\"><shadow type=\"screen_image_picker\"><field name=\"img\">assets.image`Purple Gate`</field><data>{\"commentRefs\":[],\"fieldData\":{\"img\":\"myImages.image6\"}}</data></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">PGate</field></shadow></value></block></value><next><block type=\"spritesetpos\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"(F;_}dB@k`MLkW=677o*\">PurpleGate</field></block></value><value name=\"x\"><shadow type=\"positionPicker\"></shadow><block type=\"device_random\"><value name=\"min\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow></value><value name=\"limit\"><block type=\"scenescreenwidth\"></block></value></block></value><value name=\"y\"><shadow type=\"positionPicker\"></shadow><block type=\"scenescreenheight\"></block></value><next><block type=\"spritesetvel\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"(F;_}dB@k`MLkW=677o*\">PurpleGate</field></block></value><value name=\"vx\"><shadow type=\"spriteSpeedPicker\"><field name=\"speed\">0</field></shadow></value><value name=\"vy\"><shadow type=\"spriteSpeedPicker\"></shadow><block type=\"variables_get\"><field name=\"VAR\" id=\"QW*jlKg?*{X!i~8`|Tkn\">SkierSpeed</field></block></value><next><block type=\"device_pause\"><value name=\"pause\"><shadow type=\"timePicker\"></shadow><block type=\"variables_get\"><field name=\"VAR\" id=\"`QSYU?Lu+Kk9oh_],e9,\">PurpleGateTimer</field></block></value></block></next></block></next></block></next></block></statement></block><block type=\"gameinterval\" x=\"725\" y=\"575\"><value name=\"period\"><shadow type=\"timePicker\"><field name=\"ms\">3000</field></shadow></value><statement name=\"HANDLER\"><block type=\"variables_change\"><field name=\"VAR\" id=\"QW*jlKg?*{X!i~8`|Tkn\">SkierSpeed</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">-5</field></shadow></value><next><block type=\"variables_set\"><field name=\"VAR\" id=\"QW*jlKg?*{X!i~8`|Tkn\">SkierSpeed</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"math_op2\"><field name=\"op\">max</field><value name=\"x\"><block type=\"variables_get\"><field name=\"VAR\" id=\"QW*jlKg?*{X!i~8`|Tkn\">SkierSpeed</field></block></value><value name=\"y\"><shadow type=\"math_number\"><field name=\"NUM\">-100</field></shadow></value></block></value><next><block type=\"variables_change\"><field name=\"VAR\" id=\"!KVeyU1F8i~dua@9,4yQ\">RockSpawnTime</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">-200</field></shadow></value><next><block type=\"variables_set\"><field name=\"VAR\" id=\"!KVeyU1F8i~dua@9,4yQ\">RockSpawnTime</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"math_op2\"><field name=\"op\">max</field><value name=\"x\"><block type=\"variables_get\"><field name=\"VAR\" id=\"!KVeyU1F8i~dua@9,4yQ\">RockSpawnTime</field></block></value><value name=\"y\"><shadow type=\"math_number\"><field name=\"NUM\">500</field></shadow></value></block></value></block></next></block></next></block></next></block></statement></block><block type=\"gamelifeevent\" x=\"1471\" y=\"575\"><statement name=\"HANDLER\"><block type=\"game_show_long_text\"><field name=\"layout\">DialogLayout.Center</field><value name=\"str\"><shadow type=\"text\"><field name=\"TEXT\"></field></shadow><block type=\"text_join\"><mutation items=\"3\"></mutation><value name=\"ADD0\"><shadow type=\"text\"><field name=\"TEXT\">\"you went\"</field></shadow></value><value name=\"ADD1\"><shadow type=\"text\"><field name=\"TEXT\"></field></shadow><block type=\"math_js_round\"><field name=\"OP\">round</field><value name=\"ARG0\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"variables_get\"><field name=\"VAR\" id=\"{[ZVq~o+-x%pAtt,+7pC\">distance</field></block></value></block></value><value name=\"ADD2\"><shadow type=\"text\"><field name=\"TEXT\">\"feet!\"</field></shadow></value></block></value><next><block type=\"hudChangeScoreBy\"><value name=\"value\"><block type=\"math_js_round\"><field name=\"OP\">round</field><value name=\"ARG0\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"variables_get\"><field name=\"VAR\" id=\"{[ZVq~o+-x%pAtt,+7pC\">distance</field></block></value></block></value><next><block type=\"gameOver\"><mutation xmlns=\"http://www.w3.org/1999/xhtml\" _expanded=\"0\" _input_init=\"false\"></mutation><value name=\"win\"><shadow type=\"toggleWinLose\"><field name=\"win\">false</field></shadow></value></block></next></block></next></block></statement></block><block type=\"spritesondestroyed\" x=\"0\" y=\"908\"><value name=\"HANDLER_DRAG_PARAM_sprite\"><shadow type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">sprite</field></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Rock</field></shadow></value><statement name=\"HANDLER\"><block type=\"hudChangeScoreBy\"><value name=\"value\"><shadow type=\"math_number\"><field name=\"NUM\">1</field></shadow></value></block></statement></block><block type=\"spritesoverlap\" x=\"431\" y=\"908\"><value name=\"HANDLER_DRAG_PARAM_sprite\"><shadow type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">sprite</field></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Player</field></shadow></value><value name=\"HANDLER_DRAG_PARAM_otherSprite\"><shadow type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">otherSprite</field></shadow></value><value name=\"otherKind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Rock</field></shadow></value><statement name=\"HANDLER\"><block type=\"spritedestroy\"><mutation xmlns=\"http://www.w3.org/1999/xhtml\" _expanded=\"2\" _input_init=\"true\"></mutation><field name=\"effect\">effects.blizzard</field><value name=\"sprite\"><block type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">otherSprite</field></block></value><value name=\"duration\"><shadow type=\"timePicker\"><field name=\"ms\">100</field></shadow></value><next><block type=\"hudChangeLifeBy\"><value name=\"value\"><shadow type=\"math_number\"><field name=\"NUM\">-1</field></shadow></value></block></next></block></statement></block><block type=\"spritesoverlap\" x=\"1175\" y=\"908\"><value name=\"HANDLER_DRAG_PARAM_sprite\"><shadow type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">sprite</field></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Player</field></shadow></value><value name=\"HANDLER_DRAG_PARAM_otherSprite\"><shadow type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">otherSprite</field></shadow></value><value name=\"otherKind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">PGate</field></shadow></value><statement name=\"HANDLER\"><block type=\"spritedestroy\"><mutation xmlns=\"http://www.w3.org/1999/xhtml\" _expanded=\"2\" _input_init=\"true\"></mutation><field name=\"effect\">effects.coolRadial</field><value name=\"sprite\"><block type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">otherSprite</field></block></value><value name=\"duration\"><shadow type=\"timePicker\"><field name=\"ms\">200</field></shadow></value><next><block type=\"variables_change\"><field name=\"VAR\" id=\"QW*jlKg?*{X!i~8`|Tkn\">SkierSpeed</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">-5</field></shadow></value><next><block type=\"hudChangeScoreBy\"><value name=\"value\"><shadow type=\"math_number\"><field name=\"NUM\">3</field></shadow></value></block></next></block></next></block></statement></block><block type=\"variables_get\" disabled=\"true\" x=\"1946\" y=\"908\"><field name=\"VAR\" id=\"+1:;E.5VkMF:uUbJ]jiL\">mySprite</field></block><block type=\"variables_get\" disabled=\"true\" x=\"2112\" y=\"908\"><field name=\"VAR\" id=\"+1:;E.5VkMF:uUbJ]jiL\">mySprite</field></block><block type=\"forever\" x=\"130\" y=\"1070\"><statement name=\"HANDLER\"><block type=\"controls_if\"><value name=\"IF0\"><shadow type=\"logic_boolean\"><field name=\"BOOL\">TRUE</field></shadow><block type=\"logic_compare\"><field name=\"OP\">GTE</field><value name=\"A\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"variables_get\"><field name=\"VAR\" id=\"{[ZVq~o+-x%pAtt,+7pC\">distance</field></block></value><value name=\"B\"><shadow type=\"math_number\"><field name=\"NUM\">500</field></shadow></value></block></value><statement name=\"DO0\"><block type=\"variables_set\"><field name=\"VAR\" id=\")9Ba?PQ7POy{j:QL,Bel\">CheckGate</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"spritescreate\"><value name=\"img\"><shadow type=\"screen_image_picker\"><field name=\"img\">assets.image`CheckGate`</field><data>{\"commentRefs\":[],\"fieldData\":{\"img\":\"myImages.image7\"}}</data></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">CGate</field></shadow></value></block></value><next><block type=\"spritesetpos\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\")9Ba?PQ7POy{j:QL,Bel\">CheckGate</field></block></value><value name=\"x\"><shadow type=\"positionPicker\"></shadow><block type=\"device_random\"><value name=\"min\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow></value><value name=\"limit\"><block type=\"scenescreenwidth\"></block></value></block></value><value name=\"y\"><shadow type=\"positionPicker\"></shadow><block type=\"scenescreenheight\"></block></value><next><block type=\"spritesetvel\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\")9Ba?PQ7POy{j:QL,Bel\">CheckGate</field></block></value><value name=\"vx\"><shadow type=\"spriteSpeedPicker\"><field name=\"speed\">0</field></shadow></value><value name=\"vy\"><shadow type=\"spriteSpeedPicker\"></shadow><block type=\"variables_get\"><field name=\"VAR\" id=\"QW*jlKg?*{X!i~8`|Tkn\">SkierSpeed</field></block></value></block></next></block></next></block></statement><next><block type=\"device_pause\"><value name=\"pause\"><shadow type=\"timePicker\"><field name=\"ms\">100</field></shadow><block type=\"variables_get\"><field name=\"VAR\" id=\"BclbIm;{r]X-9C?gM*Y#\">CGateTimer</field></block></value></block></next></block></statement></block><block type=\"spritesoverlap\" x=\"1250\" y=\"1230\"><value name=\"HANDLER_DRAG_PARAM_sprite\"><shadow type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">sprite</field></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Player</field></shadow></value><value name=\"HANDLER_DRAG_PARAM_otherSprite\"><shadow type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">otherSprite</field></shadow></value><value name=\"otherKind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">CGate</field></shadow></value><statement name=\"HANDLER\"><block type=\"game_show_long_text\"><field name=\"layout\">DialogLayout.Center</field><value name=\"str\"><shadow type=\"text\"><field name=\"TEXT\"></field></shadow><block type=\"text_join\"><mutation items=\"3\"></mutation><value name=\"ADD0\"><shadow type=\"text\"><field name=\"TEXT\">\"you went\"</field></shadow></value><value name=\"ADD1\"><shadow type=\"text\"><field name=\"TEXT\"></field></shadow><block type=\"math_js_round\"><field name=\"OP\">round</field><value name=\"ARG0\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"variables_get\"><field name=\"VAR\" id=\"{[ZVq~o+-x%pAtt,+7pC\">distance</field></block></value></block></value><value name=\"ADD2\"><shadow type=\"text\"><field name=\"TEXT\">\"feet!\"</field></shadow></value></block></value><next><block type=\"hudChangeScoreBy\"><value name=\"value\"><block type=\"math_js_round\"><field name=\"OP\">round</field><value name=\"ARG0\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"variables_get\"><field name=\"VAR\" id=\"{[ZVq~o+-x%pAtt,+7pC\">distance</field></block></value></block></value><next><block type=\"gameOver\"><mutation xmlns=\"http://www.w3.org/1999/xhtml\" _expanded=\"0\" _input_init=\"false\"></mutation><value name=\"win\"><shadow type=\"toggleWinLose\"><field name=\"win\">true</field></shadow></value></block></next></block></next></block></statement></block></xml>",
  "main.ts": "namespace SpriteKind {\n    export const Rock = SpriteKind.create()\n    export const PGate = SpriteKind.create()\n    export const CGate = SpriteKind.create()\n}\nsprites.onOverlap(SpriteKind.Player, SpriteKind.PGate, function (sprite, otherSprite) {\n    otherSprite.destroy(effects.coolRadial, 200)\n    SkierSpeed += -5\n    info.changeScoreBy(3)\n})\nsprites.onOverlap(SpriteKind.Player, SpriteKind.Rock, function (sprite, otherSprite) {\n    otherSprite.destroy(effects.blizzard, 100)\n    info.changeLifeBy(-1)\n})\nsprites.onDestroyed(SpriteKind.Rock, function (sprite) {\n    info.changeScoreBy(1)\n})\ninfo.onLifeZero(function () {\n    game.showLongText(\"\\\"you went\\\"\" + Math.round(distance) + \"\\\"feet!\\\"\", DialogLayout.Center)\n    info.changeScoreBy(Math.round(distance))\n    game.over(false)\n})\nsprites.onOverlap(SpriteKind.Player, SpriteKind.CGate, function (sprite, otherSprite) {\n    game.showLongText(\"\\\"you went\\\"\" + Math.round(distance) + \"\\\"feet!\\\"\", DialogLayout.Center)\n    info.changeScoreBy(Math.round(distance))\n    game.over(true)\n})\nlet CheckGate: Sprite = null\nlet PurpleGate: Sprite = null\nlet Rocks: Sprite = null\nlet distance = 0\nscene.setBackgroundColor(1)\nlet mySprite = sprites.create(assets.image`Skier`, SpriteKind.Player)\ncontroller.moveSprite(mySprite)\nmySprite.setStayInScreen(true)\nmySprite.setPosition(80, 11)\ndistance = 0\nlet SkierSpeed = -20\nlet RockSpawnTime = 2000\nlet PurpleGateTimer = 5000\nlet CGateTimer = 7000\nforever(function () {\n    pause(100)\n    distance += SkierSpeed * -0.05\n})\nforever(function () {\n    Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)\n    Rocks.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())\n    Rocks.setVelocity(0, SkierSpeed)\n    Rocks.setFlag(SpriteFlag.AutoDestroy, true)\n    pause(RockSpawnTime)\n})\nforever(function () {\n    PurpleGate = sprites.create(assets.image`Purple Gate`, SpriteKind.PGate)\n    PurpleGate.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())\n    PurpleGate.setVelocity(0, SkierSpeed)\n    pause(PurpleGateTimer)\n})\nforever(function () {\n    if (distance >= 500) {\n        CheckGate = sprites.create(assets.image`CheckGate`, SpriteKind.CGate)\n        CheckGate.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())\n        CheckGate.setVelocity(0, SkierSpeed)\n    }\n    pause(CGateTimer)\n})\ngame.onUpdateInterval(3000, function () {\n    SkierSpeed += -5\n    SkierSpeed = Math.max(SkierSpeed, -100)\n    RockSpawnTime += -200\n    RockSpawnTime = Math.max(RockSpawnTime, 500)\n})\n",
  "pxt.json": "{\n    \"name\": \"Downhill Ski V2.0\",\n    \"description\": \"\",\n    \"dependencies\": {\n        \"device\": \"*\"\n    },\n    \"files\": [\n        \"main.blocks\",\n        \"main.ts\",\n        \"README.md\",\n        \"assets.json\",\n        \"images.g.jres\",\n        \"images.g.ts\",\n        \"tilemap.g.jres\",\n        \"tilemap.g.ts\"\n    ],\n    \"targetVersions\": {\n        \"branch\": \"v1.8.6\",\n        \"tag\": \"v1.8.6\",\n        \"commits\": \"https://github.com/microsoft/pxt-arcade/commits/0a7c70fbd5b49238ff1863f55640d33531b82578\",\n        \"target\": \"1.8.6\",\n        \"pxt\": \"7.4.14\"\n    },\n    \"preferredEditor\": \"blocksprj\"\n}\n",
  "tilemap.g.jres": "{\n    \"transparency16\": {\n        \"data\": \"hwQQABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true\n    },\n    \"*\": {\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"dataEncoding\": \"base64\",\n        \"namespace\": \"myTiles\"\n    }\n}",
  "tilemap.g.ts": "// Auto-generated code. Do not edit.\nnamespace myTiles {\n    //% fixedInstance jres blockIdentity=images._tile\n    export const transparency16 = image.ofBuffer(hex``);\n\n    helpers._registerFactory(\"tile\", function(name: string) {\n        switch(helpers.stringTrim(name)) {\n            case \"transparency16\":return transparency16;\n        }\n        return null;\n    })\n\n}\n// Auto-generated code. Do not edit.\n"
}
```