# Implementation of classic arcade game Pong

import simplegui
import random

# initialize globals - pos and vel encode vertical info for paddles
WIDTH = 600
HEIGHT = 400       
BALL_RADIUS = 20
PAD_WIDTH = 8
PAD_HEIGHT = 80
HALF_PAD_WIDTH = PAD_WIDTH / 2
HALF_PAD_HEIGHT = PAD_HEIGHT / 2
LEFT = False
RIGHT = True
ball_pos = [300,150]
ball_vel = [0,0]
paddle1_vel = 0
paddle2_vel = 0
score1 = 0
score2 = 0
direction = LEFT
paddle1_pos = [0,0]
paddle2_pos = [600-PAD_WIDTH,0]
# initialize ball_pos and ball_vel for new bal in middle of table
# if direction is RIGHT, the ball's velocity is upper right, else upper left
def spawn_ball(direction):
    global ball_pos, ball_vel # these are vectors stored as lists
    ball_pos = [300,150]
    a = (random.random()+10)/11
    if direction:
        ball_vel = [-2*a,-a]
    else:
        ball_vel = [2*a,-a]

# define event handlers
def new_game():
    global paddle1_pos, paddle2_pos, paddle1_vel, paddle2_vel  # these are numbers

    global score1, score2  # these are ints
    global direction
    direction = not direction
    spawn_ball(direction)

def draw(c):
    global score1, score2, paddle1_pos, paddle2_pos, ball_pos, ball_vel
 
        
    # draw mid line and gutters
    c.draw_line([WIDTH / 2, 0],[WIDTH / 2, HEIGHT], 1, "White")
    c.draw_line([PAD_WIDTH, 0],[PAD_WIDTH, HEIGHT], 1, "White")
    c.draw_line([WIDTH - PAD_WIDTH, 0],[WIDTH - PAD_WIDTH, HEIGHT], 1, "White")
        
    # update ball
    if(ball_pos[1]<=BALL_RADIUS):
        ball_vel[1] = -ball_vel[1]
    elif(ball_pos[1]>=HEIGHT- BALL_RADIUS):
        ball_vel[1] =  -ball_vel[1]
        
    if(ball_pos[0]-BALL_RADIUS<PAD_WIDTH):
        if(paddle1_pos[1]<ball_pos[1]<paddle1_pos[1]+PAD_HEIGHT):
            ball_vel[0] = -ball_vel[0]
        else:
            global score2
            score2 += 1
            new_game()
            
             
    if(ball_pos[0]+BALL_RADIUS>WIDTH-PAD_WIDTH):
        if(paddle2_pos[1]<ball_pos[1]<paddle2_pos[1]+PAD_HEIGHT):
            ball_vel[0] = -ball_vel[0]
        else:
            global score1
            score1 += 1
            new_game()       
            
    ball_pos[0] = ball_pos[0] + ball_vel[0]
    ball_pos[1] = ball_pos[1] + ball_vel[1]  
    ball_vel[0] *= 1.001
    ball_vel[1] *= 1.001
    
    # draw ball
    c.draw_circle(ball_pos, BALL_RADIUS, 1, 'White','White')
    # update paddle's vertical position, keep paddle on the screen
    global paddle1_vel
    global paddle2_vel

    if(paddle1_pos[1]==0 and paddle1_vel<=-1):
        paddle1_vel = 0
    if(paddle1_pos[1]==HEIGHT-PAD_HEIGHT and paddle1_vel>=1):
        paddle1_vel = 0
    if(paddle2_pos[1]==HEIGHT-PAD_HEIGHT and paddle2_vel>=1):
        paddle2_vel = 0
    if(paddle2_pos[1]==0 and paddle2_vel<=-1):
        paddle2_vel = 0

    paddle1_pos[1] += paddle1_vel 
    paddle2_pos[1] += paddle2_vel

    # draw paddles
    c.draw_polygon([paddle1_pos, [paddle1_pos[0]+PAD_WIDTH,paddle1_pos[1]],
                    [paddle1_pos[0]+PAD_WIDTH, paddle1_pos[1]+PAD_HEIGHT],
                    [paddle1_pos[0], paddle1_pos[1]+PAD_HEIGHT],], 1, 'White','White')
    c.draw_polygon([paddle2_pos, [paddle2_pos[0]+PAD_WIDTH,paddle2_pos[1]],
                    [paddle2_pos[0]+PAD_WIDTH, paddle2_pos[1]+PAD_HEIGHT],
                    [paddle2_pos[0], paddle2_pos[1]+PAD_HEIGHT],], 1, 'White','White')

    
    # draw scores
    c.draw_text(str(score1), (175, 70), 50, 'White')
    c.draw_text(str(score2), (400, 70), 50, 'White')  
    
def keydown(key):
    global paddle1_vel, paddle2_vel
    if key == simplegui.KEY_MAP['s']:
        paddle1_vel += 2
    elif key == simplegui.KEY_MAP['w']:
        paddle1_vel -= 2
    elif key == simplegui.KEY_MAP['down']:
        paddle2_vel += 2
    elif key == simplegui.KEY_MAP['up']:
        paddle2_vel -= 2   
   
def keyup(key):
    global paddle1_vel, paddle2_vel
    paddle1_vel = 0
    paddle2_vel = 0
def reset():
    global score2
    score2 =0
    global score1
    score1 =0 
    new_game()


# create frame
frame = simplegui.create_frame("Pong", WIDTH, HEIGHT)
frame.set_draw_handler(draw)
frame.set_keydown_handler(keydown)
frame.set_keyup_handler(keyup)
frame.add_button('Reset', reset)

# start frame
new_game()
frame.start()
