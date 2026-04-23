# project-soai
#Heni Oufras, Mikail Celik (groep 2)

import pygame
pygame.init()
pygame.display.set_caption("NOT SUPER SMASH BROS")


scherm = pygame.display.set_mode((1280,720))
frame_count = 60.0
clock = pygame.time.Clock()


class personnage_2(pygame.sprite.Sprite):
    def __init__(self): 
        super(personnage_2, self).__init__() 
        self.image_right = pygame.image.load("GOKU .png")
        self.image_left = pygame.image.load("GOKU_reverse.png")
        self.surf = self.image_right
        self.richting = 1
        self.sprong = 0
        self.max_sprong = 2
        self.damage = 0
        self.op_grond = False 
        self.rect = self.surf.get_rect() 
        self.rect.x = 640
        self.rect.y = 450 
        self.gr = 0 
        self.dashing = False
        self.dashing_tijd = 0
        self.dashing_maxtijd = frame_count * 0.15
        self.dashing_cooldown = frame_count * 2
        self.dashing_Ctijd = 0 
        self.levens = 1
    def update(self,pressed_keys): 
        self.rect.y +=self.gr 
        if self.richting == 1:
            self.surf = self.image_right
        else:
            self.surf = self.image_left
        if self.rect.y <= 0 or self.rect.y >= 720 or self.rect.x <= 0 or self.rect.x >= 1280:
            if self.levens >= 0:
                self.rect.x = 640
                self.rect.y = 450
                self.levens -=1
            else:
                print("player 2 lose")
        if pressed_keys[pygame.K_RETURN] and not self.dashing and self.dashing_Ctijd >= self.dashing_cooldown:
            self.dashing = True
            self.dashing_tijd = 0
        if pressed_keys[pygame.K_RSHIFT]:
            if len(attaque) < 1:
                projectiel = long_range_att(self.rect.center, self.richting)
                attaque.add(projectiel)
        if self.dashing:
            if self.dashing_tijd < self.dashing_maxtijd:
                self.rect.x += 25 * self.richting
                self.dashing_tijd += 1
            else:
                self.dashing = False
                self.dashing_Ctijd = 0
        if not self.dashing:
            self.dashing_Ctijd += 1
        if pressed_keys[pygame.K_RCTRL]:
            if len(attaque) < 1:
                projectiel = long_range_att(self.rect.center, self.richting)
                attaque.add(projectiel)
        if pressed_keys[pygame.K_RIGHT]: 
            self.rect.x +=7 
            self.richting = 1
        if pressed_keys[pygame.K_LEFT]: 
            self.rect.x -= 7 
            self.richting = -1
        if pressed_keys[pygame.K_DOWN]: 
            if 480 <=self.rect.y <= 500 and 250 <= self.rect.x <= 950: 
                self.rect.y = 485
            else:
                self.rect.y +=20 
        if pressed_keys[pygame.K_UP] and self.sprong <= self.max_sprong: 
            if self.sprong == 0:
                self.gr = -65
            else:
                self.gr = -40
            self.sprong += 1 
        elif 295<= self.rect.y <= 300 and 750 <= self.rect.x <= 1070: 
            self.rect.y = 300 
            self.gr = 0 
            self.sprong = 0
        elif 295<=self.rect.y <= 300 and 140 <= self.rect.x <= 460: 
            self.rect.y = 300 
            self.gr = 0 
            self.sprong = 0
        elif 480 <=self.rect.y <= 500 and 250 <= self.rect.x <= 950: 
            self.rect.y = 485 
            self.gr = 0 
            self.sprong = 0
        else: 
            self.gr += 5        
            self.gr = min(self.gr, 25)
    
class personnage(pygame.sprite.Sprite): 
    def __init__(self): 
        super(personnage, self).__init__() 
        self.image_right = pygame.image.load("GOKU .png")
        self.image_left = pygame.image.load("GOKU_reverse.png")
        self.surf = self.image_right
        self.richting = 1
        self.sprong = 0
        self.max_sprong = 2
        self.op_grond = False 
        self.rect = self.surf.get_rect() 
        self.rect.x = 640
        self.rect.y = 450 
        self.gr = 0 
        self.dashing = False
        self.dashing_tijd = 0
        self.dashing_maxtijd = frame_count * 0.15
        self.dashing_cooldown = frame_count * 2
        self.dashing_Ctijd = 0 
        self.levens = 1
    def update(self,pressed_keys): 
        self.rect.y +=self.gr 
        if self.richting == 1:
            self.surf = self.image_right
        else:
            self.surf = self.image_left
            
        if self.rect.y <= 0 or self.rect.y >= 720 or self.rect.x <= 0 or self.rect.x >= 1280:
            if self.levens >= 0 :
                self.rect.x = 640
                self.rect.y = 450
                self.levens -= 1
            else:
                print("player 1 lose")
        if pressed_keys[pygame.K_LSHIFT] and not self.dashing and self.dashing_Ctijd >= self.dashing_cooldown:
            self.dashing = True
            self.dashing_tijd = 0
        
        if self.dashing:
            if self.dashing_tijd < self.dashing_maxtijd:
                self.rect.x += 25 * self.richting
                self.dashing_tijd += 1
            else:
                self.dashing = False
                self.dashing_Ctijd = 0
        if not self.dashing:
            self.dashing_Ctijd += 1
        if pressed_keys[pygame.K_SPACE]:
            if len(attaque) < 1:
                projectiel = long_range_att(self.rect.center, self.richting)
                attaque.add(projectiel)
        if pressed_keys[pygame.K_d]: 
            self.rect.x +=7 
            self.richting = 1
        if pressed_keys[pygame.K_q]: 
            self.rect.x -= 7 
            self.richting = -1
        if pressed_keys[pygame.K_s]: 
            if 480 <=self.rect.y <= 500 and 250 <= self.rect.x <= 950: 
                self.rect.y = 485
            else: 
                self.rect.y +=20 
        if pressed_keys[pygame.K_z] and self.sprong <= self.max_sprong: 
            if self.sprong == 0:
                self.gr = -65
            else:
                self.gr = -40
            self.sprong += 1 
        elif 295<= self.rect.y <= 300 and 750 <= self.rect.x <= 1070: 
            self.rect.y = 300 
            self.gr = 0 
            self.sprong = 0
        elif 295<=self.rect.y <= 300 and 140 <= self.rect.x <= 460: 
            self.rect.y = 300 
            self.gr = 0 
            self.sprong = 0
        elif 480 <=self.rect.y <= 500 and 250 <= self.rect.x <= 950: 
            self.rect.y = 485 
            self.gr = 0 
            self.sprong = 0
        else: 
            self.gr += 5        
            self.gr = min(self.gr, 25)
        

class long_range_att(pygame.sprite.Sprite):
    def __init__(self, center_personnage, direction):
        super().__init__()
        self.surf = pygame.Surface((20,20))
        self.surf.fill((0,250,0))
        self.rect = self.surf.get_rect(center = center_personnage)
        self.direction = direction
    def update(self):
        self.rect.x += (15 * self.direction)
        if self.rect.right >= 1280 or self.rect.left <= 0:
            self.kill()
            
            
        
            
attaque = pygame.sprite.Group()
Geveta = personnage_2()
Kogu = personnage()
alle_spelers = pygame.sprite.Group()
alle_spelers.add(Kogu)
alle_spelers.add(Geveta)


doorlopen = True
while doorlopen:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            doorlopen = False
    scherm.fill((135, 206, 235)) # achtregrond
    pygame.draw.circle(scherm, (255,255,255),(650,120),30)
    pygame.draw.circle(scherm, (255,255,255),(690,120),35)
    pygame.draw.circle(scherm,(255,255,255),(730,120),30) 
    pygame.draw.rect(scherm, (255,255,255),(650,120,80,30)) #wolk rechts
    pygame.draw.circle(scherm,(255,255,255),(180,80),25)
    pygame.draw.circle(scherm, (255,255,255), (150,80), 30)
    pygame.draw.circle(scherm, (255,255,255), (120,80), 25)
    pygame.draw.rect(scherm,(255,255,255), (120,80,70,25)) # wolk links
    pygame.draw.circle(scherm,(255,255,255),(280,235),15)
    pygame.draw.circle(scherm,(255,255,255),(300,235),20)
    pygame.draw.circle(scherm,(255,255,255),(320,235),15)
    pygame.draw.rect(scherm,(255,255,255),(280,235,40,20)) # wolk middel
    pygame.draw.circle(scherm,(255,223,0),(1080,150),80) # zon 
    pygame.draw.rect(scherm,(160,82,45),(320,586,630,65))
    pygame.draw.rect(scherm,(124,252,0),(320,586,630,15))
    pygame.draw.rect(scherm,(160,82,45),(820,400,250,45))
    pygame.draw.rect(scherm,(124,252,0),(820,400,250,12))
    pygame.draw.rect(scherm,(160,82,45),(210,400,250,45))
    pygame.draw.rect(scherm,(124,252,0),(210,400,250,12)) #platforms
    for speler in alle_spelers:
        scherm.blit(speler.surf,speler.rect)# spelers
    key_pressed = pygame.key.get_pressed()
    alle_spelers.update(key_pressed)
    attaque.update()
    for projectiel in attaque:
        scherm.blit(projectiel.surf, projectiel.rect)
    pygame.display.flip()
    clock.tick(frame_count)

pygame.quit() #achtergrond klaar
