import pygame
import os
import random
os.environ["SDL_VIDEO_CENTERED"]='1'
Height = 600
Width = 600
class grid:
    def __init__(self,height,width,scale,offset):
         self.height = height
         self.width = width
         self.board = []
         self.scale = scale
         self.offset = offset
         for row in range(height):
             rows = []
             for column in range(width):
                 rows.append(cell())
             self.board.append(rows)

    def two_dim_array(self):
         for i in self.board:
             for j in i:
                  if(random.randint(0,1) == 1):
                      j.make_alive()
         return self.board

    def neighbours(self,row,column):
         lst = []
         for i in range(-1,2):
             for j in range(-1,2):
                 neigh_row = row + i
                 neigh_col = column + j
                 valid = 1
                 if((neigh_row) == row and (neigh_col) == column) or ((neigh_row) < 0 or (neigh_row) >= self.height) or ((neigh_col) < 0 or (neigh_col) >= self.width):
                     valid = 0
                 if(valid == 1):
                     lst.append(self.board[neigh_row][neigh_col])
         return lst 
    
    def next_generation(self):
         live = []
         die = []
         for row in range(len(self.board)):
             for column in range(len(self.board[row])):
                 neighbours = self.neighbours(row,column)
                 count = 0
                 for neighbour in neighbours:
                     if(neighbour.is_alive()):
                         count += 1
                 Cell = self.board[row][column]
                 status = Cell.is_alive()
                 if status == True:
                     if(count == 2 or count == 3):
                         live.append(cell)
                     if(count < 2 or count > 3):
                         die.append(cell)
                 else:
                     if(count == 3):
                         live.append(cell)
         for i in live:
             i.make_alive(self)
         for j in die:
             j.make_dead(self) 
    def display_grid(self,surface,live_colour,dead_colour):
         for i in range(self.height):
             for j in range(self.width):
                 x = i*self.scale
                 y = j*self.scale
                 if(self.board[i][j].is_alive()):
                     pygame.draw.rect(surface,live_colour,[x,y,self.scale-self.offset,self.scale-self.offset])
                 else:
                     pygame.draw.rect(surface,dead_colour,[x,y,self.scale-self.offset,self.scale-self.offset])
class cell:
    def __init__(self):
         self.status = 'dead'
    def make_alive(self):
         self.status = 'alive'
    def make_dead(self):
         self.status = 'dead'
    def is_alive(self):
         if(self.status == 'alive'):
             return True
         return False

def main():
    height = int(input('height = '))
    width = int(input('width = '))
    pygame.init()
    size = (Width,Height)
    pygame.display.set_caption("Conway's Game of Life")
    screen = pygame.display.set_mode(size)
    clock = pygame.time.Clock()
    fps = 5
    black = (0,0,0)
    blue = (0,14,71) 
    white = (255,255,255)
    scale = 40
    offset = 1
    clock.tick(fps)
    screen.fill(black)
    Grid = grid(height,width,scale,offset)
    Grid.two_dim_array()
    Grid.display_grid(surface=screen,live_colour=white,dead_colour=blue)
    while True:
        for event in pygame.event.get():
            if(event.type == pygame.QUIT):
                pygame.quit()
                return
        Grid.next_generation()
        Grid.display_grid(surface=screen,live_colour=white,dead_colour=blue)
        pygame.display.update()
main()
