- 👋 Hi, I’m @belktech
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
belktech/belktech is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import pygame
from pygame.locals import *
from PIL import Image, ImageDraw
import sys

# Initialisation de Pygame
pygame.init()

# Paramètres du jeu
largeur_fenetre = 800
hauteur_fenetre = 600
couleur_fond = (255, 255, 255)

# Initialisation de la fenêtre du jeu
fenetre = pygame.display.set_mode((largeur_fenetre, hauteur_fenetre))
pygame.display.set_caption("Jeu de voiture")

# Création de l'image de voiture avec Pillow
def creer_image_voiture():
    largeur_image = 50
    hauteur_image = 30
    image = Image.new("RGB", (largeur_image, hauteur_image), (255, 255, 255))
    draw = ImageDraw.Draw(image)

    # Dessin de la voiture (rectangle rouge)
    couleur_voiture = (255, 0, 0)
    position_x = 10
    position_y = 10
    largeur_voiture = 30
    hauteur_voiture = 20
    draw.rectangle([position_x, position_y, position_x + largeur_voiture, position_y + hauteur_voiture], fill=couleur_voiture)

    # Enregistrement de l'image
    image.save("car.png")

# Chargement de l'image de la voiture
creer_image_voiture()
voiture_image = pygame.image.load("car.png")

# Position initiale de la voiture
x_voiture = largeur_fenetre // 2 - voiture_image.get_width() // 2
y_voiture = hauteur_fenetre - voiture_image.get_height() - 10

# Vitesse de déplacement de la voiture
vitesse_voiture = 5

# Boucle principale du jeu
while True:
    for event in pygame.event.get():
        if event.type == QUIT:
            pygame.quit()
            sys.exit()

    # Déplacement de la voiture
    touches = pygame.key.get_pressed()
    if touches[K_LEFT] and x_voiture > 0:
        x_voiture -= vitesse_voiture
    if touches[K_RIGHT] and x_voiture < largeur_fenetre - voiture_image.get_width():
        x_voiture += vitesse_voiture

    # Rafraîchissement de l'écran
    fenetre.fill(couleur_fond)
    fenetre.blit(voiture_image, (x_voiture, y_voiture))
    pygame.display.flip()

    # Limiter la fréquence d'images pour ne pas surcharger le processeur
    pygame.time.Clock().tick(60)
