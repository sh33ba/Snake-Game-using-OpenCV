# **Classical Snake Game using OpenCV** 
---
---
**Requirements**
* Python3.5
* Opencv-Python
---
---
### Defining Functions
1. for collision of snake with boundary
2. for collision of snake with itself
3. for collision of snake with apple

'''Python
#function for boundary collision of snake
def boundary_collision(snake_h):    
    if snake_h[0]>=500 or snake_h[0]<0 or snake_h[1]>=500 or snake_h[1]<0:
        return 1
    else:
        return 0
    
#function for self collision of snake
def self_collision(snake_pos):
    snake_h=snake_pos[0]
    if snake_h in snake_pos[1:]:
        return 1
    else:
        return 0

#function for collision of snake with apple
def apple_collision(apple_pos,score):
    apple_pos=[random.randrange(1,50)*10,random.randrange(1,50)*10]
    score+=1
        
    return apple_pos,score
'''
---
---
### Making Canvas and initialising variables
'''Python
img=np.zeros((500,500,3),dtype='uint8')
snake_pos=[[250,250],[240,250],[230,250]]
apple_pos=[random.randrange(1,50)*10,random.randrange(1,50)*10]

score=0
prev_button_direction=1
button_direction=1
snake_h=[250,250]
'''

### While loop where all actions take place 

1. Generating random position of apple
 
'''Python
#apple random position
    cv.rectangle(img,(apple_pos[0],apple_pos[1]),(apple_pos[0]+10,apple_pos[1]+10),(255,0,255),-1)

'''

2. Position of Snake
'''Python
 #position of snake
    for pos in snake_pos:
        cv.rectangle(img,(pos[0],pos[1]),(pos[0]+10,pos[1]+10),(0,255,0),-1)
'''

3. Using time
'''Python
 #using time to execute whole program until esc is pressed
    t_end = time.time() + 0.2
    k = -1
    while time.time() < t_end:
        if k == -1:
            k = cv.waitKey(125)
        else:
            continue
'''

4. Assigning Direction to Keys(Keyboard Keys)
'''Python
#left direction
    if k == ord('a') and prev_button_direction != 1:
        button_direction = 0
    
    #right direction
    if k==ord("d") and prev_button_direction != 0:
        button_direction = 1
        
    #up direction
    if k==ord("w") and prev_button_direction != 2:
        button_direction = 3
        
    ##down direction
    if k==ord("s") and prev_button_direction != 3:
        button_direction = 2
    
    #quit
    elif k == ord('q'):
        break
    else:
        button_direction = button_direction
'''

5. Making Snake move in pressed Direction
'''Python
 #move right
    if button_direction == 1:
        snake_h[0] += 10
    #move left
    elif button_direction == 0:
        snake_h[0] -= 10
    #move up
    elif button_direction == 2:
        snake_h[1] += 10
    #move down
    elif button_direction == 3:
        snake_h[1] -= 10
'''

6. Calling apple_collision()
'''Python
#calling apple_collision() 
    if snake_h == apple_pos:
        apple_pos,score = apple_collision(apple_pos,score)
        snake_pos.insert(0,list(snake_h))
        
    else:
        snake_pos.insert(0,list(snake_h))
        snake_pos.pop()
'''

7. Checking boundary_collision() and self_self_collision() and Displaying the result
'''Python
 if boundary_collision(snake_h) == 1 or self_collision(snake_pos) == 1:
        font = cv.FONT_HERSHEY_TRIPLEX
        img = np.zeros((500,500,3),dtype='uint8')
        #displays result according to number of successful eating of apple by snake
        cv.putText(img,'Your Score is {}'.format(score),(140,250), font, 1,(255,255,255),2,cv.LINE_AA)
        cv.imshow('test',img)
        cv.waitKey(0)
        
        break
'''
---
---
### Sample Images of above Code in running state

[image]: ./images_doc/01.jpg
---

[image]: ./images_doc/02.jpg
---

[image]: ./images_doc/03.jpg
---