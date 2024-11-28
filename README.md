- 👋 Hi, I’m @MIZZI-ai
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
MIZZI-ai/MIZZI-ai is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import pygame
import sys
import random

# Initialize Pygame
pygame.init()

# Screen dimensions
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption('Simple Hole Game')

# Colors
BLACK = (0, 0, 0)
WHITE = (255, 255, 255)
HOLE_COLOR = (50, 50, 50)

# Hole properties
hole_radius = 30
hole_pos = [WIDTH // 2, HEIGHT // 2]
hole_speed = 5
growth_rate = 1

# Object properties
object_radius = 10
objects = [pygame.Rect(random.randint(0, WIDTH), random.randint(0, HEIGHT), object_radius*2, object_radius*2) for _ in range(20)]

# Game loop
clock = pygame.time.Clock()
running = True

while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT]:
        hole_pos[0] -= hole_speed
    if keys[pygame.K_RIGHT]:
        hole_pos[0] += hole_speed
    if keys[pygame.K_UP]:
        hole_pos[1] -= hole_speed
    if keys[pygame.K_DOWN]:
        hole_pos[1] += hole_speed

    screen.fill(WHITE)
    
    for obj in objects:
        pygame.draw.circle(screen, BLACK, obj.center, object_radius)
        if obj.collidepoint(hole_pos[0], hole_pos[1]):
            objects.remove(obj)
            hole_radius += growth_rate

    pygame.draw.circle(screen, HOLE_COLOR, hole_pos, hole_radius)
    
    pygame.display.flip()
    clock.tick(60)

pygame.quit()
sys.exit()
