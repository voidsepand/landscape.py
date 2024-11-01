import pygame 
import random
pygame.init()


WIDTH = 640
HEIGHT = 480
SIZE = (WIDTH, HEIGHT)
moon_raduis = 30
moon_x = 0
moon_y = HEIGHT//2
moon_speed = 2 
screen = pygame.display.set_mode(SIZE) # setting the display at normal speed for evryone so that it displays  it the same
clock = pygame.time.Clock()
fps = 60
count = 0
# ---------------------------



#create the locations of the stars for when we animate the background

ice_field_fast = []





for fast_stars in range(35):
    star_loc_x = random.randrange(0, WIDTH)
    star_loc_y = random.randrange(0, HEIGHT)
    ice_field_fast.append([star_loc_x, star_loc_y])



running = True
while running:
    # EVENT HANDLING(ex for if someone presses any key on the keyboard)
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False 

    # GAME STATE UPDATES(mostly for answeing to the #event handeling ) 
    # All game math and comparisons happen here

    moon_x += moon_speed
    if moon_x > WIDTH + moon_raduis:
        moon_x -= moon_raduis
    # DRAWING(the final is drawing the player)
    screen.fill((0,0,0))  # always the first drawing command

     
    pygame.draw.circle(screen, (246, 241, 213), (0,0), 50) # the moon 
    pygame.draw.rect(screen,(211, 187, 159), (220, 240, 200, 200)) # the house 
    pygame.draw.rect(screen,(183,177,174), (1, 375, 640, 117)) # the pavment  
    pygame.draw.polygon(screen,(255,165,0) , ((220, 240), (320, 160), (420, 240)))# the roof

# making compound shapes (aka adding windows )
    window_width, window_height = 35, 35
    left_window = pygame.Rect(250, 280, window_width, window_height)  # Left window
    right_window = pygame.Rect(340, 280, window_width, window_height)  # Right window


    pygame.draw.rect(screen, (0,0,0), left_window)  
    pygame.draw.rect(screen, (0,0,0) , right_window) 



# pumkins 

    pumpkin1_outer = pygame.Rect(100, 323, 80, 50)  # Left pumpkin outer ellipse
    pumpkin1_inner = pygame.Rect(110, 333, 50, 30)  # Left pumpkin inner ellipse

    pumpkin2_outer = pygame.Rect(480, 333, 80, 50)  # Right pumpkin outer ellipse
    pumpkin2_inner = pygame.Rect(492, 340, 50, 30)  # Right pumpkin inner ellipse


    pygame.draw.ellipse(screen, (255, 165, 0), pumpkin1_outer)  # Outer
    pygame.draw.ellipse(screen, (255,140,0), pumpkin1_inner)  # Inner

    # Draw the right pumpkin
    pygame.draw.ellipse(screen, (255,140,0), pumpkin2_outer)  # Outer
    pygame.draw.ellipse(screen, (204,85,0), pumpkin2_inner)


    # adding a door 

    door_width = 25 
    door_height = 55
    door = (300, 317, door_width , door_height)
    pygame.draw.rect(screen, (139,70,20), (door))

    for star in ice_field_fast:
        star[1] += 3
        if star[1] > HEIGHT:
            star[0] = random.randrange(0, WIDTH)
            star[1] = random.randrange(-20, -5)
        pygame.draw.circle(screen, (255,255,255), star, 1)

    # adding a pile of snow 
    count += 1
    pygame.draw.rect(screen,(255,255,255),(1, 375, 640, count//100))

    # Must be the last two lines
    # of the game loop
    pygame.display.flip()
    clock.tick(fps)
    #---------------------------


pygame.quit()
