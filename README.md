- 👋 Hi, I’m @jordiPIP
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
jordiPIP/jordiPIP is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->import pygame
import random

# Inicialización de Pygame
pygame.init()

# Configuración de la pantalla
screen_width = 800
screen_height = 600
screen = pygame.display.set_mode((screen_width, screen_height))
pygame.display.set_caption("Atrapa la pelota")

# Colores
white = (255, 255, 255)
blue = (0, 0, 255)

# Jugador
player_width = 50
player_height = 50
player_x = (screen_width - player_width) // 2
player_y = screen_height - player_height

# Pelota
ball_width = 25
ball_height = 25
ball_x = random.randint(0, screen_width - ball_width)
ball_y = 0
ball_speed = 5

# Puntuación
score = 0

# Reloj
clock = pygame.time.Clock()

# Bucle principal del juego
running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT] and player_x > 0:
        player_x -= 5
    if keys[pygame.K_RIGHT] and player_x < screen_width - player_width:
        player_x += 5

    ball_y += ball_speed

    # Colisión entre la pelota y el jugador
    if (
        player_x < ball_x < player_x + player_width
        and player_y < ball_y < player_y + player_height
    ):
        ball_x = random.randint(0, screen_width - ball_width)
        ball_y = 0
        score += 1

    # Dibujar la pantalla
    screen.fill(white)
    pygame.draw.rect(screen, blue, (player_x, player_y, player_width, player_height))
    pygame.draw.ellipse(screen, blue, (ball_x, ball_y, ball_width, ball_height))

    # Mostrar la puntuación
    font = pygame.font.Font(None, 36)
    text = font.render(f"Puntuación: {score}", True, blue)
    screen.blit(text, (10, 10))

    pygame.display.update()
    clock.tick(60)

pygame.quit()
