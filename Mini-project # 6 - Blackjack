# Mini-project #6 - Blackjack

import simplegui
import random

# load card sprite - 949x392 - source: jfitz.com
CARD_SIZE = (73, 98)
CARD_CENTER = (36.5, 49)
card_images = simplegui.load_image("http://commondatastorage.googleapis.com/codeskulptor-assets/cards.jfitz.png")

CARD_BACK_SIZE = (71, 96)
CARD_BACK_CENTER = (35.5, 48)
card_back = simplegui.load_image("http://commondatastorage.googleapis.com/codeskulptor-assets/card_back.png")    

# initialize some useful global variables
in_play = False
outcome = ""
score = 0

# define globals for cards
SUITS = ('C', 'S', 'H', 'D')
RANKS = ('A', '2', '3', '4', '5', '6', '7', '8', '9', 'T', 'J', 'Q', 'K')
VALUES = {'A':1, '2':2, '3':3, '4':4, '5':5, '6':6, '7':7, '8':8, '9':9, 'T':10, 'J':10, 'Q':10, 'K':10}
cards = []

# define card class
class Card:
    def __init__(self, suit, rank):
        if (suit in SUITS) and (rank in RANKS):
            self.suit = suit
            self.rank = rank
        else:
            self.suit = None
            self.rank = None
            print "Invalid card: ", suit, rank

    def __str__(self):
        return self.suit + self.rank

    def get_suit(self):
        return self.suit

    def get_rank(self):
        return self.rank

    def draw(self, canvas, pos):
        card_loc = (CARD_CENTER[0] + CARD_SIZE[0] * RANKS.index(self.rank), 
                    CARD_CENTER[1] + CARD_SIZE[1] * SUITS.index(self.suit))
        canvas.draw_image(card_images, card_loc, CARD_SIZE, [pos[0] + CARD_CENTER[0], pos[1] + CARD_CENTER[1]], CARD_SIZE)
        
# define hand class
        
class Hand:
    def __init__(self):
        self.cards = []
        self.ace = False
        #pass	# create Hand object

    def __str__(self):
        cards = 'Hand contains '
        for card in self.cards:
            cards += str(card) + ' '
        return cards    
        #pass	# return a string representation of a hand

    def add_card(self, card):
        self.cards.append(card)
        #pass	# add a card object to a hand

    def get_value(self):
        # count aces as 1, if the hand has an ace, then add 10 to hand value if it doesn't bust
        value = 0
        for card in self.cards:
            value += VALUES[card.get_rank()]
        for card in self.cards:
            if card.rank == 'A' and value <= 11:
                value += 10
        #pass	# compute the value of the hand, see Blackjack video
        return value
    
    def draw(self, canvas, pos):
        for card in self.cards:
            card.draw(canvas, pos) 
            pos[0] += CARD_SIZE[0]
        #pass	# draw a hand on the canvas, use the draw method for cards
    

# define deck class 
class Deck:
    def __init__(self):
        self.cards = []
        for suit in SUITS:
            for rank in RANKS:
                self.cards.append(Card(suit,rank))
        #pass	# create a Deck object

    def shuffle(self):
        # shuffle the deck 
        random.shuffle(self.cards)
        #pass    # use random.shuffle()

    def deal_card(self):
        return self.cards.pop()
        #pass	# deal a card object from the deck
    
    def __str__(self):
        cards = 'Deck contains '
        for card in self.cards:
            cards += str(card) + ' ' 
        return cards
        #pass	# return a string representing the deck


#define event handlers for buttons
def deal():
    global outcome, in_play, cards, deck, dealer, player
    deck = Deck()
    deck.shuffle()
    cards = Deck().cards
    # your code goes here
    dealer = Hand()
    player = Hand()
    dealer.add_card(deck.deal_card())
    player.add_card(deck.deal_card())
    dealer.add_card(deck.deal_card())
    player.add_card(deck.deal_card())
    in_play = True
    outcome = 'Hit or stand?'
    #print deck
    #print player
    #print dealer
def hit():
    #pass	# replace with your code below
    global player, deck, outcome, in_play, score
    # if the hand is in play, hit the player
    if in_play:
        player.add_card(deck.deal_card())
        if player.get_value() <= 21:
            print player.get_value()
        else:
            outcome = 'Player busted and lose.'
            in_play = False
            score -= 1
            outcome += ' New deal?'
    # if busted, assign a message to outcome, update in_play and score
    #print deck
    #print player
    #print dealer   
def stand():
    #pass	# replace with your code below
   
    # if hand is in play, repeatedly hit dealer until his hand has value 17 or more
    global player, deck, outcome, in_play, score
    if in_play:
        if player.get_value() > 21:
            outcome = 'Player busted and lose.'
            score -= 1
            outcome += ' New deal?'
        else:
            print dealer.get_value()
            while dealer.get_value() < 17:
                dealer.add_card(deck.deal_card())
            if dealer.get_value() > 21:
                outcome = 'Dealer busted, you win.'
                score += 1
            else:
                if(dealer.get_value()>=player.get_value()):
                    outcome = 'Dealer win.'
                    score -= 1
                else:
                    outcome = 'Player win.'
                    score += 1
            print dealer.get_value()
        in_play = False;
        outcome += ' New deal?'
    # assign a message to outcome, update in_play and score

# draw handler    
def draw(canvas):
    # test to make sure that card.draw works, replace with your code below
    canvas.draw_text('Dealer:', (100, 120), 20, 'Black')
    dealer.draw(canvas, [100, 150])
    canvas.draw_text('Player:', (100, 320), 20, 'Black')
    player.draw(canvas, [100, 350])
    canvas.draw_text(outcome, (250, 120), 20, 'Black')
    canvas.draw_text('Score:', (500, 50), 20, 'Black')
    canvas.draw_text(str(score), (500, 80), 20, 'Black')
    canvas.draw_text('Blackjack', (50, 50), 20, 'Black')
    # if in play, cover the dealer's first card
    if in_play:
        canvas.draw_image(card_back, CARD_BACK_CENTER, CARD_BACK_SIZE, [101 + CARD_BACK_CENTER[0], 151 + CARD_BACK_CENTER[1]], CARD_BACK_SIZE)
# initialization frame
frame = simplegui.create_frame("Blackjack", 600, 600)
frame.set_canvas_background("Green")

#create buttons and canvas callback
frame.add_button("Deal", deal, 200)
frame.add_button("Hit",  hit, 200)
frame.add_button("Stand", stand, 200)
frame.set_draw_handler(draw)


# get things rolling
deal()
frame.start()

# remember to review the gradic rubric
