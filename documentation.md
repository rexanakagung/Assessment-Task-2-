# Assessment-Task-2

## PART A: Data Selection and Attributes.
I have chose these attributes as they are the main factors of a car, they are easily interpereted and flexible. This allows  players to have the ability to understand these attributes as they are extremely simple, these are the Acceleration, engine size, Braking Speed, Horsepower, Year and Top speed of a car. I will be obtaining real life data from the website carsales.com. 

### Attributes (From Most powerful to Least)
1. Top Speed: This attribute refers to the highest speed a particular car model can reach under normal driving conditions. It is valuable to both drivers and manufacturers because it helps drivers understand the level of tyre speed required and reassures them that the car can maintain highway speeds without putting excessive strain on the engine. At the same time, it offers an indication of the vehicle’s overall strength, performance, and reliability. This attribute was selected because top speed is widely recognised as a universal symbol of a car’s performance and status. However, placing too much emphasis on it can cause other important attributes to be overlooked, giving top speed an unfair advantage. This highlights the need for power limits on certain attributes to be applied thoughtfully and in balance.

2. Acceleration: Acceleration refers to the rate at which a vehicle can speed up and how responsive it will be when the driver steps on the accelerator pedal. The most common test used for determining acceleration involves measuring the time it takes for a vehicle to go from standstill to normal driving speed or even better, the time it takes to change velocities. It is an essential feature of a car in day-to-day driving as it will help in pulling away from traffic signals, merging into high-speed lanes and responding to unforeseen dangers such as animals or any other objects in the road. Electric vehicles tend to perform better when it comes to acceleration since they can deliver power immediately without taking time to rev the engine up like conventional engines do. Acceleration has come to be used as a standard means of comparing the performance of one car against another; however, it should always be considered together with other aspects such as weight, grip, and power.

3. Engine Size: The attribute engine size is one of the most important factors of a car or vehchile. It refers to the total volume of all the engine;s cyllinders combine usually measured in Litres. It is the engines cpacity which  dictates how a vehicle drives and how much fuel it consumes. 

4. Braking Speed: This attribute is not mainly recorded but is still extemelt important when it comes to racing. This is attttribute is included in this game as it is easy to understand and compare. 

5. Horsepower: The measure of horsepower defines how powerful the engine of the car is in terms of producing energy and, therefore, provides a reliable way to evaluate the power of a particular vehicle. The more horsepower the engine of a vehicle has, the greater power it produces, which means that it becomes easier for the engine to accelerate and maintain high speeds. It is widely used for comparison of different cars, since it makes it possible to compare two vehicles from the point of view of their power. Thus, horsepower not only determines the speed of the car but influences its ability to accelerate, which makes it a vital factor in driving. Nevertheless, besides being a good indication of the power of a vehicle, it does not provide full information about the performance of the car, since other factors also play an important role in it.

6. Year: The year of the car classifies what year the car was produced. This is so that users can determine if the car is up to date with the standards as most people would want the latest and greatest. It also tell us how advanced the tecnology is as we can determine between the timestamps of the years.



# Examples of Car

| Attributes    | Example of 2021 BMW X1 sDrive18i F48 LCI Auto     | Measurements In Game |   |   |
|---------------|---------------------------------------------------|----------------------|---|---|
| Acceleration  | 0-100 km/h 9.6-9.7 seconds                        | 1-100                |   |   |
| Engine Size   | 1.5‑litre (1499 cm³) inline‑3 turbocharged petrol | 0.5L - 5L            |   |   |
| Braking Speed | 100–0 km/h braking distance: 36–38 metres         | 1-100                |   |   |
| Horsepower    | 134 hp / 136 PS / 100 kW @ 4500 rpm               | 100-1000             |   |   |
| Year          | 2021 (F48 LCI facelift generation)                | eg (2000)            |   |   |
| Top speed     | Top speed: 205 km/h (127 mph)                     | KM                   |   |   |

# Part B — Class Design

## Car

**Attributes ()**
- `private String make`
- `private String model`
- `private int year`
- `private double acceleration`
- `private double engineSize`
- `private double brakingSpeed`
- `private int horsepower`
- `private int topSpeed`

**Methods ()**
- `public String getMake()`
- `public String getModel()`
- `public int getYear()`
- `public double getAcceleration()`
- `public double getEngineSize()`
- `public double getBrakingSpeed()`
- `public int getHorsepower()`
- `public int getTopSpeed()`
- `public String displaySpecs()`

**Description ()**
This stores the real-world data for a single car, sourced from carsales.com. It holds the six attributes selected in Part A and exists purely to store data — it has no game logic, which keeps it reusable and separates "what a car is" from "how the game uses it."

---

## Card

**Attributes ()**
- `private Car car`
- `private boolean isFaceUp`
- `private String cardID`

**Methods ()**
- `public Car getCar()`
- `public double getAttributeValue(String attributeName)`
- `public void revealCard()`
- `public String displayCard()`

**Description ()**
This wraps a Car object so the card game doesn't need to know about car internals directly — Card is the thing that gets played, compared and passed between players, while Car is just the data. This is a composition relationship (Card *has a* Car), worth naming explicitly in your justification.

---

## Deck

**Attributes ()**
- `private ArrayList<Card> cards`
- `private int remainingCards`

**Methods ()**
- `public void buildDeck()`
- `public void shuffleDeck()`
- `public Card dealCard()`
- `public boolean isEmpty()`
- `public int getRemainingCount()`
- `public void resetDeck()`

**Description ()**
This manages the full collection of cards — building it from car data, shuffling, and dealing one card at a time to players. It's the only class that should touch the full set of cards at once, keeping Player and Game from needing to know how dealing actually works.

---

## Player

**Attributes ()**
- `private int playerID`
- `private String playerName`
- `private ArrayList<Card> hand`
- `private int score`
- `private int roundsWon`
- `private boolean isCurrentTurn`
- `private Card activeCard`

**Methods ()**
- `public void drawCard(Deck deck)`
- `public Card playCard()`
- `public String chooseAttribute()`
- `public void receiveCard(Card card)`
- `public void addPoint()`
- `public void incrementRoundsWon()`
- `public Card getTopCard()`
- `public boolean hasCardsRemaining()`
- `public void displayHand()`

**Description ()**
This is the player and here is where actions that the player can take to play will be executed.

---

## Game

**Attributes ()**
- `private int gameID`
- `private ArrayList<Player> players`
- `private Deck deck`
- `private int currentRound`
- `private Player currentPlayer`
- `private Player winningPlayer`
- `private String gameStatus`
- `private Player roundWinner`
- `private ArrayList<Card> cardsInBattle`

**Methods ()**
- `public void startGame()`
- `public void setupPlayers()`
- `public void dealCards()`
- `public void playRound()`
- `public void compareCards()`
- `public Player determineRoundWinner()`
- `public void awardCardsToWinner()`
- `public void switchTurn()`
- `public boolean checkGameOver()`
- `public Player determineGameWinner()`
- `public void displayLeaderboard()`
- `public void restartGame()`
- `public void endGame()`

**Description ()**
This allows the system to interact with turns from players and terminate, start and manipulate the game.

# PART C: Class Design
https://excalidraw.com/#json=A9Y11RIg6_-Fu5RXHhZPc,AhuPKHOZRIhA0x5Hm2w9Wg
![alt text](<Class Diagram.png>)

# Part D: Game Mechanics Design 
How a round is played
The game begins by each player having his/her own deck of cards with the faces downward, and he/she can only see the topmost card of his/her deck.Around begins by each player having his/her own deck of cards with the faces downward, and he/she can only see the topmost card of his/her deck. The player whose turn it is looks at his/her topmost card and chooses one out of the six attributes, let’s say horsepower, to play against each other for that particular round. Each player then turns their topmost card upward at the same time, and whoever gets the highest value of that particular chosen attribute wins the round. He/She takes all the cards that have been played and adds them to the bottom of his/her own deck, and he/She becomes the one to decide the attribute for the next round.

Selection of Attributes

Each player evaluates his/her top card and chooses from any of the six attributes, acceleration, engine size, braking, horse power, year, or top speed that he/she thinks gives him/her an edge in winning that round. This is done without consulting any of the other players hence giving the player on his/her turn an edge since the player will be playing his/her own strengths.

Winning in a Round

Once the attributes have been chosen, all players will play their top cards and the numbers for that particular attribute will be compared. The person with the highest number will win the round and he/she will take all the cards played and place them at the bottom of his/her pile. The winner will choose the attribute for the next round. 

How the game ends
The game ends when one player has all of the cards, while the rest have none. The player with all the cards wins. If there is a pre-set number of rounds, the winner is the player who has more cards at that point.

Game Balance
The balance is achieved by normalizing each attribute so that each one does not exceed the maximum value and therefore, no one car is superior in all aspects. A car with exceptionally high horsepower won't always win in top speed or acceleration, thus giving players actual choices during each round as opposed to having one card better than the rest at all times. Nevertheless, there is a big problem since horsepower and top speed are highly correlated in reality, and thus the winner can focus on only those two aspects.

Unfair advantage and fix
The main unfair advantage of the game is that the person whose turn it is picks the attribute, which gives the player an opportunity to always play according to their best attribute, while all other players have to react to this choice without any prior knowledge of what is being chosen. As a result of the game, the one who has been winning for several rounds is gaining more and more advantage, as the one who has won the round is picking the attribute in the next round, thus making it impossible for other players to catch up. The solution is to pick the attribute by a certain order regardless of who won the last round.