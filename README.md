# Logisim cannon game

This is a game/project made in logisim. The game consists in destroying all the stars in the top of the 32x32 screen with the cannon at the bottom. The player can move left or right and can tilt the cannon left or right. The player loses if the bullets hit the cannon itself (by bouncing back at the player).

## How to start

Use logisim to open the game. Once the project is loaded then the ticks/clock must be enabled and the frequency set to 64/128 Hz (for optimal experience). Finally, press the start button and select the keyboard input in order to move the cannon.


The description of the components are below.

### Main

In this circuit are found the 32x32 screen, the keyboard input to move the cannon, the cannonMov subcircuit and the general movement subcircuit. All of these together make the game functional.

### Keyboard

In this subcircuit the keyboard input is managed. The player can use the A and D keys to move to the sides and the Q and E keys to tilt the direction of the cannon.

### CannonMov

In this subcircuit the movement of the cannon is managed. The player can move to the sides in the bottom of the 32x32 board and can also tilt the cannon. This circuits moves the cannon and analyzes if the player or the cannon are going out of boundaries, and also fires the command if the player shoots the cannon.

### MoveBullet

In this circuit the bullet position is read, and depending of the direction at the moment it return the next position of it. It also analyzes if the bullets hit the wall, so they must return the next position in the opposite direction (because it bounces on the wall).

### rowCompare

It verifies if the incoming bullet will hit a star, if it's true then it will return the intersection of the row with the bullet and the row with the stars (resulting in the row with that star destroyed) and will also return a signal indicating that the player has destroyed a star (to increase the score)

### rowReg

In this circuit the rows of the matrix will be updated given the position of the bullets going upward or downward. It will return the updated position of the row, the updated position of the bullet and their properties (like the bullet inclination and bounce check).


### rowModifier

This will receive the outputs of rowCompare, that is, the position of the initially random generated rows, the new position of the bullet and the indication if there was a hit (bullet hitting a star). When there is a hit, the row of the intersection will be modified, removing the star.

### movement

This circuit has 30 rowReg and 60 moveBullet, which will allow to save the registers of each bullet in each row and their movement be it upward or downward. This will give in real time all the modifications made to the matrix.


### Score

If a star is destroyed, this circuit will update the score of the player

### cannonHit

It is possible to lose the game. This happens if the incoming downward bullet is going to hit the cannon. This circuit verifies if the bullet is going to hit the player, and if that's true then the game ends.



