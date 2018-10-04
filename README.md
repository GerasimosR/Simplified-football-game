# Simplified Football Game
The game evolves into a grid as shown in the following pictures and for simplification we think that a footballer moves only horizontally (he always remains in the same line) and also if he has the ball he can also transfer it to a particular line again. For example, player Π can only move to the blue area and send the ball to the yellow line. If the ball is in the green or red area then there is a chance of a goal being scored by the corresponding team.

![map](https://raw.githubusercontent.com/GerasimosR/Simplified-football-game/master/map.png)

The **Team** class represents a football team and contains a list of Player class objects, representing a player and his Team Name, Mistakes, Passes and Goals variables.

The **Player** class is an abstract class, has coordinates (X, Y) and has fields for the name, jersey number, the line of the field on which he is allowed to move (Movement Line) and the line of the field in which he is allowed to transfer the ball (Aim Line). It also has three main methods: Movement, Transfer, and Special Movement.

 - **Movement:** Simply moves the player to a position either left or right (always stays on his Movement Line and of course within the boundaries of the map).
 - **Transfer:**  If the player has in his possession the ball, he transfers it to a random column of the Aim Line.
 - **Special Movement:** Is overloaded in each subclass by a different function.

The Defender and Forward are subclasses of Player class. 
- The **Defender** has extra variables, like the number of Yellow Cards and the number of Steals. If the ball is in the possession of an opponent player, who is surrounded by a Defender, Defender steals the ball with a 70% probability. If he fails stealing the ball, he receives a yellow card with a probability of 20%. If the Defender had already received a yellow card before, he is being removed from the simulation.
    - _The **Midfielder** is a subclass of Defender class, with similar behavior._
- The **Forward** moves away from the nearest opponent, since the ball is in the possession of a teammate. He is also more likely to transfer the ball near to the center columns. 
    - _The **Striker** is a subclass of Forward class, with similar behavior._        

The **Ball** class represents the ball of the game and has coordinates (X,Y) and two variables pointing to Player Objects: Current Player and Ex Player. The Current Player points either to the player who has the ball in his possession or to NULL if it is free. The Ex Player when the ball is free points to the last one Current Player. If the ball is free (Current Player Player points to NULL) and is adjacent to the Player Π then assigns Player Π as the Current Player. If the Ex Player and Player Π are in the same team, we increase their team's Passes (successful transfers). Otherwise, we increase their statistical mistakes (failed transfers).

The **Team** Class has an action() method that loops over the players of a team and for each one 1) performs randomly one of the Movement (35% probability), Transfer (35%), Special Movement (30%) methods and then 2) checks if the player can take possession of the ball.

The **Game** class has a variable that holds how many rounds have passed since the beginning of the game. The runTurn() method runs action() for each of the Teams (in random order). At the end of each round, if the ball is near the nets (see yellow or red area in the original image) then a goal can be scored with 50% probability, otherwise the ball is assigned to the nearest player.

In the **main()** function, we create a Game object and make the necessary initializations by uploading the necessary data (eg. players' details and their initial positions) from a file. The simulation ends either if a specific number of game iterations is completed or if one of the two teams scores a specific number of goals.

_**Game Assumptions:**_ 
1) _We assume that is permitted only one player in each line._
2) _There must be at least one player whose Aim line points to the opponent's net (in order to score a goal)._
3) _Whenever the ball stays in the same position for 5 consecutive rounds, it is automatically assigned to the nearest player._


