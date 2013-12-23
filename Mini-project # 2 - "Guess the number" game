# template for "Guess the number" mini-project
# input will come from buttons and an input field
# all output for the game will be printed in the console
import random
import simplegui


# initialize global variables used in your code
secret_number = 0
guess_times = 0


# helper function to start and restart the game
def new_game():
    range100()
    
# define event handlers for control panel
def range100():
    # button that changes range to range [0,100) and restarts
    print 
    print 'New Game:','the secret number is between 0 and 100'
    global guess_times
    guess_times = 7
    print 'You have',guess_times,'times to guess'
    global secret_number
    secret_number = random.randrange(0,100)

def range1000():
    # button that changes range to range [0,1000) and restarts
    print
    print 'New Game:','the secret number is between 0 and 1000'
    global guess_times
    guess_times = 10
    print 'You have',guess_times,'times to guess'
    global secret_number
    secret_number = random.randrange(0,1000)
    
def input_guess(guess):
    # main game logic goes here	
    global guess_times
    guess = int(guess)
    print 
    print "Your guess is", guess
    guess_times = guess_times-1
    if(guess>secret_number):
        print 'Lower!'
        print guess_times,'times left'
    elif(guess<secret_number):
        print 'Higher!'
        print guess_times,'times left'
    else:
        print 'Correct!'
        print 'The secrect number is',secret_number
        new_game()
    if(guess_times == 0):
        print 'The secrect number is',secret_number
        new_game()
        return

    
# create frame
frame = simplegui.create_frame("Guess the number", 300, 200)

frame.add_button("Range: 0 - 100", range100)
frame.add_button("Range: 0 - 1000", range1000)
inp = frame.add_input('Guess Number', input_guess, 50)
# register event handlers for control elements



# call new_game and start frame
frame.start()
new_game()

# always remember to check your completed program against the grading rubric

