from sense_hat import SenseHat
import time
import random

sense = SenseHat()

#declare color tuples
r = (255,0,0)
w = (255,255,255)
k = (0,0,0)

no_arrow = [
w,w,w,w,w,w,w,w,
w,w,w,w,w,w,w,w,
w,w,w,w,w,w,w,w,
w,w,w,w,w,w,w,w,
w,w,w,w,w,w,w,w,
w,w,w,w,w,w,w,w,
w,w,w,w,w,w,w,w,
w,w,w,w,w,w,w,w
]

left_arrow = [   
w,w,w,w,w,w,w,w,
w,w,r,w,w,w,w,w,
w,r,r,w,w,w,w,w,
r,r,r,r,r,r,r,w,
w,r,r,w,w,w,w,w,
w,w,r,w,w,w,w,w,
w,w,w,w,w,w,w,w,
w,w,w,w,w,w,w,w
]

right_arrow =[   
w,w,w,w,w,w,w,w,
w,w,w,w,w,r,w,w,
w,w,w,w,w,r,r,w,
w,r,r,r,r,r,r,r,
w,w,w,w,w,r,r,w,
w,w,w,w,w,r,w,w,
w,w,w,w,w,w,w,w,
w,w,w,w,w,w,w,w
]

down_arrow =[   
w,w,w,w,w,w,w,w,
w,w,w,r,w,w,w,w,
w,w,w,r,w,w,w,w,
w,w,w,r,w,w,w,w,
w,w,w,r,w,w,w,w,
w,r,r,r,r,r,w,w,
w,w,r,r,r,w,w,w,
w,w,w,r,w,w,w,w
]

up_arrow =[   
w,w,w,r,w,w,w,w,
w,w,r,r,r,w,w,w,
w,r,r,r,r,r,w,w,
w,w,w,r,w,w,w,w,
w,w,w,r,w,w,w,w,
w,w,w,r,w,w,w,w,
w,w,w,r,w,w,w,w,
w,w,w,r,w,w,w,w
]

 
# list of arrows
arrows = ["up", "right", "down", "left"]


# variable to hold level
level = 0

player_turn = False

player_pattern = []
current_pattern = []

def next_level():
    global player_turn, level, current_pattern, player_pattern
    
    # empty the lists
    player_pattern = []
    current_pattern = []
    
    sense.show_message(str(level))
    
    for i in range(level+2):
        current_pattern.append(random.choice(arrows))
        
    for arrow in current_pattern:
        if arrow == "up":
            sense.set_pixels(up_arrow)
        elif arrow == "right":
            sense.set_pixels(right_arrow)
        elif arrow == "down":
            sense.set_pixels(down_arrow)
        else:
            sense.set_pixels(left_arrow)
     
        time.sleep(0.5)
        sense.set_pixels(no_arrow)
        time.sleep(0.5)
    
    # add a level
    level = level + 1
    
    player_turn = True
    
def submit_guess():
    global player_pattern, current_pattern, player_turn
    
    if current_pattern == player_pattern:
        sense.show_message("LEVEL CLEAR", text_colour=r, back_colour=w, scroll_speed=.05)
        player_turn = False
    else:
        sense.show_message("Game Over")
        player_pattern = []

next_level()

while True:
    
    if player_turn:
        sense.show_letter("?")
        for event in sense.stick.get_events():
            print(event.direction, event.action)
            if event.action == "pressed" and event.direction != "middle":
                # store each event in player_pattern
                player_pattern.append(event.direction)
            if event.action == "released" and event.direction == "middle":
                print("current: " + str(current_pattern))
                print("player: " + str(player_pattern))
                submit_guess()
    else:
        next_level()
