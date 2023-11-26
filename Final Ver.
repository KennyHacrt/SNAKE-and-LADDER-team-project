import pygame
import random
import os
import curses
import math
import time
L1 = [ 0, 144, 120, 72 ]
L2 = [ 0, 5, 6, 10 ]


Player1 = pygame.image.load("Player1.png")
Player2 = pygame.image.load("Player2.png")
Player3 = pygame.image.load("Player3.png")
Player4 = pygame.image.load("Player4.png")
Player5 = pygame.image.load("Player5.png")
dice1 = pygame.image.load("Dice1.png")
dice2 = pygame.image.load("Dice2.png")
dice3 = pygame.image.load("Dice3.png")
dice4 = pygame.image.load("Dice4.png")
dice5 = pygame.image.load("Dice5.png")
dice6 = pygame.image.load("Dice6.png")



def dice ():
    return random.randint(1,6)

def determine_player_no_valid ():
    while 1:
        try :
            player_numbers=int(input('How many players? : ')) 
        except:
            os.system('clear')
            print('error occurred,it should be integers 1-5')
        else:
            return player_numbers

def draw_the_board(mode,PLAYER_SYMBOLS_POS,snakes_ladder_store,PLAYER_NUMBER):
    a, b = pygame.Surface((L1[mode],L1[mode])), pygame.Surface((L1[mode],L1[mode]))
    font = pygame.font.Font(None, 30+30*(3-mode))
    red, green, blue = 64,255,255
    
    
    a.fill(( 233, 218, 0 ))
    b.fill(( 0, 169, 0 ))
    x, y = L2[mode]-1, 0
    for i in range(L2[mode]**2):

        if i % 2 == 0:
            screen.blit(a, (x * L1[mode], y * L1[mode]))
            pygame.display.update()
        else:
            screen.blit(b, (x * L1[mode], y * L1[mode]))
            pygame.display.update()
        text_surface = font.render(str( L2[mode]**2-i ), True, (0,0,0))
        screen.blit(text_surface,(x * L1[mode]+2, y * L1[mode]+2))
        if x == L2[mode]-1 and y % 2 == 1 or x == 0 and y % 2 == 0:
            y += 1
        elif y % 2 == 0:
            x -= 1
        else:
            x += 1

    
    for j in range(PLAYER_NUMBER):
        for i in snakes_ladder_store[2]:
            if PLAYER_SYMBOLS_POS[j+1] == i:
                PLAYER_SYMBOLS_POS.update({PLAYER_SYMBOLS_POS[j+1] : snakes_ladder_store[2][i]})
                break

    
    for i in snakes_ladder_store[0]:
        pygame.draw.line(screen, ( 166, 91, 0 ), ((pos_to_coor(i,mode)[0]+.5)*L1[mode],(pos_to_coor(i,mode)[1]+.5)*L1[mode]), ((pos_to_coor(snakes_ladder_store[0][i],mode)[0]+.5)*L1[mode],(pos_to_coor(snakes_ladder_store[0][i],mode)[1]+.5)*L1[mode]), 8)
    for i in snakes_ladder_store[1]:
        pygame.draw.line(screen, ( 0 , 128, 0 ), ((pos_to_coor(i,mode)[0]+.5)*L1[mode],(pos_to_coor(i,mode)[1]+.5)*L1[mode]), ((pos_to_coor(snakes_ladder_store[1][i],mode)[0]+.5)*L1[mode],(pos_to_coor(snakes_ladder_store[1][i],mode)[1]+.5)*L1[mode]), 8)
    

    
    screen.blit(Player1,(((pos_to_coor(PLAYER_SYMBOLS_POS[1],mode)[0]))*L1[mode] ,(pos_to_coor(PLAYER_SYMBOLS_POS[1],mode)[1])*L1[mode] + 2*L1[mode]/3))
    if PLAYER_NUMBER > 1:
        screen.blit(Player2,(((pos_to_coor(PLAYER_SYMBOLS_POS[2],mode)[0]))*L1[mode] + L1[mode]/3, (pos_to_coor(PLAYER_SYMBOLS_POS[2],mode)[1])*L1[mode] + 2 *L1[mode]/3))
    if PLAYER_NUMBER > 2:
        screen.blit(Player3,(((pos_to_coor(PLAYER_SYMBOLS_POS[3],mode)[0]))*L1[mode] + 2*L1[mode]/3, (pos_to_coor(PLAYER_SYMBOLS_POS[3],mode)[1])*L1[mode] + 2*L1[mode]/3))
    if PLAYER_NUMBER > 3:
        screen.blit(Player4,(((pos_to_coor(PLAYER_SYMBOLS_POS[4],mode)[0]))*L1[mode] + 2*L1[mode]/3, (pos_to_coor(PLAYER_SYMBOLS_POS[4],mode)[1])*L1[mode] + L1[mode]/3))
    if PLAYER_NUMBER > 4:
        screen.blit(Player5,(((pos_to_coor(PLAYER_SYMBOLS_POS[5],mode)[0]))*L1[mode] + 2*L1[mode]/3, (pos_to_coor(PLAYER_SYMBOLS_POS[5],mode)[1])*L1[mode]))
    



def game_mode():
    while 1:
        try:
            Select=int(input('please select game mode[Easy:1 Medium:2 Hard:3]\nEasy: Small board 5x5 with (fewer snakes than ladders)\nMedium: 6x6 board (number of snakes = number of ladders)\nHard: 10x10 board (more snakes than ladders)\n'))
        except:
            os.system('clear')
            print('error occurred,it should be integers 1-3')
        else:
            return Select

def snakes_ladders(mode):
    snakes_and_lad=[]
    #in the return list[0],for knowing ladders
    ladder_dict={}
    #in the return list[1],for knowing snakes
    snake_dict={}
    check_list=[]
    #in the return list[2],for knowing all positions
    position_dict={}

    if mode==1:
        for i in range(25):
            position_dict.update({i+1:i+1})
        number_of_lad=random.randint(4,8)
        for i in range(number_of_lad):
            ladder_top=random.randint(4,24)
            ladder_bot=random.randint(2,ladder_top-1)
            while 1:
                for i in check_list:
                    if ladder_top==i or ladder_bot==i:
                        break
                else:
                    break
                ladder_top=random.randint(4,24)
                ladder_bot=random.randint(2,ladder_top-1)
            check_list.append(ladder_top)
            check_list.append(ladder_bot)
            ladder_dict.update({ladder_bot:ladder_top})
            position_dict.update({ladder_bot:ladder_top})

        number_of_snake=random.randint(2,number_of_lad-1)
        for j in range(number_of_snake):
            snake_head=random.randint(2,24)
            snake_tail=random.randint(1,snake_head-1)
            while 1:
                for i in check_list:
                    if snake_head==i or snake_tail==i:
                        break
                else:
                    break
                snake_head=random.randint(4,24)
                snake_tail=random.randint(2,snake_head-1)
            check_list.append(snake_head)
            check_list.append(snake_tail)
            snake_dict.update({snake_head:snake_tail})
            position_dict.update({snake_head:snake_tail})



    if mode==2:
        for i in range(36):
            position_dict.update({i+1:i+1})
        number_of_lad=random.randint(4,8)
        for i in range(number_of_lad):
            ladder_top=random.randint(4,35)
            ladder_bot=random.randint(2,ladder_top-1)
            while 1:
                for i in check_list:
                    if ladder_top==i or ladder_bot==i:
                        break
                else:
                    break
                ladder_top=random.randint(4,24)
                ladder_bot=random.randint(2,ladder_top-1)
            check_list.append(ladder_top)
            check_list.append(ladder_bot)
            ladder_dict.update({ladder_bot:ladder_top})
            position_dict.update({ladder_bot:ladder_top})


        for j in range(number_of_lad):
            snake_head=random.randint(4,35)
            snake_tail=random.randint(2,snake_head-1)
            while 1:
                for i in check_list:
                    if snake_head==i or snake_tail==i:
                        break
                else:
                    break
                snake_head=random.randint(2,35)
                snake_tail=random.randint(1,snake_head-1)
            check_list.append(snake_head)
            check_list.append(snake_tail)
            snake_dict.update({snake_head:snake_tail})
            position_dict.update({snake_head:snake_tail})
        #0 is ladder, 1 is snake in list, 2 is total position



    if mode==3:
        for i in range(100):
            position_dict.update({i+1:i+1})
        number_of_snake=random.randint(4,8)
        number_of_lad=random.randint(2,number_of_snake-1)
        for i in range(number_of_snake):
            snake_head=random.randint(4,99)
            snake_tail=random.randint(2,snake_head-1)
            while 1:
                for i in check_list:
                    if snake_head==i or snake_tail==i:
                        break
                else:
                    break
                snake_head=random.randint(2,35)
                snake_tail=random.randint(1,snake_head-1)
            snake_dict.update({snake_head:snake_tail})
            position_dict.update({snake_head:snake_tail})
            check_list.append(snake_head)
            check_list.append(snake_tail)

        for j in range(number_of_lad):
            ladder_top=random.randint(2,99)
            ladder_bot=random.randint(1,ladder_top-1)
            while 1:
                for i in check_list:
                    if ladder_top==i or ladder_bot==i:
                        break
                else:
                    break
                ladder_top=random.randint(2,99)
                ladder_bot=random.randint(1,ladder_top-1)
            check_list.append(ladder_top)
            check_list.append(ladder_bot)
            ladder_dict.update({ladder_bot:ladder_top})
            position_dict.update({ladder_bot:ladder_top})
    #0 is ladder, 1 is snake in list
    snakes_and_lad.append(ladder_dict)   
    snakes_and_lad.append(snake_dict)
    snakes_and_lad.append(position_dict)
    return snakes_and_lad


def pos_to_coor(pos,mode):
    # posminus1 = pos - 1
    # if (L2[mode]-((posminus1 - posminus1 % L2[mode])/L2[mode])) % 2 == 1:
    #     x, y = posminus1 % L2[mode] + 1, L2[mode]+1 -(L2[mode] - (posminus1 - posminus1 % L2[mode])/L2[mode] + 1)
    #     if posminus1 % L2[mode] == 0:
    #         x = 1
    # else:
    #     x, y = L2[mode] - posminus1 % L2[mode], L2[mode]+1 -(L2[mode] - (posminus1 - posminus1 % L2[mode])/L2[mode] + 1)
    #     if posminus1 % L2[mode] == 0:
    #         x = L2[mode]
    # return [ x ,y ]

    num = pos - 1
    y = L2[mode]-1-(num-num%L2[mode])/L2[mode]
    if y%2 == 0:
        x = num % L2[mode]
    else:
        x = L2[mode]-1-num % L2[mode]
    return [x,y]




def start_game () :
    
    
    
    PLAYER_SYMBOLS=['\U0001F911','\U0001F917','\U0001F92B','\U0001F976','\U0001F913']
    PLAYER_SYMBOLS_POS={1:1,2:1,3:1,4:1,5:1}
    PLAYER_NUMBER=int(determine_player_no_valid ())
    while 1:
        if PLAYER_NUMBER > 5 or PLAYER_NUMBER <1:
            print('player numbers should be 1-5')
            PLAYER_NUMBER=int(determine_player_no_valid())
        else:
            break
    #collect mode
    mode=game_mode()
    #build lists according to mode


    #spawn snakes and ladder,(it's a list,[0]is ladder,[1] is snake,and numbers of them are stored in dictionary)
    snakes_ladder_store=snakes_ladders(mode)
    # print(snakes_ladder_store)
    # draw_the_board(mode,PLAYER_SYMBOLS_POS,snakes_ladder_store,PLAYER_NUMBER)
    


    character_key=1
    while 1:

        if character_key==PLAYER_NUMBER+1:
            character_key=1


        c = pygame.Surface((720,120))
        c.fill((255,255,255))
        screen.blit(c,(0,720))
        text_surface = font.render(f"Player{character_key}", True, (0,0,0))
        screen.blit(text_surface,(10,740))
        
        os.system('clear')
        dicen=dice()
        # pygame.event.get()
        # if event.type==pygame.KEYDOWN and event.key==pygame.K_SPACE:
        #     continue
        

        # draw_the_board(mode,PLAYER_SYMBOLS_POS,snakes_ladder_store,PLAYER_NUMBER)

        # for i in range(30):
            
        #     a = pygame.image.load(f"Dice{dice()}.png")
        #     screen.blit( a, (610, 730) )

        #     c = pygame.Surface((100,100))
        #     c.fill((255,255,255))
        #     screen.blit(c,(610,730))

            
        a = pygame.image.load(f"Dice{dicen}.png")
        screen.blit( a, (610, 730) )
        # print(f'The dice rolled to {dicen}') 

        #position player was staying
        original_position=PLAYER_SYMBOLS_POS[character_key]
        #new position player is staying
        new_position=original_position+dicen

        
        
        

        if mode==1 and new_position>=25 or mode==2 and new_position>=36 or mode==3 and new_position>=100:
            
            draw_the_board(mode,PLAYER_SYMBOLS_POS,snakes_ladder_store,PLAYER_NUMBER)
            text_surface = font.render(f"{character_key} won!!", True, (0,0,0))
            screen.blit(text_surface,(240,740))
            pygame.display.update()
            
            running = True
            while running:
                for event in pygame.event.get():
                    # Event handling code goes here
                    if event.type == pygame.KEYDOWN or event.type == pygame.QUIT:
                        pygame.quit()
            

        
        PLAYER_SYMBOLS_POS.update({PLAYER_SYMBOLS[character_key]:new_position})
        # print(f'{PLAYER_SYMBOLS[character_key]} is now in position {new_position}')
        new_position2=snakes_ladder_store[2][new_position]
        PLAYER_SYMBOLS_POS.update({character_key:new_position2})
        
        draw_the_board(mode,PLAYER_SYMBOLS_POS,snakes_ladder_store,PLAYER_NUMBER)
        
        if new_position2>new_position:
            text_surface = font.render(f"Ladder {new_position2}", True, (0,0,0))
            screen.blit(text_surface,(220,740))
            # print(f'u climbed up a ladder to position {new_position2}')
            
        elif new_position2<new_position:
            text_surface = font.render(f"Snake {new_position2}", True, (0,0,0))
            screen.blit(text_surface,(220,740))
            # print(f'u slipped from a snake to position {new_position2}')
        
        
        pygame.display.update()
        
        running = True
        while running:
            for event in pygame.event.get():
                # Event handling code goes here
                if event.type == pygame.KEYDOWN:
                    running = False
                elif event.type == pygame.QUIT:
                    pygame.quit()
                    exit()

        character_key+=1


pygame.init()
screen = pygame.display.set_mode((720,840))
font = pygame.font.Font(None, 80)
pygame.display.set_caption("Grid")
clock = pygame.time.Clock()
screen.fill((255,255,255))
start_game()

while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            exit()
