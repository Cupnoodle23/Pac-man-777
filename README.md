add_library('sound')
import random
boardTiles = [
    [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0],
    [0, 1, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0],
    [0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0],
    [0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 0, 0],
    [0, 1, 1, 1, 1, 0, 1, 1, 0, 1, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0],
    [0, 1, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0],
    [0, 1, 0, 0, 1, 0, 1, 1, 1, 1, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0],
    [0, 1, 1, 1, 1, 1, 1, 0, 0, 0, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0],
    [0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 1, 0, 1, 0, 0, 1, 0, 0, 0, 0],
    [0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 0, 0],
    [0, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0],
    [0, 1, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0],
    [0, 1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 0, 0, 0, 0],
    [0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 0],
    [0, 1, 1, 1, 1, 0, 1, 1, 0, 1, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0],
    [0, 1, 0, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0],
    [0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
]

import time
#This function will get the position of the cherries, five-point squares as well as power cubes
def square_power_cherry(d,begin):
    squares=[]
    cherries=[]
    power_cubes=[]
    #The two for loops go through each value from row to row in the array boardTiles
    for i in range(len(boardTiles)):
        for x in range(len(boardTiles[i])):
            fill(200,189.8,170.6)
            #If the current value that is being gone through is one then enter the if loop
            if boardTiles[i][x] == 1:
                #Append the position of a five-point square on the screen into the array squares 
                squares.append((begin[0]-5,begin[1]-5))
                #If the 1 value is at the corner of the array boardTiles then append the on-screen position to power cube
                if ((i == 1 and x == 1) or (i == 1 and x == len(boardTiles[i])-5)) or ((i == len(boardTiles)-3 and x == 1) or (i == len(boardTiles)-3 and x == len(boardTiles[i])-5)):
                    fill(0,365,0)
                    power_cubes.append((begin[0]-5,begin[1]-5))
                #If a randomly generated number from 1 to 20 is 1 then a cherry is generated at this point and its on screen position is appended to cherries
                if random.randint(1,20) == 1 and (begin[0]-5,begin[1]-5) not in power_cubes:
                    # fill(0,0,365)
                    cherries.append((begin[0]-5,begin[1]-5))
                    image(cherry,begin[0]-5,begin[1]-5,10,10)
                else:
                    square(begin[0]-5,start[1]-5,10)
            #Go to the value on the right
            begin[0]=begin[0]+d
        #Go to the line bellow
        begin[1]=begin[1]+d
        #Go to the beginning of the line
        begin[0]=200
    return squares, cherries,power_cubes

#This function will find the positions that pacman will be able to travel on
def path_coordinates(d,begin):
    path=[]
    #This for loop goes through all the values in the array boardTiles. If the value is one and the value to the right is one, then append all the on screen coordinates beteen the two points to path. The same goes if there is also a 1 bellow.
    for i in range(len(boardTiles)):
        for x in range(len(boardTiles[i])):
            if x < len(boardTiles[i]) - 1 and boardTiles[i][x] == 1:
                if boardTiles[i][x+1] == 1:
                    for y in range(begin[0],begin[0]+d+5,1):
                        path.append((y,begin[1]))
                    # count+=1
            if i < len(boardTiles) - 1 and boardTiles[i][x] == 1:
                if boardTiles[i+1][x] == 1:
                    for y in range(begin[1],begin[1]+d+5,1):
                        path.append((begin[0],y))
            begin[0]=begin[0]+d
        begin[1]=begin[1]+d
        begin[0]=200
    return path

def setup():
    global ghost1, sf, path, squares, cherries, power_cubes,start, vulnerable_ghost,cherry
    cherry=loadImage('cherry.png')
    # time.sleep(3)
    start=[200,200]
    size(900,2000)
    #This is the on-screen distance between each value in the array tableLength.
    distance_between_each_point=30
    # distance_between_each_point=(height-400)//len(boardTiles)
    # print((height-400)//len(boardTiles))
    # print((width-400)//len(boardTiles[0]))
    # fill(0,0,355)
    frameRate(50)
    rect(200,200,480,540)
    #This for loop is supposed to draw the game board.
    for i in range(len(boardTiles)):
        for x in range(len(boardTiles[i])):
            #If the current value is one
            if boardTiles[i][x] == 1:
                if x+1 < len(boardTiles[i]):
                    #If the value to the right has a value of 1 then by drawing multiple lines between the current value and the right value create a thick bar
                    if boardTiles[i][x+1] == 1:
                        for p in range(start[1]-9,start[1]+10,1):
                            line(start[0],p,start[0]+30,p)
                        # line(start[0],start[1],start[0]+30,start[1])
                if i+1 < len(boardTiles):
                    #If the value bellow is one then draw multiple lines between the current one and the one bellow to form a thick bar
                    if boardTiles[i+1][x] == 1:
                        for p in range(start[0]-9,start[0]+10,1):
                            line(p,start[1],p,start[1]+30)
                        # line(start[0],start[1],start[0],start[1]+30)
            #Go to the next value on the right
            start[0]=start[0]+30
        #Go the line bellow    
        start[1]=start[1]+30
        #Go to the start of the line
        start[0]=200
    fill(200,189.8,170.6)
    start=[200,200]
    #Get the positions of cherries, five-point squares and power cubes
    items_generated=square_power_cherry(distance_between_each_point,start)
    squares=items_generated[0]
    cherries=items_generated[1]
    power_cubes=items_generated[2]
    ghost1=loadImage("ghost1.png")
    vulnerable_ghost=loadImage("vulnerable_ghost.png")
    start=[200,200]
    count=0
    #Get the path pacman can go on
    path=path_coordinates(distance_between_each_point,start)
    sf=SoundFile(this,'Pac-Man-Theme-Song.mp3')
    sf.play()
    
"""resume"""
#x position of pacman
x_co=440
#y position of pacman
y_co=590
add_x=0
add_y=0
#position of red ghost
red_ghost_pos=[440,450]
#ammount of time red ghost stays in spawn
red_timer=150
#keeps track of each frame
count=3
sub_count=1
red_in_line=True
add_on=(0,0)
score=0
life_gone=False
red_x_speed=1
red_y_speed=1
power_time=0
speed=5
chosen=False
#Whether the use has selected a difficulty
mode=None
#Whether the user has decided to play again or not
decision=False
def draw():
    global red_captured,speed,x_co,y_co, add_x, add_y, count, red_in_line,add_on, sub_count,red_timer, score, life_gone, red_x_speed, red_y_speed, power_time,red_ghost_pos, chosen, mode, decision
    # image(ghost1,500,500,20,20)
    #If pacman has not been killed and there are stillm objects on the board
    if life_gone == False and squares != [] and chosen == True:
        #If the user presses an arrow key then the lines up to 189 will check whether pacman can move to that direction and if so then pacman is moved there.
        if keyCode == UP:
            if (x_co,y_co - 5) in path:
                add_y=-5
                add_x=0
                # y_co-=5
        if keyCode == DOWN:
            if (x_co, y_co + 5) in path:
                # y_co+=5
                add_y=5
                add_x=0
        if keyCode == LEFT:
            if (x_co - 5,y_co) in path:
                add_x=-5
                add_y=0
                # x_co-=5
        if keyCode == RIGHT:
            if (x_co+5,y_co) in path:
                # x_co+=5
                add_x=5
                add_y=0
        if (x_co+add_x,y_co+add_y) in path:
            x_co+=add_x
            y_co+=add_y
        fill(255,255,0)
        if (x_co-5,y_co-5) in squares:
            squares.remove((x_co-5,y_co-5))
            if (x_co-5,y_co-5) in cherries:
                score+=30
            elif (x_co-5,y_co-5) in power_cubes:
                if mode != 'Normal':
                    power_time=50
                else:
                    power_time=100
                red_captured=False
                yellow_captured=False
                blue_captured=False
                pink_captured=False
            else:
                score+=5
        #Draw pacman
        arc(x_co, y_co, 20, 20, 0.2, PI+QUARTER_PI, PIE);
        # arc(x_co, y_co, 20, 20, 0.2, TWO_PI - 0.2, PIE)
        background(128,128,128)
        fill(255,255,255)
        # square(200,200,600)
        rect(200,200,480,540)
        #This is the same code as lines 90-111 and it is used to draw the board
        start=[200,200]
        for i in range(len(boardTiles)):
            for x in range(len(boardTiles[i])):
                if boardTiles[i][x] == 1:
                    if x+1 < len(boardTiles[i]):
                        if boardTiles[i][x+1] == 1:
                            for p in range(start[1]-9,start[1]+10,1):
                                line(start[0],p,start[0]+30,p)
                            # line(start[0],start[1],start[0]+30,start[1])
                    if i+1 < len(boardTiles):
                        if boardTiles[i+1][x] == 1:
                            for p in range(start[0]-9,start[0]+10,1):
                                line(p,start[1],p,start[1]+30)
                            # line(start[0],start[1],start[0],start[1]+30)
                start[0]=start[0]+30
            start[1]=start[1]+30
            start[0]=200
        #line 228 to 234 goes through the array containing the position of the squares, cherries and power cubes and draws them onto the screen
        for i in squares:
            fill(200,189.8,170.6)
            if i in cherries:
                image(cherry,i[0],i[1],10,10)
            elif i in power_cubes:
                fill(0,365,0)
                square(i[0],i[1],10)
            else:
                square(i[0],i[1],10)
        fill(255,255,0)
        arc(x_co, y_co, 20, 20, 0.2, TWO_PI - 0.2, PIE)
        # text(str(power_time),100,100)
        right=(red_ghost_pos[0]+speed,red_ghost_pos[1])
        left=(red_ghost_pos[0]-speed,red_ghost_pos[1])
        up=(red_ghost_pos[0],red_ghost_pos[1]-speed)
        down=(red_ghost_pos[0],red_ghost_pos[1]+speed)
        coordinates=[]
        directions=[]
        textSize(50)
        fill(255,192,203)
        text('Score: '+str(score),350,100)
        red_timer-=1
        #If there is no power cube effect present then make sure that it is declared that by no means can the ghost be vulnerable
        if power_time <= 0:
            red_captured=False
        #Once it is time for the ghost to leave spawn then once it has reached the middle point of spawn make it move down until it reaches the path
        if red_timer <= 0 and (red_ghost_pos[0],red_ghost_pos[1]) not in path and red_ghost_pos[0] == 440:
            red_ghost_pos[1]+=2
        #If the ghost is in spawn and it is not yet time for it to leave then it will keep colliding against surrounding walls
        elif (red_ghost_pos[0],red_ghost_pos[1]) not in path:
            if red_ghost_pos[0] + red_x_speed >= 486 or red_ghost_pos[0] + red_x_speed <= 393:
                red_x_speed*=-1
            if red_ghost_pos[1] + red_y_speed <= 423 or red_ghost_pos[1] + red_y_speed >= 457:
                red_y_speed*=-1
            red_ghost_pos[0]+=red_x_speed
            red_ghost_pos[1]+=red_y_speed
            # print(red_ghost_pos)
        #If the ghost is in hunting mode due to their being no power effect or the ghost has already been captured during power effect
        elif power_time <= 0 or red_captured == True:
            if mode == 'Normal':
                speed=5
            else:
                speed=10
            #If ghost is about to exit the path then enter if loop
            if (red_ghost_pos[0]+add_on[0], red_ghost_pos[1]+add_on[1]) not in path:
                red_in_line=True
            not_two_in_a_row=False
            #If this is an odd frame(so every two frames)
            if count % 2 == 1:
                not_two_in_a_row=True
            if red_in_line == True and not_two_in_a_row == True:
                # print(1)
                #The lines up to 285 find all the possible ghost directions
                if right in path:
                    coordinates.append(right)
                    directions.append((speed,0))
                if left in path:
                    coordinates.append(left)
                    directions.append((-1*speed,0))
                if up in path:
                    coordinates.append(up)
                    directions.append((0,-1*speed))
                if down in path:
                    coordinates.append(down)
                    directions.append((0,speed))
                #The direction which is closest to pacman is found
                min_distance=999999999
                closest_coordinate=0
                for i in range(len(coordinates)):
                    x1=coordinates[i][0]
                    y1=coordinates[i][1]
                    x2=x_co
                    y2=y_co
                    distance=((y2-y1)**2+(x2-x1)**2)**0.5
                    if distance < min_distance:
                        min_distance=distance
                        closest_coordinate=coordinates[i]
                        add_on=directions[i]
                red_in_line=False
            else:
                ghost_pacman_distance=((red_ghost_pos[1]-y_co)**2+(red_ghost_pos[0]-x_co)**2)**0.5
                #If pacman is going left or right
                if add_on[1]  == 0:
                    top=(red_ghost_pos[0],red_ghost_pos[1]-speed)
                    bottom=(red_ghost_pos[0],red_ghost_pos[1]+speed)
                    #If pacman can move up or down then find whether it is best to move up or down
                    if top in path or bottom in path:
                        top_distance=0
                        bottom_distance=0
                        if top in path:
                            top_distance=((top[1]-y_co)**2+(x_co-x_co)**2)**0.5
                        if bottom in path:
                            bottom_distance=((bottom[1]-y_co)**2+(x_co-x_co)**2)**0.5
                        if top_distance < bottom_distance:
                            if top_distance <= ghost_pacman_distance:
                                add_on=(0,-1*speed)
                                red_in_line+=True

                        else:
                            if bottom_distance <= ghost_pacman_distance:
                                add_on=(0,speed)
                                red_in_line=True
                #If pacman is going up or down
                elif not_two_in_a_row == True:
                    left=(red_ghost_pos[0]-speed,red_ghost_pos[1])
                    right=(red_ghost_pos[0]+speed,red_ghost_pos[1])
                    #If pacman can go left or right find whether it is best to move up or down
                    if left in path or right in path:
                        left_distance=0
                        right_distance=0
                        if left in path:
                            left_distance=((y_co-y_co)**2+(left[0]-x_co)**2)**0.5
                        if right in path:
                            right_distance=((y_co-y_co)**2+(right[0]-x_co)**2)**0.5
                        if left_distance < right_distance:
                            if left_distance <= ghost_pacman_distance:
                                add_on=(-1*speed,0)
                                red_in_line=True
                        else:
                            if right_distance <= ghost_pacman_distance:
                                add_on=(speed,0)
                                red_in_line=True
            if (red_ghost_pos[0]+add_on[0],red_ghost_pos[1]+add_on[1]) in path:
                red_ghost_pos[0]+=add_on[0]
                red_ghost_pos[1]+=add_on[1]
        #This else statement is basically the same as the elif one above. It is used for when the ghost is running away and makes the ghost move the opposite direction to the best direction
        else:
            if mode != 'Normal':
                speed=5
            else:
                speed=1
            if (red_ghost_pos[0]+add_on[0], red_ghost_pos[1]+add_on[1]) not in path:
                red_in_line=True
            not_two_in_a_row=False
            if count % 2 == 1:
                not_two_in_a_row=True
            if red_in_line == True and not_two_in_a_row == True:
                # print(1)
                if right in path:
                    coordinates.append(right)
                    directions.append((speed,0))
                if left in path:
                    coordinates.append(left)
                    directions.append((-1*speed,0))
                if up in path:
                    coordinates.append(up)
                    directions.append((0,-1*speed))
                if down in path:
                    coordinates.append(down)
                    directions.append((0,speed))
                max_distance=-1
                furthest_coordinate=0
                for i in range(len(coordinates)):
                    x1=coordinates[i][0]
                    y1=coordinates[i][1]
                    x2=x_co
                    y2=y_co
                    distance=((y2-y1)**2+(x2-x1)**2)**0.5
                    if distance > max_distance:
                        max_distance=distance
                        furthest_coordinate=coordinates[i]
                        add_on=directions[i]
                red_in_line=False
            else:
                ghost_pacman_distance=((red_ghost_pos[1]-y_co)**2+(red_ghost_pos[0]-x_co)**2)**0.5
                if add_on[1]  == 0:
                    top=(red_ghost_pos[0],red_ghost_pos[1]-speed)
                    bottom=(red_ghost_pos[0],red_ghost_pos[1]+speed)
                    if top in path or bottom in path:
                        top_distance=0
                        bottom_distance=0
                        if top in path:
                            top_distance=((top[1]-y_co)**2+(x_co-x_co)**2)**0.5
                        if bottom in path:
                            bottom_distance=((bottom[1]-y_co)**2+(x_co-x_co)**2)**0.5
                        if top_distance > bottom_distance:
                            if top_distance >= ghost_pacman_distance:
                                add_on=(0,-1*speed)
                                red_in_line+=True
                        else:
                            if bottom_distance >= ghost_pacman_distance:
                                add_on=(0,speed)
                                red_in_line=True
                elif not_two_in_a_row == True:
                    left=(red_ghost_pos[0]-speed,red_ghost_pos[1])
                    right=(red_ghost_pos[0]+speed,red_ghost_pos[1])
                    if left in path or right in path:
                        left_distance=0
                        right_distance=0
                        if left in path:
                            left_distance=((y_co-y_co)**2+(left[0]-x_co)**2)**0.5
                        if right in path:
                            right_distance=((y_co-y_co)**2+(right[0]-x_co)**2)**0.5
                        if left_distance > right_distance:
                            if left_distance >= ghost_pacman_distance:
                                add_on=(-1*speed,0)
                                red_in_line=True
                        else:
                            if right_distance >= ghost_pacman_distance:
                                add_on=(speed,0)
                                red_in_line=True
            if (red_ghost_pos[0]+add_on[0],red_ghost_pos[1]+add_on[1]) in path:
                red_ghost_pos[0]+=add_on[0]
                red_ghost_pos[1]+=add_on[1]
        left_right=x_co-red_ghost_pos[0]
        up_down=y_co-red_ghost_pos[1]
        count+=1
        sub_count+=1
        #If the ghost has not been captured and it is not power time
        if power_time <= 0 or red_captured == True:
            image(ghost1,red_ghost_pos[0]-5,red_ghost_pos[1]-5,25,17)
        #If the ghost is being hunted during power time make it look vulnerable
        else:
            image(vulnerable_ghost,red_ghost_pos[0]-5,red_ghost_pos[1]-5,15,17)
        #If the ghost is on of pacman
        if abs(red_ghost_pos[1]-y_co) < 7 and abs(red_ghost_pos[0]-x_co) < 7:
            #If it is not special power time
            if power_time > 0 and red_captured == True or power_time <= 0:
                life_gone=True
            #If it is special power time
            else:
                red_timer=150
                red_ghost_pos=[440,450]
                red_captured=True
                score+=100
        power_time-=1
    #If the user has either died or beaten the game
    elif chosen == True:
        #display the score and whether you have won or lost and let the user decide whether he wants to play again
        background(255,255,255)
        fill(1)
        if life_gone == True:
            if squares != []:
                text('You lose',330,400)
            else:
                text('You win',330,400)
            text('Score: '+str(score),310,500)
            text('Play again?(y/n)',330,600)
        else:
            text('You win',330,400)
            text('Score: '+str(score),315,500)
            text('Play again?(y/n)',330,600)
            life_gone=True
        if decision == True:
            sf.stop()
            background(211,211,211)
            fill(365,365,365)
            setup()
            #x position of pacman
            x_co=440
            #y position of pacman
            y_co=590
            add_x=0
            add_y=0
            #position of red ghost
            red_ghost_pos=[440,450]
            #ammount of time red ghost stays in spawn
            red_timer=150
            #keeps track of each frame
            count=3
            sub_count=1
            red_in_line=True
            add_on=(0,0)
            score=0
            life_gone=False
            red_x_speed=1
            red_y_speed=1
            power_time=0
            speed=5
            chosen=False
            mode=None
            decision=False
            # noLoop()
    else:
        textSize(30)
        distanceNorm=((mouseY-150)**2+(mouseX-330)**2)**0.5
        distanceHard=((mouseY-150)**2+(mouseX-560)**2)**0.5
        text('Pacman vs Blinky',320,100)
        if distanceNorm < 50:
            fill(365,0,0)
        text('Normal',280,150)
        fill(0,365,0)
        if distanceHard < 40:
            fill(365,0,0)
        text('Hard',525,150)
        fill(0,365,0)
#when the mouse is pressed
def mousePressed():
    global chosen, mode, decision
    #If the left mouse button is clicked then see if the cursor is on a level button if so chosen becomes true
    if mouseButton == LEFT and chosen == False:
        distanceNorm=((mouseY-150)**2+(mouseX-330)**2)**0.5
        distanceHard=((mouseY-150)**2+(mouseX-560)**2)**0.5
        if distanceNorm < 50:
            chosen=True
            mode='Normal'
        elif distanceHard < 40:
            chosen=True
            mode='Hard'
#When a key is pressed
def keyPressed():
    global decision
    #If y has been pressed then the game then you are brought back to the menu if it is n then the game ends
    if key == 'y' and life_gone == True:
        decision=True
    elif key == 'n':
        decision=None

