# ProjectBlackJack.github.io
BlackJack card game

## Welcome to iSchool Style: BlackJack
by: Alex Acuna, Anthony J. Aruldoss, Daniel Monyei

### OVERVIEW and APPROACH

- Approach/ideology
- Challenges
- Successful Group Practices 
- How/Why we selected a project idea 

**Components:**
  - Dictionaries
  - Lists 
  - Global and local variables
  - If/elif/else statements
  - While loops
  - Print/Prompt/Input statements
 
**Key Tasks:**
- Establishing iSchool Rules
- A dictionary used to simulate a deck of cards
- Draw function using random.choice()
- Summing number of cards in hand/drawed and total card value
- HIT or STAY 
- Simulating up to 5 player draws
- PUSH (Ties; Dealer Card Value == Player Card Value)
- BUST (card value > 21)
- Aces ( == 11 versus == 1)

 
### STEPS TO FUNCTIONALITY

1. Dealer vs. Player Variables
2. Do you want to play (Yes/No?)
3. random.choice() player 2 cards
4. State keys (cards in hand) and value
5. HIT/STAY?
6. If hit, random.choice() another card
7. State keys and value
8. If Ace choose 1 or 11
9. HIT (instance 1, 2, 3, 4, and/or 5)
10. WIN? LOST? BUST? PUSH

### CHALLENGES

- Aces to be valued at 1 or 11?
- Dealing with invalid user inputs
- Ties
- First hand == 21
- Class Storage Name as player & Dealer
- Creating Rules (Computer Logic vs Human Logic)
- User Friendliness

### CODE

```
import random

deck = {"Ace of Diamonds": 11, "Two of Diamonds" : 2, "Three of Diamonds": 3 , "Four of Diamonds": 4 , "Five of Diamonds" : 5,
        "Six of Diamonds": 6, "Seven of Diamonds": 7, "Eight of Diamonds": 8, "Nine of Diamonds": 9, "Ten of Diamonds": 10,
        "Jack of Diamonds" :10,"Queen of Diamonds": 10, "King of Diamonds" : 10, "Ace of Hearts": 11,
        "Two of Hearts": 2, "Three of Hearts": 3 ,"Four of Hearts": 4, "Five of Hearts": 5, "Six of Hearts": 6,
        "Seven of Hearts": 7, "Eight of Hearts": 8,"Nine of Hearts": 9, "Ten of Hearts": 10,
        "Jack of Hearts": 10, "Queen of Hearts": 10, "King of Hearts": 10,
        "Ace of Spades": 11, "Two of Spades": 2, "Three of Spades": 3, "Four of Spades": 4,
        "Five of Spades": 5, "Six of Spades": 6, "Seven of Spades": 7, "Eight of Spades": 8, "Nine of Spades": 9,
        "Ten of Spades": 10, "Jack of Spades": 10, "Queen of Spades": 10, "King of Spades": 10, "Ace of Clubs": 11,
        "Two of Clubs": 2, "Three of Clubs": 3, "Four of Clubs": 4, "Five of Clubs": 5, "Six of Clubs": 6,
        "Seven of Clubs": 7, "Eight of Clubs": 8, "Nine of Clubs": 9, "Ten of Clubs": 10,
        "Jack of Clubs": 10, "Queen of Clubs": 10, "King of Clubs": 10
        }

def score_hand(hand):
    score_without_aces = 0
    ace_count = 0
    possible_scores = []
    for card in hand:
        if card.startswith('Ace'):
            ace_count += 1
            pass
        else:
            score_without_aces += deck[card]
    if ace_count == 0:
        return score_without_aces
    elif ace_count == 1:

        possible_scores.append(score_without_aces + 1)
        possible_scores.append(score_without_aces + 11)
    elif ace_count == 2:

        possible_scores.append(score_without_aces + 2)
        possible_scores.append(score_without_aces + 12)
    elif ace_count == 3:

        possible_scores.append(score_without_aces + 3)
        possible_scores.append(score_without_aces + 13)
    elif ace_count == 4:

        possible_scores.append(score_without_aces + 4)
        possible_scores.append(score_without_aces + 14)
    elif ace_count == 5:

        possible_scores.append(score_without_aces + 5)
        possible_scores.append(score_without_aces + 15)
    for s in sorted(possible_scores, reverse = True):
        if s > 21:
            continue
        else:
            return s

class Players:
    def __init__(self, name):
        self.name = name
        self.hand = []
    def draw(self):
        list_deck = list(deck)
        if len(self.hand) == 0:
            self.hand.append(random.choice(list_deck))
            self.hand.append(random.choice(list_deck))
            print(self.name + 'Hand: ' + ', '.join(self.hand))
        else:
            self.hand.append(random.choice(list_deck))
            print(self.name + 'Hand: ' + ', '.join(self.hand))

dealer = Players("Dealer")
player = Players("Player")

Start_or_Stop = input("Welcome to ISchool Casino Blackjack table, Press Enter to continue or 'NO' to Exit")
print("Rules: 1. Dealer must stay on all 17's" '\n' + '       ' + "2. When player has 5 cards in hand and value less than or equal to 21, player wins.  ")#  " '\n' + '       '
    #  + "3.
print("***************************************************************************************************************")

if Start_or_Stop == '' \
                    '':
    player.draw()
    sum_of_player = score_hand(player.hand)
    print("Hand Total: ", sum_of_player)
    #print("Cards in Hand: ", len(player.hand))
    if sum_of_player == 21:
        print("Blackjack, YOU WIN")
        exit()
    choice = input("Do you want to 'HIT' or 'STAY', type your result. ")
    decision = choice.upper()
    while decision == 'HIT':
        #print(player.hand)
        player.draw()
        #print(player.hand)
        sum_of_player = score_hand(player.hand)
        if sum_of_player == None:
            print("BUST, better luck next time.")
            exit()
        print("Hand Total: ", sum_of_player)
        #print("Cards in Hand: ", player.hand)
        if sum_of_player == 21:
            print("Blackjack, YOU WIN")
            break
        if len(player.hand) >= 5 and sum_of_player < 21:
            print("You beat the odds, YOU WIN")
            exit()
        elif sum_of_player > 21:
            print("BUST, better luck next time.")
            exit()

        choice = input("Do you want to 'HIT' or 'STAY', type your result. ")
        decision = choice.upper()
    while decision == "STAY":
            dealer.draw()
            sum_of_dealer = score_hand(dealer.hand)
            print("Dealer Total: ", sum_of_dealer)
           # print("Cards in Hand: ", dealer.hand)
            #print(sum_of_dealer)
            if sum_of_player == sum_of_dealer:
                print("push....you Tie, maybe next time.")
                exit()
            if sum_of_dealer == None:
                print("Dealer Bust, Player wins")
                exit()
            while sum_of_dealer < 17:
                dealer.draw()
                sum_of_dealer = score_hand(dealer.hand)
                print("Dealer Total: ", sum_of_dealer)
                #print("number of cards in dealer hand", dealer.hand)
                #print("Total of dealer cards", sum_of_dealer)
                if sum_of_player == sum_of_dealer:
                    print("push....you Tie, maybe next time.")
                    exit()
                if sum_of_dealer > 21:
                         print("Dealer Bust, Player wins")
                         exit()
            if sum_of_dealer >= 17:
                if sum_of_player > sum_of_dealer:
                    print("You Win, Test your luck with another round?")
                    exit()
                elif sum_of_dealer > sum_of_player:
                    print("You lose, play again???")
                    exit()
            exit()
if Start_or_Stop == "NO":
        print("You have exited game")

#****************************************************************************************************************************************
#Fixes:

        # user input corrections with no error status


        # Add on: press enter to play again.....maybe????


        # add names to the output numbers - Completed
        # fix upper and lowercsase inputs - COMPLETED
        # bug if first cards are black jack why no win - Completed
        # fix ace problem, once it accounts for ace it still sees ace count as 1 and will subtract 10 for each additional hit - Completed
        # weird bug of Tie  not working in answer to give answer when both are automatic from the random generator.......why???? - Completed

# Example may work:

        while True:
            choice = input("Do you want to 'HIT' or 'STAY', type your result. ")
            decision = choice.upper()
            try:
                choice = ('hit', 'HIT', 'H', 'h', 'hits', 'HITS', 'stay', 'STAY', 'S', 's', 'stays', 'STAYS')
                break
            except:
                print("This was not a valid input, please try again.")
        exit()


        while True:
            Start_or_Stop = input("Welcome to ISchool Casino Blackjack table, Press Enter to continue or 'NO' to Exit")
            try:
                choice = ('No', 'no', 'n', ''
                                           '')
                break
            except:
                print("This was not a valid input, please try again.")
        exit()


```
