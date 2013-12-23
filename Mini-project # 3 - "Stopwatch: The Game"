import simplegui
# template for "Stopwatch: The Game"

# define global variables
time = 0;
success_times = 0;
try_times = 0
# define helper function format that converts time
# in tenths of seconds into formatted string A:BC.D
#format(11) = 0:01.1
def format(t):
    d = t%10;
    second = t/10%60;
    if(second>9):
        b=second/10
        c=second%10
    else:
        b=0
        c=second
    a = t/600;
    return str(a)+":"+str(b)+str(c)+"."+str(d)
    
# define event handlers for buttons; "Start", "Stop", "Reset"


# define event handler for timer with 0.1 sec interval
def timer_handler():
    global time
    time = time+1
    return time

# define draw handler

    
# create frame


# register event handlers
def start():
    timer.start()
    return

def stop():
    if(timer.is_running()):
        timer.stop()
        global try_times
        try_times = try_times + 1
        if(time%50==0):
            global success_times
            success_times = success_times + 1
    
    return

def reset():
    global time
    time = 0
    global success_times
    success_times = 0
    global try_times
    try_times = 0
    timer.stop()
    return

def draw(canvas):
    times = str(success_times)+'/'+str(try_times);
    canvas.draw_text(times, [250,25], 25, "Green")
    canvas.draw_text(format(time), [80,112], 50, "White")

    
# start frame
frame = simplegui.create_frame("Home", 300, 200)
frame.add_button("Start", start)
frame.add_button("Stop", stop)
frame.add_button("Reset", reset)
frame.set_draw_handler(draw)


timer = simplegui.create_timer(100, timer_handler)


# Start the frame animation
frame.start()
timer.start()

# Please remember to review the grading rubric
