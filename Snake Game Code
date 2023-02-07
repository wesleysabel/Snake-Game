# Snake-Game
import pygame
from pygame.locals import *
from random import randint

pygame.init()


# Generate random coordinates to apple
def pos_apple_random():
    x_apple = randint(0, 590)
    y_apple = randint(0, 590)
    return x_apple // 10 * 10, y_apple // 10 * 10


# collision snake in apple
def collision_apple(pos_snake, pos_apple):
    if pos_snake == pos_apple:
        return True


# collision snake in the tail
def collision_tail():
    global snake
    for tail in range(1, len(snake)):
        if snake[tail] == snake[0]:
            return True


# Music
# sound_collision = pygame.mixer.Sound('assets/sounds/collision_sound.wav')

# Config the window
height = 600
width = 600
size = (height, width)
window = pygame.display.set_mode(size)
pygame.display.set_caption('Snake Game')

# Directions
UP = 0
RIGHT = 1
LEFT = 2
DOWN = 3

# Snake
snake = [(300, 300), (310, 300), (320, 300)]
snake_body = pygame.Surface((10, 10))
snake_body.fill(color=(255, 255, 255))
snake_died = False
my_direction = LEFT
points = 0

# Apple
apple_pos = pos_apple_random()
apple = pygame.Surface((10, 10))
apple.fill(color=(255, 0, 0))

# Fps
fps = pygame.time.Clock()

# Switches for change direction
switch_up = True
switch_down = True
switch_left = True
switch_right = True

# Text
font = pygame.font.SysFont('Arial', 20, True)

gaming = True
game_pause = False

while gaming:

    if collision_tail():
        snake_died = True
        points = 0
        while snake_died:
            window.fill((255, 0, 0))
            snake = [(300, 300), (310, 300), (320, 300)]
            my_direction = LEFT
            message_game_over = "GAME OVER"
            message_game_restart = 'Press enter to return to game'
            formatted_text = font.render(message_game_over, True, (0, 0, 0))
            formatted_text2 = font.render(message_game_restart, True, (0, 0, 0))
            window.blit(formatted_text, (240, 200))
            window.blit(formatted_text2, (160, 300))

            for event in pygame.event.get():
                if event.type == QUIT:
                    pygame.quit()
                if event.type == KEYDOWN:
                    if event.key == K_RETURN:
                        snake_died = False
                        apple_pos = pos_apple_random()

            pygame.display.update()


    fps.tick(30)
    window.fill((0, 0, 0))

    if collision_apple(pos_snake=snake[0], pos_apple=apple_pos):
        apple_pos = pos_apple_random()
        points += 1
        # sound_collision.play()
        snake.append(apple_pos)

    message_points = f'Points: {points}'
    formatted_text = font.render(message_points, True, (0, 0, 255))
    window.blit(formatted_text, (260, 10) )

    for event in pygame.event.get():
        if event.type == QUIT:
            pygame.quit()
            exit()
        if event.type == KEYDOWN:
            if event.key == K_w or event.key == K_UP:
                if switch_up:
                    my_direction = UP
                    switch_down = False

                switch_left = True
                switch_right = True

            if event.key == K_s or event.key == K_DOWN:
                if switch_down:
                    my_direction = DOWN
                    switch_up = False

                switch_left = True
                switch_right = True

            if event.key == K_d or event.key == K_RIGHT:
                if switch_right:
                    my_direction = RIGHT
                    switch_left = False

                switch_up = True
                switch_down = True

            if event.key == K_a or event.key == K_LEFT:
                if switch_left:
                    my_direction = LEFT
                    switch_right = False

                switch_up = True
                switch_down = True
            
            if event.key == K_ESCAPE:
                game_pause = True
                
                while game_pause:

                    window.fill((255, 255, 255))
                    message_pause = 'The game has been paused. click ESC to return'
                    formatted_text = font.render(message_pause, True, (0, 0, 0))
                    window.blit(formatted_text, (70, 300))

                    for event in pygame.event.get():
                        if event.type == QUIT:
                            pygame.quit()
                        if event.type == KEYDOWN:
                            if event.key == K_ESCAPE:
                                game_pause = False
                            
                    pygame.display.update()


    for i in range(len(snake) - 1, 0, -1):
        snake[i] = (snake[i - 1][0], snake[i - 1][1])

    if my_direction == UP:
        snake[0] = (snake[0][0], snake[0][1] - 10)
    if my_direction == DOWN:
        snake[0] = (snake[0][0], snake[0][1] + 10)
    if my_direction == RIGHT:
        snake[0] = (snake[0][0] + 10, snake[0][1])
    if my_direction == LEFT:
        snake[0] = (snake[0][0] - 10, snake[0][1])


    for pos in snake:
        window.blit(snake_body, pos)
    window.blit(apple, apple_pos)

    if snake[0][0] > width:
        snake[0] = (0, snake[0][1])
    if snake[0][0] < 0:
        snake[0] = (width, snake[0][1])
    if snake[0][1] > height:
        snake[0] = (snake[0][0], 0)
    if snake[0][1] < 0:
        snake[0] = (snake[0][0], height)

    pygame.display.update()
