import pygame

# 初期設定
pygame.init()
WIDTH, HEIGHT = 600, 400
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("ふわふわバルーンぼうけん！")

# 色設定
WHITE = (255, 255, 255)
BLUE = (150, 200, 255)

# 妖精の初期位置と速度
fairy_x = WIDTH // 2
fairy_y = HEIGHT // 2
velocity = 0
gravity = 0.2  # ふんわり落ちる
jump_power = -5  # ふわっと上昇

# ゲームループ
running = True
while running:
    screen.fill(WHITE)
    
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_SPACE:  # スペースキーで上昇
                velocity = jump_power

    # 重力の影響で下降
    velocity += gravity
    fairy_y += velocity

    # 画面の端で止める
    if fairy_y < 50:
        fairy_y = 50
        velocity = 0
    if fairy_y > HEIGHT - 50:
        fairy_y = HEIGHT - 50
        velocity = 0

    # 妖精（仮：青い丸）を描画
    pygame.draw.circle(screen, BLUE, (fairy_x, int(fairy_y)), 20)

    pygame.display.update()
    pygame.time.delay(20)

pygame.quit()
