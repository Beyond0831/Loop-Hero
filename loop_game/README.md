1. Aims

Apply object-oriented programming principles and design patterns
Synthesise and adapt to changes in user requirements
Practice agile software development in a team environment
Work with the Java Programming Language and Java Class Libraries
Learn practical aspects of graphical user interface development
Appreciate issues in design and development
Design reusable software solutions


2. Client Requirements 🧳
The client wants you to develop a game application called "Loop Mania" as described below. The proposed game application is like the application "Loop Hero" (free download is available here) with many major changes, so please read the requirements below, as you need to follow them for this project.
The following describes the features the client wants in Loop Mania.

The game world contains a path composed of image tiles (see more details in this document) which forms a loop. The Character automatically moves clockwise from position to position through this path, starting from the Hero's Castle  (see example in separate file:moving through path).
The game world contains buildings (see buildings table below), enemies (see enemies table below), gold , health potions , and the Character . You can see more information about gold and health potions in the items table below. Enemies will move around the path, and their method of doing so depends on the enemy type.
It is important to note that in this document, the Human Player and Character are distinct:

The Character refers to the main Character within the game which the Human Player wishes to help win the game, represented by a picture of a person . The Character completes many interactions such as moving around and fighting battles automatically, without input from the Human Player.
The Human Player refers to the user playing the game application. The Human Player wishes to win the game by helping the Character complete all goals, and is able to help the Character win the game by creating buildings (see buildings table below), equipping items (see items table below), purchasing and selling items, consuming health potions, and pausing the game (pausing makes it easier to drag and drop).

When the Character is attacked by an enemy, a battle is started involving nearby enemies and the Character, and either the Character will defeat all enemies within this battle and win rewards, which can consist of cards (see buildings table below), experience, gold, and equipment (see items table below). Alternatively, the Character will be killed and the Human Player loses the game, and the game ends. The battle is automatically played - the Human Player has no ability to perform any game interactions during a battle.
More precisely, when the Character moves within the battle radius of an enemy on the path (this differs by type of enemy), a battle will commence. Those enemies for which the Character is within their support radius (support radius is distinct from battle radius, and differs by type of enemy) will join the battle against the Character and its allies. Some enemies such as vampires have a larger support radius (see enemies table below).

In the example above, when the Character moves to the position indicated by the red arrow, the Character will be within the battle radius of the slug, and within the support radius of the vampire, so a battle will be started between the Character and the slug, and the vampire will join the battle in support of the slug.
These radii are calculated as a straight-line distance in the above example (the circles are drawn to indicate the distance around the vampire/slug, you do not need to draw circles in your application). You can implement calculation of distance differently if you prefer.
Challenging bosses spawn when specified conditions are met. Killing them provides special items and larger experience upgrades.
The Character may lose health from a battle. Health can be restored fully by consuming a health potion (see example in separate file:using health potion). Health potions can be bought from the Hero's Castle, taken from dead enemies, picked up from the ground, or obtained when a card is destroyed due to having too many cards (as below). You should determine in your design how best to allow the Character to consume a health potion.
Gold can be obtained by selling items at the Hero's Castle, by killing enemies, or by picking it up from the ground, when a card is destroyed due to having too many cards (as below), or when an item is destroyed due to having too many items (as below).

Cards are received when the Character defeats enemies (1 or more will be received at the bottom of the screen, as in this example in separate file:gold/experience/cards). The Human Player can drag and drop these cards onto appropriate places on the map which depend on the building type, as outlined in the buildings table below (see examples in separate files here:drop locations, and here:dragging cards). Dropping a card on a valid location spawns the building corresponding to that card at the location of the drop. The Human Player will want to create buildings since they can provide various benefits, as outlined in the buildings table below. When too many cards are received, the oldest card is lost, and the Character receives additional gold, experience, and items  (see example in separate file:replacing oldest card).

Equipment can be received when the Character defeats enemies or a card is lost due to receiving too many cards (see example in separate file:replacing oldest card) (for both events, one or more pieces of equipment can be received). The Human Player can drag and drop the equipment from the unequipped inventory into the equipped inventory, so that the benefits of the equipment improve the Character, improving the chances of winning the game. When too much equipment is received, the oldest piece of equipment is lost, and the Character receives additional gold and experience (see example in separate file:replacing oldest item).
The Human Player should be able to pause the game by pressing Spacebar, and then resume it by pressing Spacebar again.
After the first full cycle of the path (returning to the Hero's castle for the first time), the Human Player should be offered a menu where armour, shields, helmets, and weapons can be purchased by using gold (see more details on these items in the items table below). When the Human Player exits this menu, the game resumes from the same game world state. After another 2 full cycles of the path, the Human Player will be able to access the Hero's castle again to purchase items, then again after another 3 full cycles, etc (a full cycle is where the Character moves throughout the path once, as in this example in separate file:moving through path)... After buying items at the Hero's Castle (if the Human Player wishes) the Human Player should be able to continue the game. You will need to design this menu.
When the Character moves through a barracks, it will be joined by an allied soldier  (see minimalistic example in separate file:allied soldier generated from barracks - note you cannot see the allied soldier join the player on the path, as it's a basic version!). The soldier joins the Character, and fights as an ally in battles until it is killed or turned into a zombie.
When starting the game, the Human Player should have the option of choosing "Standard Mode", "Survival Mode", "Berserker Mode", or "Confusing Mode":

In survival mode, the Human Player can only purchase 1 health potion each time the Character shops at the Hero's Castle.
In berserker mode, the Human Player cannot purchase more than 1 piece of protective gear (protective gear includes armour, helmets, and shields) each time it shops at the Hero's Castle.
Standard mode has no distinguishing effects.
In confusing mode, rare items look the same as the original item, but have both their original properties/behaviour, and the added properties/behaviour of another random rare item. For example, "The One Ring" may allow respawning upon death of the character (the original behaviour), and also enable the player to inflict a higher amount of damage against all enemies and triple damage against bosses (the added behaviour of the sword "Anduril, Flame of the West").

The game is won once the Character has completed some specified combination of goals, which are some logical combination of killing all bosses, obtaining a specified level of experience, amassing a specified amount of gold, and completing a specified number of cycles of the path). See goals section below for more information.
The client overall wants you to satisfy the criteria, but as you can see in the specification, there are some things you can change regarding how the game is developed. You can show your creativity here and add more features. You should also apply UI design principles to improve and extend the UI.

2.1 Enemies 🐙

Possible enemy types are listed below:



Enemy Type
Example
Description
Spawn conditions




Slug

A standard enemy type. Low health and low damage. The battle radius is the same as the support radius for a slug.
Spawns randomly on path tiles


Zombie

*Braaaaaaiiiinnnnnssss!*Zombies have low health, moderate damage, and are slower compared to other enemies. A critical bite from a zombie against an allied soldier (which has a random chance of occurring) will transform the allied soldier into a zombie, which will then proceed to fight against the Character until it is killed. Zombies have a higher battle radius than slugs
Spawns from zombie pit every time the Character completes a cycle of the path


Vampire

*I vant to suck your blood!*Vampires have high damage, are susceptible to the stake weapon, and run away from campfires. They have a higher battle radius than slugs, and an even higher support radius. A critical bite (which has a random chance of occurring) from a vampire causes random additional damage with every vampire attack, for a random number of vampire attacks
Spawns from vampire castle every 5 cycles of the path completed by the Character


Doggie


Wow much coin how money so crypto plz mine v rich very currencyA special boss which spawns the DoggieCoin upon defeat, which randomly fluctuates in sellable price to an extraordinary extent. It has high health and can stun the character, which prevents the character from making an attack temporarily. The battle and support radii are the same as for slugs
Spawns after 20 cycles


Elan Muske

*To the moon!*An incredibly tough boss which, when appears, causes the price of DoggieCoin to increase drastically. Defeating this boss causes the price of DoggieCoin to plummet. Elan has the ability to heal other enemy NPCs. The battle and support radii are the same as for slugs
Spawns after 40 cycles, and the player has reached 10000 experience points




2.2 Buildings 🏛️
The following are the available building types for your project:



Building Type
Example
Card To Spawn Building
Description
Placement




Vampire castle


Produces vampires every 5 cycles of the path completed by the Character, spawning nearby on the path
Only on non-path tiles adjacent to the path


Zombie pit


Produces zombies every cycle of the path completed by the Character, spawning nearby on the path
Only on non-path tiles adjacent to the path


Tower


During a battle within its shooting radius, enemies will be attacked by the tower
Only on non-path tiles adjacent to the path


Village


Character regains health when passing through
Only on path tiles


Barracks


Produces allied soldier to join Character when passes through
Only on path tiles


Trap


When an enemy steps on a trap, the enemy is damaged (and potentially killed if it loses all health) and the trap is destroyed
Only on path tiles


Campfire


Character deals double damage within campfire battle radius
Any non-path tile


Hero's Castle

N/A
Character starts at the Hero's Castle, and upon finishing the required number of cycles of the path completed by the Character, when the Character enters this castle, the Human Player is offered a window to purchase items at the Hero's Castle
Exists at the starting position of the Character (not spawned by a card, always exists)




2.3 Basic Items ⚔️
Possible basic item types are listed below:



Item Type
Example
Description
Where can obtain




Sword

A standard melee weapon. Increases damage dealt by Character
Purchase in Hero's Castle, loot from enemies, or obtained from cards lost due to being the oldest and replaced


Stake

A melee weapon with lower stats than the sword, but causes very high damage to vampires
Purchase in Hero's Castle, loot from enemies, or obtained from cards lost due to being the oldest and replaced


Staff

A melee weapon with very low stats (lower than both the sword and stake), which has a random chance of inflicting a trance, which transforms the attacked enemy into an allied soldier temporarily (and fights alongside the Character). If the trance ends during the fight, the affected enemy reverts back to acting as an enemy which fights the Character. If the fight ends whilst the enemy is in a trance, the enemy dies
Purchase in Hero's Castle, loot from enemies, or obtained from cards lost due to being the oldest and replaced


Armour

Body armour, provides defence and halves enemy attack
Purchase in Hero's Castle, loot from enemies, or obtained from cards lost due to being the oldest and replaced


Shield

Defends against enemy attacks, critical vampire attacks have a 60% lower chance of occurring
Purchase in Hero's Castle, loot from enemies, or obtained from cards lost due to being the oldest and replaced


Helmet

Defends against enemy attacks, enemy attacks are reduced by a scalar value. The damage inflicted by the Character against enemies is reduced (since it is harder to see)
Purchase in Hero's Castle, loot from enemies, or obtained from cards lost due to being the oldest and replaced


Gold

Money, used to buy things
Obtain in Hero's Castle by selling items, loot from enemies, pick up off the ground, or obtained from cards/items lost due to being the oldest and replaced. Spawns randomly on path tiles


Health potion

Refills Character health
Purchase from Hero's Castle, loot from enemies, pick up off the ground, or obtained from cards lost due to being the oldest and replaced. Spawns randomly on path tiles


DoggieCoin

A revolutionary asset type, which randomly fluctuates in sellable price to an extraordinary extent. Can sell at shop
Obtained when defeat Doggie



Basic item types may be available in every game (receiving a particular item/items is based on random chance after winning a battle).

2.4 Rare Items 🔱

Every time the Character wins a battle, there is a small chance of winning a "Rare Item". The available rare items are specified in the world configuration file.
Rare items are listed below:



Rare Item Type
Example
Description




The One Ring

If the Character is killed, it respawns with full health up to a single time


Anduril, Flame of the West

A very high damage sword which causes triple damage against bosses


Tree Stump

An especially powerful shield, which provides higher defence against bosses



Note that DoggieCoin is not considered to be a rare item, since the player will have the opportunity to obtain DoggieCoin every game.
Rare item types will not be available in a game if it is not added to the world configuration file.

2.5 Evolution of Requirements 🤖

The following requirements have been added to the applicable sections in this specification document:

Bosses
DoggieCoin
Additional rare items
An additional "confusing mode"
A goal type of killing all bosses

See commit link with milestone 3 requirement additions for full details.
Suggestion about Elan Muske boss behaviour: when the boss Elan Muske is spawned, it is unlikely (although possible) by the above requirements that the player will reach the shop before having to fight Elan. So it is unlikely the requirement to have the DoggieCoin price fluctuate will come into effect. You could implement a small extension so Elan Muske randomly "jumps over" the player without fighting, making the price fluctuation more likely to come into effect - this would improve the gameplay (but it is not compulsory to do this specifically, just a suggestion)!

2.6 Diversity in Behaviour/Features 🌎

You will notice that the above requirements allow you significant freedom in how you will implement the game. For example, these requirements do not define particular battle/support radii for different enemies, the types of random distributions to use, the event to trigger the Character consuming a potion (e.g. pressing a particular keyboard key), and many other aspects you will need to decide on.
Whilst you're implementing different behaviour in your game (e.g. if you added an extension with new types of enemies, or clarify ambiguities), make sure that the behaviours you have implemented are different in nature rather than similar to existing behaviours with slight modifications.
For example, in the above enemy definition table, the vampire has different behaviour from slugs by causing additional random damage for critical bites which continues for several attacks after the critical bite. If we implemented a game where vampires simply had different attack and defence values compared to slugs, but no different behaviours, this would be an example of low behaviour diversity.
With respect to Object Oriented Programming (OOP), high behaviour diversity in your code will result in different behavioural methods being required for different backend entities, and more complex relationships between the entities, and thus will incentivise the use of design patterns.
With respect to how enjoyable a game is - high behaviour diversity should result in your game having more diverse ways to play the game, rewarding Human Player creativity, increasing replayability, and making the game more enjoyable.
Notice in this separate game example, behaviour diversity for enemy types is implemented through various abilities/traits. Something similar to this could be a nifty extension!

2.7 Goals 🥅

In addition to its layout, each world also has a goal that defines what must be achieved by the Character for the world to be considered complete. Basic goals are:

Killing all bosses
Obtaining a specified level of experience
Amassing a specified amount of gold
The Character completing a specified number of cycles of the path

More complex goals can be built by logically composing goals. For example,

Killing all bosses AND amassing 10000 gold
Amassing 90000 gold OR completing 100 cycles
Obtaining 123456 experience points AND (completing 100 cycles OR amassing 11000 gold)
Obtaining 123456 experience points AND (killing all bosses OR amassing 11000 gold)


2.8 Input ➡️
Your application will read from a JSON file containing a complete specification of the world (the initial position of entities, goal, etc.). Example worlds are included in the worlds directory and the starter code contains an incomplete world loader.
The world files have the following format:

{ "width": width in squares, "height": height in squares, "rare_items": list of available rare items, "entities": list of entities, "goal-condition": goal condition }

Each entity in the list of entities is structured as:

{ "type": type, "x": x-position, "y": y-position }

where type is one of (you could add more to the below list)

["path_tile", "hero_castle"]

The goal condition is a JSON object representing the logical statement that defines the goal. The bosses goal is specified as:

{ "goal": "bosses" }

Other basic goals (those with associated numerical quantity) are specified as:

{ "goal": goal, "quantity": quantity }

where goal is one of

["experience", "gold", "cycles"]

and quantity is an integer.
In the case of a more complex goal, goal is the logical operator and the additional subgoals field is a JSON array containing subgoals, which themselves are goal conditions. For example,

{ "goal": "AND", "subgoals":
  [ { "goal": "cycles", "quantity": 100 },
    { "goal": "OR", "subgoals":
      [ {"goal": "experience", "quantity": 123456 },
        { "goal": "bosses" }
      ]
    }
  ]
}


Note that the same basic goal can appear more than once in a statement.
list of available rare items will be some sublist (possibly the full list, or an empty list) of:

["the_one_ring", "anduril_flame_of_the_west", tree_stump"]

You can extend this format to include additional information if you wish.

2.9 Frontend 🎮

The UI/Frontend component of this project will be implemented in JavaFX. The starter code contains several features:

Handling drag-and-drop of cards onto the game map/items into the equipped inventory
Loading the path
Loading of the Character/enemies/cards/items/path/buildings
Spawning a building upon dropping a dragged card onto the game world
Removal of defeated enemies/used cards
A main menu which can switch to the main game using a button click, and vice versa
Character moves clockwise through the path around the world
The enemies move randomly around the path
Basic but incomplete implementations of interactions such as the player killing enemies, and obtaining swords/cards as a reward
Game is paused upon pressing Spacebar, and can be resumed upon pressing Spacebar


Notice however, that whilst there are several features implemented in the starter code, there is significant work to be done regarding implementing different types of items, enemies, and OOP structure/class relationships within the backend. The starter code primarily focuses on implementing some challenging setup/UX components which are required to make a solid attempt at the basic requirements, such as setting up the path, implementing drag-and-drop, and menus, so that you can focus on Object Oriented Design.
The client has given you free reign over the visual design of the program. Included in the starter code are some example assets, but you are free to use different ones. You can find them elsewhere or even create your own.
