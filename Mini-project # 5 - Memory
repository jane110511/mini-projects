# implementation of card game - Memory

import simplegui
import random
canvas_width = 800
canvas_height = 100
card_width = canvas_width / 16
numbers = range(8)+range(8)
positions = []
state = 0
click_times = 0
turns = 0
exposed = [False,False,False,False,False,False,False,False,False,False,False,False,False,False,False,False]

# helper function to initialize globals
def new_game():
    random.shuffle(numbers)  
    global positions,state,click_times,exposed,turns
    positions = []
    state = 0
    click_times = 0
    turns = 0
    label.set_text("Turns = "+str(turns))
    exposed = [False,False,False,False,False,False,False,False,False,False,False,False,False,False,False,False]
# define event handlers
def mouseclick(pos):
    position = pos[0]/card_width
    if(not exposed[position]):
        global click_times
        positions.append(position)
        click_times += 1
        exposed[position] = True
        global state
        if state == 0:
            state = 1
        elif state == 1:
            state = 2
            global turns
            turns += 1   
            label.set_text("Turns = "+str(turns))
        else:
            state = 1
            if(numbers[int(positions[click_times-3])] == numbers[int(positions[click_times-2])]):
                exposed[int(positions[click_times-2])] = True
                exposed[int(positions[click_times-3])] = True
            else:
                exposed[int(positions[click_times-2])] = False
                exposed[int(positions[click_times-3])] = False


    print 'click times', click_times        
    print 'state',state
    print 'position',position
    print 'numbers',numbers
    print 'exposed',exposed
    print 'pos',positions
                        
# cards are logically 50x100 pixels in size    
def draw(canvas):
    canvas.draw_line([canvas_width, 0], [canvas_width, canvas_height], 1, "White")
    canvas.draw_line([0, 0], [canvas_width, 0], 1, "White")
    canvas.draw_line([0, canvas_height], [canvas_width, canvas_height], 1, "White")
    for i in range(0,16):
        canvas.draw_line([card_width*i, 0], [card_width*i, canvas_height], 1, "White")
        if(exposed[i]):
            canvas.draw_text(str(numbers[i]), [card_width*i+5, 80], 80, "White")
        else:
            canvas.draw_polygon([[card_width*i, 0], [card_width*i, canvas_height], [card_width*(i+1), canvas_height], [card_width*(i+1), 0]], 1, 'White', 'Green')


# create frame and add a button and labels
frame = simplegui.create_frame("Memory", 800, 100)
frame.add_button("Restart", new_game)
label = frame.add_label("Turns = 0")

# register event handlers
frame.set_mouseclick_handler(mouseclick)
frame.set_draw_handler(draw)

# get things rolling
new_game()
frame.start()


# Always remember to review the grading rubric
