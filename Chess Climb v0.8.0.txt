#A chess platformer game made by Angus Sun
#Chess Climb 1.0
import simplegui, math, time
#textures for backgrounds
CHOOSEPIECE = simplegui.load_image("https://i.imgur.com/wRHvDyg.png")
WORLD1BGRD = simplegui.load_image("https://i.imgur.com/8P03prL.png")
WORLD2BGRD = simplegui.load_image("https://i.imgur.com/bPxv3Tg.png")
SELECTIONBGRD = simplegui.load_image("https://i.imgur.com/5VNue7E.png")
SELECTIONBGRD2 = simplegui.load_image("https://i.imgur.com/gG0CVTA.png")
BLACK_CIRCLES = simplegui.load_image("https://i.ibb.co/k4YSHJd/spritesheet-2.png")
CHESS_MOVES = simplegui.load_image("https://i.imgur.com/ilE1773.png")
CHESS_MOVES2 = simplegui.load_image("https://i.imgur.com/t0r3foz.png")
CHESS_GUIDE_DIALOGUE_BOX = simplegui.load_image("https://i.imgur.com/yoVVcRY.png")
TUTORIAL_OVERLAY = simplegui.load_image("https://i.imgur.com/vCF6g9n.png")
#sound effects
PIECE_UPGRADE = simplegui.load_sound("https://www.dropbox.com/scl/fi/eh7yitn3hp34h7wb1h6ny/y2mate.is-Pok-mon-Level-Up-Sound-Effect-No-Copyright-HD-a55Bg_TfF8g-192k-1686986865-4.mp3?rlkey=98rt698prgf0kbmkgfzzu3jcl&st=7383o49w&dl=1")
MOVE_SOUND 	= simplegui.load_sound("https://www.dropbox.com/scl/fi/kqem2rwrs83a9wrix9l2n/YOYOYO.mp3?rlkey=xdms83do0iaxra426jcfgkyf5&st=iwhbcxkc&dl=1")
DEATH_SOUND = simplegui.load_sound("https://www.dropbox.com/scl/fi/rvmavue2es1uhq151ep90/goofy-ahh-scream.mp3?rlkey=37yrnd775wfb91h7v724md9mv&st=4vsrfu6n&dl=1")
BUTTON_SOUND = simplegui.load_sound("https://www.dropbox.com/scl/fi/ccspzkj301beay3oyq7pk/buttonsound.mp3?rlkey=44kf3t914x4kd189so53qlh9n&st=hcw9z5ff&dl=1")
WORLD1_MUSIC = simplegui.load_sound("https://www.dropbox.com/scl/fi/0rrpj0jl2t0lvaslvl9q6/hatenovillage.mp3?rlkey=1i4bb3w1k7cx4rdi0tjfnws7e&st=w56kmsjs&dl=1")
WORLD2_MUSIC = simplegui.load_sound("https://www.dropbox.com/scl/fi/tr0dn08rk976hj2wpwham/Ocarina-of-Time-Gerudo-Valley-extended.mp3?rlkey=bcuu0md7tu31b89vub40xamx5&st=8rgwzj3p&dl=1")
LEVEL_SELECT_MUSIC = simplegui.load_sound("https://www.dropbox.com/scl/fi/j78jc66w31bbpuec4z2ml/onlymp3.to-Miitopia-OST-Cottage-Lb-lJXLBWSo-256k-1656541717758.mp3?rlkey=19bqzn4itd54ra61lv5b6ahvz&st=wwkhs53d&dl=1")
TALKING_SOUND = simplegui.load_sound("https://www.dropbox.com/scl/fi/1nivcklu0bfcc7u9i0wr6/onlymp3.to-Just-Sans-talking-TQqyArvAn4k-256k-1657490797433.mp3?rlkey=921lor2irv01akz7yh9dejw7z&st=fi3t0t5b&dl=1")
CRATEBREAK = simplegui.load_sound("https://www.dropbox.com/scl/fi/nlfusw1aha96riny5m2zh/onlymp3.to-Impact-Wood-Crack-Sound-Effect-SFX-aONb6YffPT8-256k-1654092474711_1.mp3?rlkey=yajz6f3h44fwtvfnjkqdkg7z9&st=ocqunoks&dl=1")
CRATECRACK = simplegui.load_sound("https://www.dropbox.com/scl/fi/yamj00nmm1k9stkbaeygb/onlymp3.to-Impact-Wood-Crack-Sound-Effect-SFX-aONb6YffPT8-256k-1654092474711_3.mp3?rlkey=88nhfzbx5mqro5uk0rt4irn3g&st=l7rhmg0v&dl=1")
TUTORIAL_MUSIC = simplegui.load_sound("https://www.dropbox.com/scl/fi/03fucxzibiubvcl5m5740/onlymp3.to_-_Tutorial_Instrumental-yaAIfEvQPkE-256k-1659868494390.mp3?rlkey=3kuzxmu8fzn53fn7bd4qbyv0i&st=sp3x2gk9&dl=1")
PRESSURE_PLATE_PRESSED = simplegui.load_sound("https://www.dropbox.com/scl/fi/jppctsc5qidn09r1527fb/pressureplate-pressed.mp3?rlkey=snxuc6rakqmojtq8k20o5g8tr&st=4i3uzeow&dl=1")
PRESSURE_PLATE_RELEASED = simplegui.load_sound("https://www.dropbox.com/scl/fi/beushw28to7zd59n6x4c3/pressureplate-released.mp3?rlkey=rz2hi6kw87wl81zacmdvzyh6i&st=omp65p2y&dl=1")
DOOR_OPEN = simplegui.load_sound("https://www.dropbox.com/scl/fi/bx2s464x2akbhwzjvasuf/onlymp3.to-Minecraft-Door-open-Sound-effect-HD-LZbqJbs7evs-256k-1655019128201.mp3?rlkey=x7h53aolgy16w6nkvuqzei6x5&st=geehfb1g&dl=1")
DOOR_CLOSE = simplegui.load_sound("https://www.dropbox.com/scl/fi/hb6ac311ekuis8t36orgz/tomp3.cc-Minecraft-Pressure-Plate-Sound-Effect_1.mp3?rlkey=kfp9rv6dou1nrvvp8rl1l3z34&st=f6gg6h2i&dl=1")
#textures for buttons
NEWMOVE = simplegui.load_image("https://i.imgur.com/d2aaL2c.png")
HINT_BUTTON = simplegui.load_image("https://i.imgur.com/jU2Mv86.png")
GUIDE_BUTTON = simplegui.load_image("https://i.imgur.com/7ckhIoY.png")
NOTHING = simplegui.load_image("https://media.discordapp.net/attachments/794098849739702282/1107424744694882314/120px-Antonia_Sautter_Creations.png?width=107&height=107")
LOCKED_BUTTON = simplegui.load_image("https://i.imgur.com/UPAR1qS.png")
START_BUTTON = simplegui.load_image("https://i.imgur.com/bAHczwO.png")
NEXT_BUTTON = simplegui.load_image("https://i.imgur.com/n8fsprK.png")
MENU_BACK_BUTTON = simplegui.load_image("https://i.imgur.com/Vxb5c78.png")
TUTORIAL_BUTTON = simplegui.load_image("https://i.imgur.com/Btf66yb.png")

LVL1_BUTTON = simplegui.load_image("https://i.imgur.com/qL80XKA.png")
LVL2_BUTTON = LOCKED_BUTTON
LVL3_BUTTON = LOCKED_BUTTON
LVL4_BUTTON = LOCKED_BUTTON
LVL5_BUTTON = LOCKED_BUTTON
LVL6_BUTTON = LOCKED_BUTTON
LVL7_BUTTON = LOCKED_BUTTON
LVL8_BUTTON = LOCKED_BUTTON
LVL9_BUTTON = LOCKED_BUTTON
LVL10_BUTTON = LOCKED_BUTTON
LVL11_BUTTON = LOCKED_BUTTON
LVL12_BUTTON = LOCKED_BUTTON
LVL13_BUTTON = LOCKED_BUTTON
LVL14_BUTTON = LOCKED_BUTTON
LVL15_BUTTON = LOCKED_BUTTON
LVL16_BUTTON = LOCKED_BUTTON

LVL1_COMPLETED = simplegui.load_image("https://i.imgur.com/8FxxU9F.png")
LVL2_UNCOMPLETED = simplegui.load_image("https://i.imgur.com/mInPm1m.png")
LVL2_COMPLETED = simplegui.load_image("https://i.imgur.com/93HqRtv.png")           
LVL3_UNCOMPLETED = simplegui.load_image("https://i.imgur.com/UxXWwPO.png")
LVL3_COMPLETED = simplegui.load_image("https://i.imgur.com/60UIpZh.png")   
LVL4_UNCOMPLETED = simplegui.load_image("https://i.imgur.com/YvwP2cL.png")
LVL4_COMPLETED = simplegui.load_image("https://i.imgur.com/ZVz5d1p.png")   
LVL5_UNCOMPLETED = simplegui.load_image("https://i.imgur.com/bIJy8zs.png")
LVL5_COMPLETED = simplegui.load_image("https://i.imgur.com/Mflh9UC.png")   
LVL6_UNCOMPLETED = simplegui.load_image("https://i.imgur.com/3iq4NHu.png")
LVL6_COMPLETED = simplegui.load_image("https://i.imgur.com/ylSV1nX.png")   
LVL7_UNCOMPLETED = simplegui.load_image("https://i.imgur.com/aQ1sNr7.png")
LVL7_COMPLETED = simplegui.load_image("https://i.imgur.com/fNYUXpM.png")   
LVL8_UNCOMPLETED = simplegui.load_image("https://i.imgur.com/7WG6ZCM.png")
LVL8_COMPLETED = simplegui.load_image("https://i.imgur.com/P98GtHY.png")   
LVL9_UNCOMPLETED = simplegui.load_image("https://i.imgur.com/wvA7EA9.png")
LVL9_COMPLETED = simplegui.load_image("https://i.imgur.com/PgbPj7d.png")
LVL10_UNCOMPLETED = simplegui.load_image("https://i.imgur.com/oo3kw9M.png")
LVL10_COMPLETED = simplegui.load_image("https://i.imgur.com/56GHe1G.png")
LVL11_UNCOMPLETED = simplegui.load_image("https://i.imgur.com/Fxtqrd1.png")
LVL11_COMPLETED = simplegui.load_image("https://i.imgur.com/H3y09Aa.png")
LVL12_UNCOMPLETED = simplegui.load_image("https://i.imgur.com/MHIxzw0.png")
LVL12_COMPLETED = simplegui.load_image("https://i.imgur.com/IHj0v07.png")
LVL13_UNCOMPLETED = simplegui.load_image("https://i.imgur.com/ap5Mg4u.png")
LVL13_COMPLETED = simplegui.load_image("https://i.imgur.com/FYYO3w7.png")
LVL14_UNCOMPLETED = simplegui.load_image("https://i.imgur.com/Qg7JgF4.png")
LVL14_COMPLETED = simplegui.load_image("https://i.imgur.com/py9kpqy.png")
LVL15_UNCOMPLETED = simplegui.load_image("https://i.imgur.com/zDa9Zoh.png")
LVL15_COMPLETED = simplegui.load_image("https://i.imgur.com/GwgaFsz.png")
LVL16_UNCOMPLETED = simplegui.load_image("https://i.imgur.com/kO9LYdQ.png")
LVL16_COMPLETED = simplegui.load_image("https://i.imgur.com/Z6yXEcj.png")

RESTART_BUTTON = simplegui.load_image("https://i.imgur.com/uYiJqGV.png")
BACK_BUTTON = simplegui.load_image("https://i.imgur.com/ClJCE8a.png")
CRATE1 = simplegui.load_image("https://i.imgur.com/NF3rF3j.png")
CRATE2 = simplegui.load_image("https://i.imgur.com/mRVqfYS.png")
#textures for chess pieces
BLACK_KING = simplegui.load_image("https://i.imgur.com/4yrraHj.png")
BLACK_PAWN = simplegui.load_image("https://i.imgur.com/rw53j16.png")
WHITE_KING = simplegui.load_image("https://i.imgur.com/HOtRr6n.png")
WHITE_PAWN = simplegui.load_image("https://i.imgur.com/tQun7hd.png")
WHITE_QUEEN = simplegui.load_image("https://i.imgur.com/aqEpFC1.png")
WHITE_ROOK = simplegui.load_image("https://i.imgur.com/puHFwOh.png")
WHITE_HORSE = simplegui.load_image("https://i.imgur.com/xLzCMoD.png")
WHITE_BISHOP = simplegui.load_image("https://i.imgur.com/XjkAtbE.png")
#textures for main menu
MENU_IMAGE = simplegui.load_image("https://i.imgur.com/u7FcVuN.png")
#block textures
#world 1 
GRASS = simplegui.load_image("https://i.imgur.com/rs8IXMO.png")
CONNECTED_DIRT = simplegui.load_image("https://i.imgur.com/Gwuf6iK.png")
LEFT_GRASS = simplegui.load_image("https://i.imgur.com/2hUaD1S.png")
RIGHT_GRASS = simplegui.load_image("https://i.imgur.com/9CgtOCs.png")
RIGHT_DIRT_SURFACELESS = simplegui.load_image("https://i.imgur.com/wNYTzv8.png")
LEFT_DIRT_SURFACELESS = simplegui.load_image("https://i.imgur.com/yiRDk1C.png")
LEFT_GRASS_FLOAT = simplegui.load_image("https://i.imgur.com/cth3GNk.png")
GRASS_FLOAT = simplegui.load_image("https://i.imgur.com/1FzCSWt.png")
RIGHT_GRASS_FLOAT = simplegui.load_image("https://i.imgur.com/QCBJXey.png")
LEFT_WALL_GRASS = simplegui.load_image("https://i.imgur.com/JW7KTP7.png")
RIGHT_WALL_GRASS = simplegui.load_image("https://i.imgur.com/R9hVIJx.png")
BOTTOM_RIGHT_DIRT = simplegui.load_image("https://i.imgur.com/dBRfxAM.png")
BOTTOM_LEFT_DIRT = simplegui.load_image("https://i.imgur.com/CYJs6A5.png")
FLOAT_BOTTOMLEFT_DIRT = simplegui.load_image("https://i.imgur.com/F41NxFT.png")
FLOAT_BOTTOM_DIRT = simplegui.load_image("https://i.imgur.com/gwREAde.png")
FLOAT_BOTTOMRIGHT_DIRT = simplegui.load_image("https://i.imgur.com/ztpl2Mm.png")

#world 2
RIGHT_FLOAT_SAND = simplegui.load_image("https://i.imgur.com/9GMDQws.png")
LEFT_FLOAT_SAND = simplegui.load_image("https://i.imgur.com/tT0kG00.png")
FLOAT_SAND = simplegui.load_image("https://i.imgur.com/JqA9Om1.png")
SAND_PLATFORM = simplegui.load_image("https://i.imgur.com/lDh5dN1.png")
SAND = simplegui.load_image("https://i.imgur.com/tyMiPJU.png")
CONNECTED_SAND = simplegui.load_image("https://i.imgur.com/tU9E75B.png")
LEFT_SAND = simplegui.load_image("https://i.imgur.com/NWYtbQJ.png")
RIGHT_SAND = simplegui.load_image("https://i.imgur.com/Hv8oev0.png")
LEFT_SAND_SURFACELESS = simplegui.load_image("https://i.imgur.com/5eeYLn7.png")
RIGHT_SAND_SURFACELESS = simplegui.load_image("https://i.imgur.com/92NUa2C.png")
BOTTOM_LEFT_SAND = simplegui.load_image("https://i.imgur.com/LpcGjU5.png")
BOTTOM_RIGHT_SAND = simplegui.load_image("https://i.imgur.com/Y3SfkDk.png")
LEFT_WALL_SAND = simplegui.load_image("https://i.imgur.com/4Z0JtHp.png")
RIGHT_WALL_SAND = simplegui.load_image("https://i.imgur.com/tyMiPJU.png")
FLOAT_BOTTOMLEFT_SAND = simplegui.load_image("https://i.imgur.com/A0z823u.png")
FLOAT_BOTTOMRIGHT_SAND = simplegui.load_image("https://i.imgur.com/6vY2zQZ.png")
FLOAT_BOTTOM_SAND = simplegui.load_image("https://i.imgur.com/HmEn37a.png")
DOORS = simplegui.load_image("https://i.imgur.com/48PwrI9.png")
PRESSUREPLATE = simplegui.load_image("https://i.ibb.co/t8km5kz/spritesheet-1.png")

TILE_SIZE = [80, 80]
BUTTON_SIZE = 788, 788
WIDTH = 1280
HEIGHT = 720
GRAVITY = 0.5
GRAVITYMAX = 10
b_kingtouchcount = 0
level_select_volume = 0
circle_time = 0
delay = 0
upgradeanimation = 0
displayedmessage = ''
displayedmessage2 = ''
upgrademenu = False
legalmove = True
world_1_buttons = [LVL1_BUTTON, LVL2_BUTTON, LVL3_BUTTON, LVL4_BUTTON, LVL5_BUTTON, LVL6_BUTTON, LVL7_BUTTON, LVL8_BUTTON]
world_2_buttons = [LVL9_BUTTON, LVL10_BUTTON, LVL11_BUTTON, LVL12_BUTTON, LVL13_BUTTON, LVL14_BUTTON, LVL15_BUTTON, LVL16_BUTTON]
uncompleted_buttons_1 = [LVL2_UNCOMPLETED, LVL3_UNCOMPLETED, LVL4_UNCOMPLETED, LVL5_UNCOMPLETED, LVL6_UNCOMPLETED, LVL7_UNCOMPLETED, LVL8_UNCOMPLETED]
uncompleted_buttons_2 = [LVL9_UNCOMPLETED, LVL10_UNCOMPLETED, LVL11_UNCOMPLETED, LVL12_UNCOMPLETED, LVL13_UNCOMPLETED, LVL14_UNCOMPLETED, LVL15_UNCOMPLETED, LVL16_UNCOMPLETED]
completed_buttons_1 = [LVL1_COMPLETED, LVL2_COMPLETED, LVL3_COMPLETED, LVL4_COMPLETED, LVL5_COMPLETED, LVL6_COMPLETED, LVL7_COMPLETED, LVL8_COMPLETED]
completed_buttons_2 = [LVL9_COMPLETED, LVL10_COMPLETED, LVL11_COMPLETED, LVL12_COMPLETED, LVL13_COMPLETED, LVL14_COMPLETED, LVL15_COMPLETED, LVL16_COMPLETED]
level_selects = ['level select 1', 'level select 2', 'level select 3', 'upgrade piece']
doors = ['d']
crates = ['c1', 'c2', 'c3', 'c4', 'c5']
levels_unlocked = ['upgrade piece', 'level 1']
levels_completed = []
block_list = []
crate_list = []
platform_list = []
playerclicks = []
w_kings = []
w_rooks = []
w_knights = []
w_bishops = []
w_pawns = []
w_queens = []
b_king = []
piece_list = []
piece_positions = []
availablemoves = []
music_list = []
current_level = ''
block_numbers = list(range(1, 34)) + crates
tutorial_list = []

for i in range(1, 12):
    tutorial_list.append('tutorial ' + str(i))
tutorial_list2 = []
for i in range(10, 33):
    tutorial_list2.append('tutorial ' + str(i))
tutorial_list3 = ['tutorial 24 hint', 'tutorial 24 hint 2']
for i in range(23, 25):
    tutorial_list3.append('tutorial ' + str(i))
tutorial_list4 = ['tutorial 24 hint', 'tutorial 24 hint 2']
for i in range(25, 30):
    tutorial_list4.append('tutorial ' + str(i))

world_1 = []
for i in range(1, 9):
    world_1.append('level ' + str(i))
world_2 = []
for i in range(9, 17):
    world_2.append('level ' + str(i))
world_2.append(['upgrade piece'])
fulltutorial_list = tutorial_list + tutorial_list2 + tutorial_list3    
levels = world_1 + world_2 + fulltutorial_list + ['upgrade piece']
#levels
lvl_1 = []
lvl_2 = []
lvl_3 = []
lvl_4 = []
lvl_5 = []
lvl_6 = []
lvl_7 = []
lvl_8 = []
tutorial1 = [] 
tutorial2 = []
pressure_plate_list = []

def new_game():
    global cguidedialogues, dialogue_tick, button_levels1, button_levels2
    global scene_tutorials, lvlbutton_x, lvlbutton_y, button_start_game
    global button_tutorial, button_guide, button_guide1, button_guide2
    global button_hint1, button_restartlvl, button_levelback
    global button_tutoriallevelback, button_menu, button_lvlselect1
    global button_next1, button_next2, button_queen, button_bishop
    global button_rook, button_knight, scene_menu, scene_lvlselect1
    global scene_lvlselect2, scene_lvl, scene_upgradepiece, current_scene
    global menu_effects, world_1_sfx, world_2_sfx, tutorial_sfx, music_list
    global cguidemessages, button_tutorials, button_width, button_height
    global lvlbutton_width, lvlbutton_height, selectionbgrd_width, selectionbgrd_height
    cguidedialogues = []
    dialogue_tick = 1
    button_tutorials = []
    button_levels1 = []
    button_levels2 = []
    scene_tutorials = []
    lvlbutton_x = WIDTH/2 - 380
    lvlbutton_y = HEIGHT/2 - 93
    button_width,button_height = IMG_SIZES[START_BUTTON]
    lvlbutton_width, lvlbutton_height = IMG_SIZES[LVL1_BUTTON]
    selectionbgrd_width, selectionbgrd_height = IMG_SIZES[SELECTIONBGRD]
    #menu buttons
    button_start_game = Button([WIDTH/2,HEIGHT/2],
                               (button_width/2, button_height/2), 
                               START_BUTTON, 'level select 1')   

    button_tutorial = Button([WIDTH/2,HEIGHT/2 + 200],
                               (button_width/2, button_height/2), 
                               TUTORIAL_BUTTON, 'tutorial 1') 
    #tutorial buttons
    button_guide = Button([WIDTH/2 - 570,HEIGHT/2 - 310],
                          (lvlbutton_width/9, lvlbutton_height/9),
                          GUIDE_BUTTON,
                          'guide')   
    
    button_guide1 = Button([WIDTH/2, HEIGHT/2],
                           (button_width/4,
                            button_height/4),
                           NEXT_BUTTON, 'guide 2')
    
    button_guide2 = Button([WIDTH/2,HEIGHT/2],
                           (button_width/4,
                            button_height/4),
                           NEXT_BUTTON,
                           current_level)
    
    button_hint1 = Button([WIDTH/2 + 500,HEIGHT/2 - 310],
                          (button_width/5, button_height/5),
                          HINT_BUTTON,
                          'tutorial 35 hint') 
    
    button_restartlvl = Button([WIDTH/2 - 450,HEIGHT/2 - 310],
                               (lvlbutton_width/9,
                                lvlbutton_height/9),
                               RESTART_BUTTON,
                               'tutorial 24')
    
    #level select and level buttons
    button_levelback = Button([WIDTH/2 - 570,HEIGHT/2 - 310],
                              (lvlbutton_width/9,
                               lvlbutton_height/9),
                              BACK_BUTTON,
                              'level select 1') 
    
    button_tutoriallevelback = Button([WIDTH/2 - 570,HEIGHT/2 - 310],
                                      (lvlbutton_width/9,
                                       lvlbutton_height/9),
                                      BACK_BUTTON, 'menu') 
    
    button_menu = Button([WIDTH/2 - 475,HEIGHT/2 - 280],
                         (button_width/4,
                          button_height/4),
                         MENU_BACK_BUTTON,
                         'menu') 
    
    button_lvlselect1 = Button([WIDTH/2 - 475,HEIGHT/2 - 280],
                               (button_width/4, button_height/4),
                               MENU_BACK_BUTTON,
                               'level select 1') 
    
    button_next1 = Button([WIDTH/2 + 490,HEIGHT/2 - 280],
                          (button_width/4, button_height/4),
                          NEXT_BUTTON,
                          'level select 2') 
    
    button_next2 = Button([WIDTH/2 + 490,HEIGHT/2 - 280],
                          (button_width/4,
                           button_height/4),
                          NEXT_BUTTON,
                          'level select 3') 
    
    #pawn promotion buttons
    button_queen = Button([WIDTH/2 - 305,HEIGHT/2],
                          (lvlbutton_width/4+15,
                           lvlbutton_height/4-30),
                          NOTHING, current_level)
    
    button_bishop = Button([WIDTH/2 - 96,HEIGHT/2],
                           (lvlbutton_width/4+3,
                            lvlbutton_height/4-30),
                           NOTHING, current_level)
    
    button_rook = Button([WIDTH/2 + 108,HEIGHT/2],
                         (lvlbutton_width/4+3,
                          lvlbutton_height/4-30),
                         NOTHING, current_level)
    
    button_knight = Button([WIDTH/2 + 312,HEIGHT/2],
                           (lvlbutton_width/4+3,
                            lvlbutton_height/4-30),
                           NOTHING,
                           current_level)
    #different scenes
    scene_menu = Scene('menu',
                       [button_start_game, button_tutorial])
    scene_lvlselect1 = Scene('level select 1',
                             button_levels1 + [button_menu] + [button_next1])
    scene_lvlselect2 = Scene('level select 2',
                             button_levels2 + [button_lvlselect1] + [button_next2])
    scene_lvl = Scene('level 1',
                      [button_restartlvl, button_levelback])
    scene_upgradepiece = Scene('upgrade piece',
                               [button_restartlvl, button_levelback, button_queen, button_bishop, button_rook, button_knight])
    current_scene = 'menu'    
    
    
    menu_effects = Musicsfx(LEVEL_SELECT_MUSIC, 0)
    world_1_sfx = Musicsfx(WORLD1_MUSIC, 0)
    world_2_sfx = Musicsfx(WORLD2_MUSIC, 0)
    tutorial_sfx = Musicsfx(TUTORIAL_MUSIC, 0)

    music_list = [menu_effects, world_1_sfx, tutorial_sfx, world_2_sfx]
    cguidemessages = [
        '',
        "Hey there! Welcome to the world  of Chess Climb!",
        "The name is Sir Chesster III.    Nice to meet you :)",
        "Anyways, let's jump straight     into the basics!",
        "Each level has a black king in   a designated spot.",
        "Your goal is simple.             ELIMINATE  him.",
        "Try it out! Click on your white  king to select it!",
        "The black dots are the piece's   available moves.",
        "Also, the game remembers what    you've selected.",
        "So don't worry about repeatedly  selecting the piece as you move.",
        "Great job! You ELIMINATED him    real good!",
        "Let's make sure you're familiar  with the rules of chess.",
        "Here are the movement patterns   for each piece in the game.",
        "Great! You now know how chess    works!",
        "Now let's figure out the         climbing part of chess climb!",
        "Chess pieces in this game are    affected by gravity.",
        "Their paths can blocked by       pieces or blocks!",
        'However, knights can "jump" over these pieces and blocks!',
        "One last thing! Your pieces can  fall on the king to kill it. ",
        "Now try this level! ",
        "",
        "The king is blocking the way of  the rook!",
        "Try finding a way to clear the   rook's path!",
        "Great work! ",
        "You're now ready to be a chess   climbing champion! ",
        "Good luck on your journey! "
    ]
    #stores chess guide's dialogues
    for i in range(28):
        if i == 10 or i == 14:
            cguidedialogues.append(None)
        else:
            cguidedialogues.append(Dialogue([WIDTH / 2, HEIGHT / 2],
                                            cguidemessages[dialogue_tick-1]))
            dialogue_tick += 1
            
    #allows player to click to go through tutorial dialogues
    for i in range(1,32):
        if i == 15 or i == 16:
            button_tutorials.append(Button([WIDTH/2, HEIGHT/2],
                                           (button_width/4,
                                            button_height/4),
                                           NEXT_BUTTON,
                                           'tutorial ' + str(i + 1)))

        elif i == 27:
            button_tutorials.append(Button([WIDTH/2, HEIGHT/2],
                                           (WIDTH, HEIGHT),
                                           NOTHING,
                                           'menu'))

        elif i == 28:
            button_tutorials.append(Button([WIDTH/2 + 500,HEIGHT/2 - 310],
                                           (button_width/5,
                                            button_height/5),
                                           HINT_BUTTON,
                                           'tutorial 24 hint'))

        elif i == 29:
            button_tutorials.append(Button([WIDTH/2,HEIGHT/2],
                                           (WIDTH, HEIGHT),
                                           NOTHING,
                                           'tutorial 24 hint 2'))
        elif i == 30:
            button_tutorials.append(Button([WIDTH/2,HEIGHT/2],
                                           (WIDTH, HEIGHT),
                                           NOTHING,
                                           'tutorial 24'))
        else:
            button_tutorials.append(Button([WIDTH/2,HEIGHT/2],
                                           (WIDTH, HEIGHT),
                                           NOTHING,
                                           'tutorial ' + str(i + 1)))

    
    #creates buttons for levels in world 1
    for i in range(1,9):
        if i == 1:
            lvlbutton_x = WIDTH/2 - 450
            lvlbutton_y = HEIGHT/2 - 93
        elif i == 5:
            lvlbutton_x = WIDTH/2 - 450
            lvlbutton_y = HEIGHT/2 + 180
        button_levels1.append(Button([lvlbutton_x,lvlbutton_y],
                                     (lvlbutton_width/4,
                                      lvlbutton_height/4),
                                     world_1_buttons[i-1],
                                     'level ' + str(i)))
        lvlbutton_x += 300

    
    #creates buttons for levels in world 2
    for i in range(9, 13):
            if i == 9:
                lvlbutton_x = WIDTH/2 - 450
                lvlbutton_y = HEIGHT/2
            button_levels2.append(Button([lvlbutton_x,lvlbutton_y],
                                         (lvlbutton_width/4,
                                          lvlbutton_height/4),
                                         world_2_buttons[i-9],
                                         'level ' + str(i)))
            lvlbutton_x += 300
    
    
    for i in range(1,32):
        if i == 25:
            scene_tutorials.append(Scene('tutorial ' + str(i),
                                         [button_restartlvl, button_guide, button_tutorials[i+2]]))
        elif i == 30:
             scene_tutorials.append(Scene('tutorial 34 hint',
                                          [button_tutorials[i-2]]))
        elif i == 31:
             scene_tutorials.append(Scene('tutorial 34 hint 2',
                                          [button_tutorials[i-2]]))    
        else: 
            scene_tutorials.append(Scene('tutorial ' + str(i),
                                         [button_tutorials[i-2]] if i != 11 else []))
            
    draw_scene = scene_menu
    
def new_level():
    global w_kings, w_bishops, w_rooks, w_knights, w_queens, w_pawns
    global block_list, piece_list, crate_list
    global piece_positions, platform_list, b_king, b_kingtouchcount
    global door_list, availablemoves, availablemovesanimated, pressure_plate_list
    global upgradeanimation
    w_kings = []
    w_bishops = []
    w_rooks = []
    w_knights = []
    w_queens = []
    w_pawns = []
    block_list = []
    piece_list = []
    crate_list = []
    piece_positions = []
    platform_list = []
    b_king = []
    b_kingtouchcount = 0
    door_list = []
    availablemoves = []
    availablemovesanimated = []
    pressure_plate_list = []
    upgradeanimation = 0
    
def load_level(level):
    global tutorial1, tutorial2, tutorial3, world, current_lvl, lvl_1
    global lvl_2, lvl_3, lvl_4, lvl_5, lvl_6, lvl_7, lvl_8, lvl_9
    if level in tutorial_list:
        tutorial1 = [
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 'bk', 0, 0],
            [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1],
            [2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2]]
        world = Stage(tutorial1)
        current_lvl = tutorial1
    if level in tutorial_list2:
        tutorial2 = [
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
            [0, 0, 'wk', 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 'bk', 0, 0],
            [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1],
            [2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2]]
        world = Stage(tutorial2)
        current_lvl = tutorial2
    if level in tutorial_list3:
        new_level()
        cguidedialogues[23].dialoguepos = 0
        cguidedialogues[24].dialoguepos = 0
        tutorial3 = [
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
            [0, 'wr', 0, 'wk', 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
            [1, 1, 1, 1, 4, 0, 0, 0, 0, 3, 1, 1, 1, 1, 4, 0],
            [2, 2, 2, 2, 5, 0, 0, 0, 0, 6, 2, 2, 2, 2, 5, 'bk'],
            [2, 2, 2, 2, 5, 0, 0, 0, 0, 6, 2, 2, 2, 2, 12, 10],
            [2, 2, 2, 2, 12, 10, 1, 1, 11, 13, 2, 2, 2, 2, 2, 2]]
        if current_scene not in tutorial_list4:
            world = Stage(tutorial3)                                
            current_lvl = tutorial3
    if level == 'level 1':

        #world 1

        #0 = air
        #1 = default ground texture
        #2 = connected ground texture
        #3 = left edge ground texture
        #4 = right edge grond texture
        #5 surfaceless left ground texture
        #6 surfaceless right ground texture
        #7 floating left edge grass
        #8 floating grass
        #9 floating right edge grass
        #10 grass coming from left wall
        #11 grass coming from right wall
        #12 dirt connecting grass to bottom right of wall
        #13 dirt connecting grass to bottom left of wall
        #14 floating left edge bottom dirt
        #15 floating bottom dirt
        #16 floating right edge bottom dirt
        lvl_1 = [
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 'bk'],
            [1, 1, 1, 1, 4, 0, 0, 0, 0, 3, 1, 1, 1, 1, 1, 1],
            [2, 2, 2, 2, 5, 0, 0, 0, 0, 6, 2, 2, 2, 2, 2, 2],
            [2, 2, 2, 2, 5, 0, 0, 0, 'wb', 6, 2, 2, 2, 2, 2, 2],
            [2, 2, 2, 2, 12, 10, 1, 1, 11, 13, 2, 2, 2, 2, 2, 2]]

        world = Stage(lvl_1)
        current_lvl = lvl_1
    if level == 'level 2':
            lvl_2 = [
                [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
                [0, 0, 0, 0, 0, 'wr', 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
                [8, 8, 8, 8, 8, 8, 8, 8, 9, 0, 7, 8, 8, 8, 8, 8],
                [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
                [8, 8, 9, 0, 7, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8],
                [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
                [8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 9, 0, 7, 8],
                [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 'bk', 0, 0],
                [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 7, 8, 9, 0]]


            world = Stage(lvl_2)
            current_lvl = lvl_2

    if level == 'level 3':

            lvl_3 = [
                [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
                [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
                [0, 0, 0, 0, 0, 0, 0, 0, 'bk', 0, 0, 0, 0, 0, 0, 0],
                [8, 8, 8, 8, 8, 8, 8, 8, 8, 9, 0, 0, 0, 0, 0, 0],
                [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 3, 4, 0, 0, 0],
                [0, 'wb', 0, 0, 0, 0, 0, 'wr', 'wk', 0, 0, 6, 5, 0, 0, 0],
                [1, 1, 1, 1, 4, 0, 0, 3, 4, 0, 0, 6, 5, 0, 0, 0],
                [2, 2, 2, 2, 5, 0, 0, 6, 5, 0, 0, 6, 5, 0, 0, 0],
                [2, 2, 2, 2, 12, 10, 11, 13, 12, 10, 11, 13, 12, 10, 1, 1]]



            world = Stage(lvl_3)
            current_lvl = lvl_3

    if level == 'level 4':

        lvl_4 = [
                [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
                [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
                [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0],
                [7, 8, 8, 8, 8, 8, 9, 0, 0, 3, 4, 0, 0, 0, 2, 0],
                [0, 0, 0, 0, 0, 0, 0, 0, 0, 6, 5, 0, 0, 0, 2, 0],
                ['wkt', 0, 0, 0, 0, 0, 0, 0, 0, 6, 5, 0, 0, 0, 2, 0],
                ['wk', 0, 0, 'wb', 0, 3, 4, 0, 0, 6, 5, 0, 0, 0, 15, 'bk'],
                [1, 1, 1, 1, 11, 13, 12, 10, 11, 13, 12, 10, 1, 1, 1, 1],
                [2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2]]

        world = Stage(lvl_4)
        current_lvl = lvl_4

    if level == 'level 5':
        lvl_5 = [
                [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
                [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
                [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 3, 4, 0],
                [0, 0, 0, 0, 0, 0, 0, 3, 1, 4, 0, 0, 0, 6, 5, 0],
                [0, 0, 0, 1, 0, 0, 0, 6, 2, 5, 0, 0, 0, 6, 5, 0],
                [0, 0, 0, 2, 0, 0, 0, 6, 2, 5, 0, 0, 0, 6, 5, 0],
                [0, 'wkt', 0, 15, 'wkt', 'wk', 0, 6, 2, 5, 'wb', 'wr', 0, 6, 5, 'bk'],
                [1, 1, 1, 1, 1, 1, 11, 13, 2, 12, 10, 1, 11, 13, 12, 10],
                [2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2]]


        world = Stage(lvl_5)
        current_lvl = lvl_5

    if level == 'level 6':
        lvl_6 = [
                [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
                [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
                [0, 'wr', 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 7, 8, 8, 9],
                [1, 1, 4, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 'bk'],
                [2, 2, 5, 0, 0, 0, 0, 0, 0, 0, 0, 0, 3, 1, 1, 1],
                [2, 2, 5, 0, 0, 0, 0, 0, 0, 0, 0, 0, 6, 2, 2, 2],
                [2, 2, 5, 0, 0, 0, 0, 0, 0, 0, 0, 0, 6, 2, 2, 2],
                [2, 2, 5, 'wkt', 0, 'wb', 0, 'wr', 0, 'wkt', 0, 'wkt', 6, 2, 2, 2],
                [2, 2, 12, 10, 1, 1, 1, 1, 1, 1, 1, 11, 13, 2, 2, 2]]
        world = Stage(lvl_6)
        current_lvl = lvl_6
    if level == 'level 7':
        lvl_7 = [
                [0, 0, 0, 0, 0, 0, 'wkt', 0, 0, 0, 0, 0, 0, 0, 'wk', 0],
                [1, 1, 1, 1, 1, 1, 4, 0, 3, 1, 1, 1, 1, 1, 1, 1],
                [15, 15, 15, 15, 15, 15, 5, 0, 6, 15, 15, 15, 15, 15, 15, 15],
                [0, 0, 0, 0, 0, 0, 5, 0, 6, 0, 0, 0, 0, 0, 0, 'wr'],
                [0, 3, 4, 0, 0, 0, 5, 0, 6, 0, 7, 8, 8, 8, 8, 9],
                [0, 6, 5, 0, 0, 0, 5, 0, 6, 0, 0, 0, 0, 0, 0, 0],
                [0, 6, 5, 0, 0, 0, 16, 'c2', 14, 7, 8, 8, 8, 8, 9, 0],
                ['bk', 6, 5, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
                [11, 13, 12, 10, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1]]
        world = Stage(lvl_7)
        current_lvl = lvl_7


    if level == 'level 8':
        lvl_8 = [
                [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
                [0, 0, 0, 0, 0, 'wkt', 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
                [1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 1, 1, 1, 1],
                [15, 2, 0, 2, 0, 2, 0, 2, 2, 2, 2, 0, 2, 15, 2, 2],
                [0, 2, 2, 2, 0, 2, 2, 2, 15, 2, 2, 15, 2, 0, 2, 2],
                [2, 15, 2, 2, 15, 2, 2, 2, 0, 15, 2, 0, 2, 15, 2, 2],
                [2, 0, 15, 15, 'wb', 15, 15, 15, 0, 0, 2, 15, 2, 0, 2, 2],
                [2, 2, 'bk', 0, 2, 0, 0, 0, 2, 2, 2, 0, 2, 2, 2, 2],
                [15, 15, 15, 15, 15, 15, 15, 15, 15, 15, 15, 15, 15, 15, 15, 15]]
        world = Stage(lvl_8)
        current_lvl = lvl_8
    #world 2

    #17 = sand
    #18 = left edge sand texture
    #19 = right edge sand texture
    #20 = surfaceless left sand texture
    #21 = surfaceless right sand texture
    #22 = sand coming from left wall
    #23 = sand coming from right wall
    #24 = sand connecting grass to bottom right of wall
    #25 = sand connecting grass to bottom left of wall
    #26 = floating left edge bottom sand
    #27 = floating right edge bottom sand   
    #28 = floating bottom sand
    #29 = connected sand texture
    #30 = sand platform
    #31 = floating sand middle
    #32 = left edge floating sand
    #33 = right edge floating sand
    if level == 'level 9':
        lvl_9 = [
                [0, 0, 0, 30, 0, 0, 0, 0, 0, 20, 21, 0, 0, 0, 0, 0],
                [0, 0, 0, 30, 0, 0, 0, 0, 0, 20, 21, 0, 0, 0, 0, 0],
                [0, 0, 0, 30, 0, 0, 0, 0, 0, 20, 21, 0, 'bk', 0, 0, 0],
                [0, 0, 0, 30, 0, 0, 0, 0, 0, 20, 21, 0, 18, 19, 0, 0],
                [0, 0, 0, '30p', 0, 0, 0, 0, 0, 26, 27, 0, 26, 27, 0, 0],
                [0, 0, 0, 17, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 'wr'],
                [0, 0, 0, 0, 0, 0, 0, 0, 0, 18, 17, 17, 17, 17, 17, 17],
                [17, 17, 17, 17, 19, 0, 18, 19, 0, 20, 29, 29, 29, 29, 29, 29],
                [29, 29, 29, 29, 25, 17, 24, 25, 17, 24, 29, 29, 29, 29, 29, 29]]
        world = Stage(lvl_9)
        current_lvl = lvl_9
    if level == 'level 10':
        lvl_10 = [
                [21, 0, 0, 0, 0, 0, 0, 0, 0, 0, 26, 27, 0, 0, 0, 0],
                [21, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 32, 33, 0, 0, 0],
                [21, 0, 18, 19, 0, 32, 33, 0, 0, 32, 33, 0, 0, 0, 0, 0],
                [27, 'c2', 20, 25, 19, 0, 0, 0, 0, 0, 0, 0, 0, 0, 32, 33],
                ['bk', 0, 20, 29, 21, 0, 0, 32, 33, 0, 0, 0, 0, 0, 0, 0],
                [19, 0, 20, 29, 21, 0, 0, 0, 0, 0, 0, 0, 18, 19, 0, 0],
                [27, 0, 20, 29, 21, 0, 0, 0, 0, 0, 0, 0, 20, 25, 22, 17],
                [0, 0, 20, 29, 21, 0, 'wq', 0, 0, 0, 0, 'wkt', 20, 29, 29, 29],
                [18, 19, 26, 28, 27, 18, 17, 17, 17, 17, 17, 19, 20, 29, 29, 29]]


        world = Stage(lvl_10)
        current_lvl = lvl_10
    
    if level == 'level 11':
        lvl_11 = [
                [0, 0, 0, 0, 0, 0, 0, 0, 28, 0, 0, 0, 18, 19, 0, 0],
                [0, 0, 0, 0, 0, 0, 0, 0, 'd', 0, 0, 0, 26, 27, 0, 0],
                ['p', 32, 33, 0, 0, 0, 0, 0, 18, 19, 0, 17, 0, 0, 0, 0],
                [33, 0, 0, 0, 0, 0, 0, 0, 20, 21, 0, 28, 0, 'bk', 0, 0],
                [0, 32, 33, 0, 0, 0, 0, 0, 20, 21, 0, 18, 17, 17, 17, 19],
                [0, 0, 0, 0, 32, 31, 33, 0, 20, 21, 0, 20, 29, 29, 29, 21],
                [0, 0, 0, 0, 0, 0, 0, 0, 26, 27, 0, 20, 29, 29, 29, 21],
                [0, 0, 0, 0, 0, 'wb', 0, 'wq', 0, 0, 0, 20, 29, 29, 29, 21],
                [17, 17, 17, 17, 17, 17, 17, 17, 17, 17, 17, 26, 29, 29, 29, 27]]


        world = Stage(lvl_11)
        current_lvl = lvl_11
        
    if level == 'level 12':
        lvl_12 = [
                [0, 0, 0, 17, 0, 0, 0, 0, '30r', 0, 0, 20, 21, 0, 0, 0],
                [0, 0, 0, 0, 0, 0, 18, 19, 30, 0, 0, 20, 21, 30, 'bk', 0],
                [0, 0, 0, 17, 0, 0, 26, 27, 30, 0, 0, 20, 21, 0, 17, 0],
                [0, 0, 0, 28, 0, 0, 0, 0, 'wp', 0, 0, 20, 21, 0, 0, 0],
                [0, 0, 0, 0, 18, 17, 17, 17, 17, 17, 19, 20, 21, 0, 0, 0],
                [0, 0, 0, 0, 26, 28, 28, 28, 28, 28, 27, 26, 27, 18, 19, 0],
                [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
                ['wb', 0, 0, 0, 0, 0, 18, 17, 17, 17, 17, 17, 17, 17, 17, 17],
                [17, 17, 17, 17, 17, 23, 24, 29, 29, 29, 29, 29, 29, 29, 29, 29]]

        world = Stage(lvl_12)
        current_lvl = lvl_12

def update_buttons():
    global current_scene, button_levelback, button_guide, button_guide2, button_restartlvl, scene_lvl, scene_guide1
    global scene_guide2, scene_tutorial34, world_1_buttons, button_levels1, button_levels2
    
    button_guide2 = Button([WIDTH/2, HEIGHT/2],
                           (button_width/4,
                            button_height/4),
                           NEXT_BUTTON,
                           current_level)
    
    if current_scene in world_1:
        button_levelback = Button([WIDTH/2 - 570,HEIGHT/2 - 310],
                                  (lvlbutton_width/9,
                                   lvlbutton_height/9),
                                  BACK_BUTTON,
                                  'level select 1') 
    elif current_scene in world_2:
        button_levelback = Button([WIDTH/2 - 570,HEIGHT/2 - 310],
                                  (lvlbutton_width/9, lvlbutton_height/9),
                                  BACK_BUTTON,
                                  'level select 2') 
    
    if current_scene == 'tutorial 34':
        button_restartlvl = Button([WIDTH/2 - 450,HEIGHT/2 - 310],
                                   (lvlbutton_width/9, lvlbutton_height/9),
                                   RESTART_BUTTON,
                                   'tutorial 34')
        button_guide = Button([WIDTH/2 - 530,HEIGHT/2 - 310],
                              (lvlbutton_width/9,
                               lvlbutton_height/9),
                              GUIDE_BUTTON,
                              'guide') 
    else:
        button_restartlvl = Button([WIDTH/2 - 450,HEIGHT/2 - 310],
                                   (lvlbutton_width/9,
                                    lvlbutton_height/9),
                                   RESTART_BUTTON,
                                   current_scene)
        button_guide = Button([WIDTH/2 - 330,HEIGHT/2 - 310],
                              (lvlbutton_width/9,
                               lvlbutton_height/9),
                              GUIDE_BUTTON,
                              'guide') 
        
    scene_lvl = Scene('level 1', [button_restartlvl, button_levelback])
    scene_guide1 = Scene('guide 1', [button_guide1])
    scene_guide2 = Scene('guide 2', [button_guide2])
    scene_tutorial34 = Scene('tutorial 34', [button_restartlvl, button_guide,button_hint1])
   
    
    for i in range(1, 9):
        if world_1[i-1] in levels_completed:
            world_1_buttons[i-1] = completed_buttons_1[i-1]
        elif world_1[i-1] in levels_unlocked:
            if i != 1:
                world_1_buttons[i-1] = uncompleted_buttons_1[i-2]
    
    for i in range(9, 17):
        if world_2[i-9] in levels_completed:
            world_2_buttons[i-9] = completed_buttons_2[i-9]
        elif world_2[i-9] in levels_unlocked:
            world_2_buttons[i-9] = uncompleted_buttons_2[i-9]

    button_levels1 = []
    for i in range(1,9):
        if i == 1:
            lvlbutton_x = WIDTH/2 - 450
            lvlbutton_y = HEIGHT/2 - 93
        elif i == 5:
            lvlbutton_x = WIDTH/2 - 450
            lvlbutton_y = HEIGHT/2 + 180
        button_levels1.append(Button([lvlbutton_x,lvlbutton_y],
                                     (lvlbutton_width/4,
                                      lvlbutton_height/4),
                                     world_1_buttons[i-1],
                                     'level ' + str(i)))
        lvlbutton_x += 300
        
    button_levels2 = []
    #creates buttons for levels in world 2
    for i in range(9, 13):
        if i == 9:
            lvlbutton_x = WIDTH/2 - 450
            lvlbutton_y = HEIGHT/2 
        button_levels2.append(Button([lvlbutton_x,lvlbutton_y],
                                     (lvlbutton_width/4,
                                      lvlbutton_height/4),
                                     world_2_buttons[i-9],
                                     'level ' + str(i)))
        lvlbutton_x += 300
        
def update_image_dictionary():
    global IMG_SIZES
    IMG_SIZES = {START_BUTTON: (958, 383),
             TUTORIAL_BUTTON: (958, 383),
             LVL1_BUTTON: (BUTTON_SIZE),
             LVL2_BUTTON: (BUTTON_SIZE),
             LVL3_BUTTON: (BUTTON_SIZE),
             LVL4_BUTTON: (BUTTON_SIZE),
             LVL5_BUTTON: (BUTTON_SIZE),
             LVL6_BUTTON: (BUTTON_SIZE),
             LVL7_BUTTON: (BUTTON_SIZE),
             LVL8_BUTTON: (BUTTON_SIZE),
             SELECTIONBGRD: (1280, 720),
             RESTART_BUTTON: (BUTTON_SIZE),
             MENU_BACK_BUTTON: (958,383),
             BACK_BUTTON: (BUTTON_SIZE),
             WHITE_KING: (BUTTON_SIZE),
             WORLD1BGRD: (1280, 720),
             CRATE1: (230, 230),
             NOTHING: (107, 107),
             NEXT_BUTTON: (958, 383),
             GUIDE_BUTTON: (BUTTON_SIZE),
             HINT_BUTTON: (958, 383),
             LVL1_COMPLETED: (BUTTON_SIZE),
             LVL2_UNCOMPLETED: (BUTTON_SIZE),
             LVL2_COMPLETED: (BUTTON_SIZE),
             LVL3_UNCOMPLETED: (BUTTON_SIZE),
             LVL3_COMPLETED: (BUTTON_SIZE),
             LVL4_UNCOMPLETED: (BUTTON_SIZE),
             LVL4_COMPLETED: (BUTTON_SIZE),
             LVL5_UNCOMPLETED: (BUTTON_SIZE),
             LVL5_COMPLETED: (BUTTON_SIZE),
             LVL6_UNCOMPLETED: (BUTTON_SIZE),
             LVL6_COMPLETED: (BUTTON_SIZE),
             LVL7_UNCOMPLETED: (BUTTON_SIZE),
             LVL7_COMPLETED: (BUTTON_SIZE),
             LVL8_UNCOMPLETED: (BUTTON_SIZE),
             LVL8_COMPLETED: (BUTTON_SIZE),
             LVL9_UNCOMPLETED: (BUTTON_SIZE),
             LVL9_COMPLETED: (BUTTON_SIZE),
             LVL10_UNCOMPLETED: (BUTTON_SIZE),
             LVL10_COMPLETED: (BUTTON_SIZE),
             LVL11_UNCOMPLETED: (BUTTON_SIZE),
             LVL11_COMPLETED: (BUTTON_SIZE),
             LVL12_UNCOMPLETED: (BUTTON_SIZE),
             LVL12_COMPLETED: (BUTTON_SIZE),
             LVL13_UNCOMPLETED: (BUTTON_SIZE),
             LVL13_COMPLETED: (BUTTON_SIZE),
             LVL14_UNCOMPLETED: (BUTTON_SIZE),
             LVL14_COMPLETED: (BUTTON_SIZE),
             LVL15_UNCOMPLETED: (BUTTON_SIZE),
             LVL15_COMPLETED: (BUTTON_SIZE),
             LVL16_UNCOMPLETED: (BUTTON_SIZE),
             LVL16_COMPLETED: (BUTTON_SIZE),
             DOORS: (BUTTON_SIZE),
             PRESSUREPLATE: (640, 640),
             NEWMOVE: (BUTTON_SIZE),
             BLACK_CIRCLES: (BUTTON_SIZE)} 
    
def find_available_moves(piece):
    global offsetx, offsety, TILE_SIZE, availablemoves, block_numbers, legalmove
    global availablemovesanimated, current_lvl
    availablemoves = []
    availablemovesanimated = []
    rows = 9
    cols = 16
    if piece.falling:
        availablemoves = []
        availablemovesanimated = []
    else:
        availablemoves = []
        #Stores the guide circles for the pieces in a list
        for row in range(0, rows):
            for col in range(0, cols):
                new_circle_pos = [col * TILE_SIZE[0] + offsetx, row * TILE_SIZE[1] + offsety] 
                equal_dis = abs(row - piece.row) == abs(col - piece.col)
                
                if current_lvl[row][col] not in block_numbers:
                    if piece in w_rooks:
                        if row == piece.row or col == piece.col:
                            rookobstructioncheck(row, col)
                            pieceobstructioncheck(piece.row, piece.col, row, col)
                            if legalmove:
                                if new_circle_pos != piece.pos:
                                    if current_lvl[row][col] != 'd':
                                        availablemoves.append(new_circle_pos)                               
                    elif piece in w_bishops:
                        legalmove = True
                        if equal_dis and abs(row - piece.row) > 0 or row == piece.row and col == piece.col:
                            #checks if piece or block is blocking the path of bishop
                            bishopobstructioncheck(row, col)
                            pieceobstructioncheck(piece.row, piece.col, row, col)
                            if legalmove:
                                #if move is available then a guide circle is placed where the bishop can move
                                if new_circle_pos != piece.pos:
                                    if current_lvl[row][col] != 'd':
                                        availablemoves.append(new_circle_pos)
                           
                    elif piece in w_knights:
                        legalmove = False
                        #makes sure knight only moves in an L path (horizontally)
                        if (col == piece.col + 1 or col == piece.col - 1) and (row == piece.row - 2 or row == piece.row + 2):
                            legalmove = True
                            pieceobstructioncheck(piece.row, piece.col, row, col)
                        #makes sure knight moves onlyh in an L pattern (vertically)
                        elif (row == piece.row - 1 or row == piece.row + 1) and (col == piece.col + 2 or col == piece.col - 2):
                            legalmove = True
                            pieceobstructioncheck(piece.row, piece.col, row, col)

                        elif row == piece.row and col == piece.col:
                            legalmove = True
                        #makes sure knight doesn't move to a position of an existing piece    
                        pieceobstructioncheck(piece.row, piece.col, row, col)
                        if current_lvl[row][col] == 'd':
                            legalmove = False
                        if legalmove:
                            #if move is available then a guide circle is placed where the knight can move
                            if new_circle_pos != piece.pos:
                                    availablemoves.append(new_circle_pos)
                    elif piece in w_queens:
                        legalmove = True
                        if equal_dis and abs(row - piece.row) > 0 or row == piece.row and col == piece.col:
                            #checks if piece or block is blocking the path of queen (bishop path)
                            bishopobstructioncheck(row, col)
                            pieceobstructioncheck(piece.row, piece.col, row, col)
                            if legalmove:
                                if new_circle_pos != piece.pos:
                                    #if move is available then a guide circle is placed where the queen can move
                                    if current_lvl[row][col] != 'd':
                                        availablemoves.append(new_circle_pos)
                        legalmove = True
                        if row == piece.row or col == piece.col:
                            #checks if piece or block is blocking the path of queen (rook path)
                            rookobstructioncheck(row, col)
                            pieceobstructioncheck(piece.row, piece.col, row, col)
                            if legalmove:
                                if new_circle_pos != piece.pos:
                                    #if move is available then a guide circle is placed where the queen can move
                                    if current_lvl[row][col] != 'd':
                                        availablemoves.append(new_circle_pos)      
                    elif piece in w_pawns:
                        if current_lvl[row][col] not in block_numbers:
                            legalmove = True
                            if piece.firstmove:
                                #makes sure the pawn can move 2 spaces during its first move
                                if piece.row in range(row + 1, row + 3) and piece.col == col:
                                    rookobstructioncheck(row, col)
                                    pieceobstructioncheck(piece.row, piece.col, row, col)
                                    if legalmove:
                                        if new_circle_pos != piece.pos:
                                            if current_lvl[row][col] != 'd':
                                                availablemoves.append(new_circle_pos)      
                            else:
                                #makes sure no piece or block is blocking its path
                                if piece.row == row + 1 and piece.col == col:
                                    rookobstructioncheck(row, col)
                                    pieceobstructioncheck(piece.row, piece.col, row, col)
                                    if legalmove:
                                        if new_circle_pos != piece.pos:
                                            if current_lvl[row][col] != 'd':
                                                availablemoves.append(new_circle_pos)  
                    elif piece in w_kings:
                        #can move one space in any direction
                        if piece.row in range(row - 1, row + 2) and piece.col in range(col -1, col + 2):
                            legalmove = True
                            #makes sure no pieces or blocks are blocking its path
                            pieceobstructioncheck(piece.row, piece.col, row, col)
                            if legalmove:
                                if new_circle_pos != piece.pos:
                                    if current_lvl[row][col] != 'd':
                                        availablemoves.append(new_circle_pos)
                                        
def obj_collision(obj1_pos, obj1_left, obj1_right, obj1_up,
                  obj1_down, obj2_pos,
                  obj2_left, obj2_right, obj2_up, obj2_down):
    #if the entity's left or right side is within the other entity
    if (obj1_pos[0] + obj1_right + obj2_right > obj2_pos[0]
    and obj2_pos[0] > obj1_pos[0] - obj1_left - obj2_left):
        #if the entity's up or down side is within the other entity
        if (obj1_pos[1] + obj1_down + obj2_up > obj2_pos[1] 
        and obj2_pos[1] > obj1_pos[1] - obj1_up - obj2_down):
            return True  
        
def unselectpieces():
    for piece in piece_list:
        piece.selected = False

def rookobstructioncheck(row, col):
    global legalmove, block_numbers, w_rooks
    #checks if there is an object between rook position and click position horizontally to see if it's a legal move
    for w_rook in piece_list:
        if w_rook.selected == True and w_rook.falling == False:
            if row == w_rook.row:
                legalmove = True
                if col > w_rook.col:
                    for c in range(w_rook.col, col):
                        if current_lvl[w_rook.row][c] in block_numbers:
                            legalmove = False
                        else:
                            for position in positions:
                                if position != [w_rook.row, w_rook.col]:
                                    for c in range(w_rook.col, col):
                                        if [w_rook.row, c] == position:
                                            legalmove = False
                else:
                    for c in range(col, w_rook.col):
                        if current_lvl[w_rook.row][c] in block_numbers:
                            legalmove = False
                        else:
                            for position in positions:
                                if position != [w_rook.row, w_rook.col]:
                                    for c in range(col, w_rook.col):
                                        if [w_rook.row, c] == position:
                                            legalmove = False
            #checks if there is an object between rook position and click position vertically to see if it's a legal move        
            if col == w_rook.col:
                legalmove = True
                if row > w_rook.row:
                    for r in range(w_rook.row, row):
                        if current_lvl[r][w_rook.col] in block_numbers:
                            legalmove = False
                        else:
                            for position in positions:
                                if position != [w_rook.row, w_rook.col]:
                                    for r in range(w_rook.row, row):
                                        if [r, w_rook.col] == position:
                                            legalmove = False
                else:
                    for r in range(row, w_rook.row):
                        if current_lvl[r][w_rook.col] in block_numbers:
                            legalmove = False
                        else:
                            for position in positions:
                                if position != [w_rook.row, w_rook.col]:
                                    for r in range(row, w_rook.row):
                                        if [r, w_rook.col] == position:
                                            legalmove = False

def bishopobstructioncheck(row, col):
    global legalmove, block_numbers, current_lvl, COLS, ROWS

    #checks if there are objects diagonal up to the right of bishop
    for w_bishop in piece_list:
        if w_bishop.selected == True and w_bishop.falling == False:
            if row < w_bishop.row and col > w_bishop.col:
                for c in range(w_bishop.col, col + 1):
                    for r in range(row, w_bishop.row + 1):
                        if abs(r - w_bishop.row) == abs(c - w_bishop.col): 
                            if current_lvl[r][c] in block_numbers:
                                legalmove = False

                            for position in positions:
                                if position != [w_bishop.row, w_bishop.col]:
                                    for c in range(w_bishop.col, col):
                                        for r in range(row, w_bishop.row):
                                            if [r, c] == position and abs(r - w_bishop.row) == abs(c - w_bishop.col):
                                                legalmove = False
                                                
                for r in range(row, w_bishop.row):
                    for c in range(w_bishop.col, col):
                         if abs(r - w_bishop.row) == abs(c - w_bishop.col): 
                            if current_lvl[r][c] in block_numbers:
                                legalmove = False

                            else:
                                for position in positions:
                                    if position != [w_bishop.row, w_bishop.col]:
                                        for r in range(row, w_bishop.row):
                                            for c in range(w_bishop.col, col):
                                                if [r, c] == position and abs(r - w_bishop.row) == abs(c - w_bishop.col): 
                                                    legalmove = False

                                                    
            #checks if there are objects diagonal up to the left of bishop                                    
            elif row < w_bishop.row and col < w_bishop.col:
                for c in range(col, w_bishop.col+1):
                    for r in range(row, w_bishop.row+1):
                        if abs(w_bishop.row - r) == abs(w_bishop.col - c): 
                            if current_lvl[r][c] in block_numbers: 

                                legalmove = False
                            for position in positions:
                                if position != [w_bishop.row, w_bishop.col+1]:
                                    for c in range(col, w_bishop.col+1):
                                        for r in range(row, w_bishop.row):
                                            if legalmove != False:
                                                if [r, c] == position and abs(r - w_bishop.row) == abs(c - w_bishop.col): 
                                                    legalmove = False

                
                for r in range(row, w_bishop.row):
                    for c in range(col, w_bishop.col):
                        if current_lvl[r][c] in block_numbers:
                            if abs(r - w_bishop.row) == abs(c - w_bishop.col): 
                                legalmove = False

                                
                            for position in positions:
                                if position != [w_bishop.row, w_bishop.col]:
                                    for r in range(row, w_bishop.row):
                                        for c in range(col, w_bishop.col):
                                            if [r, c] == position and abs(r - w_bishop.row) == abs(c - w_bishop.col): 
                                                legalmove = False
                                                
            #checks if there are objects diagonal down to the right of the bishop
            elif row > w_bishop.row and col > w_bishop.col:
                for c in range(w_bishop.col, col):
                    for r in range(w_bishop.row, row):
                        if current_lvl[r][c] in block_numbers and abs(r - w_bishop.row) == abs(c - w_bishop.col):
                            legalmove = False

                        for position in positions:
                            if position != [w_bishop.row, w_bishop.col]:
                                for c in range(w_bishop.col, col):
                                    for r in range(w_bishop.row, row):
                                        if [r, c] == position and abs(r - w_bishop.row) == abs(c - w_bishop.col): 
                                            legalmove = False
                for r in range(w_bishop.row, row):
                    for c in range(w_bishop.col, col):
                        if current_lvl[r][c] in block_numbers and abs(r - w_bishop.row) == abs(c - w_bishop.col):
                            legalmove = False

                    for position in positions:
                        if position != [w_bishop.row, w_bishop.col]:
                            for r in range(w_bishop.row, row):
                                for c in range(w_bishop.col, col):
                                    if [r, c] == position and abs(r - w_bishop.row) == abs(c - w_bishop.col):
                                        legalmove = False

                

            #checks if there are objects diagonal down to the left of the bishop
            elif row > w_bishop.row and col < w_bishop.col:
                for c in range(col, w_bishop.col):
                    for r in range(w_bishop.row, row):
                        if current_lvl[r][c] in block_numbers and abs(r - w_bishop.row) == abs(c - w_bishop.col): 
                            legalmove = False

                        for position in positions:
                            if position != [w_bishop.row, w_bishop.col]:
                                for c in range(col, w_bishop.col):
                                    for r in range(w_bishop.row, row):
                                        if [r, c] == position and abs(r - w_bishop.row) == abs(c - w_bishop.col): 
                                            legalmove = False
                                            
                    for r in range(w_bishop.row, row):                           
                        for c in range(col, w_bishop.col):
                            if current_lvl[r][c] in block_numbers and abs(r - w_bishop.row) == abs(c - w_bishop.col): 
                                legalmove = False

                        for position in positions:
                            if position != [w_bishop.row, w_bishop.col]:
                                for r in range(w_bishop.row, row):
                                    for c in range(col, w_bishop.col):
                                        if [r, c] == position and abs(r - w_bishop.row) == abs(c - w_bishop.col): 
                                            legalmove = False

        
def pieceobstructioncheck(piecerow, piececol, row, col):
    #checks if player click is at a piece position
    global legalmove, b_king, piece_list
    
    for piece in piece_list:
            if piece.falling == True:
                legalmove = False
                
    if b_king[0].collidable == False:
        legalmove = False

    for position in positions:
        if position != [piecerow, piececol]:
            if [row, col] == position:
                legalmove = False
            
def positionpiece(piece):
    global legalmove, levels_completed, b_king, current_lvl, MOVE_SOUND, piece_list, circle_time
                
    #positions piece and adds an offset to x and y position to center the image when clicked
    if [col * TILE_SIZE[0] + 40, row * TILE_SIZE[1] + offsety] in availablemoves:
        if piece.selected:
            piece.pos = [col * TILE_SIZE[0] + offsetx, row * TILE_SIZE[1] + offsety]
            piece.newpos = True
            circle_time = 0
            MOVE_SOUND.rewind()
            MOVE_SOUND.play()
            piece.firstmove = False

    if b_king != []:
        if piece.pos == b_king[0].pos:
            levels_completed.append(current_lvl)
            
def fadeoutothers(fadeinsound):
    for song in music_list:
        if song != fadeinsound:
            song.fadeout()
        else:
            song.fadein()       
        
class Scene:
    #draws the buttons for specific scenes of the game
    def __init__(self, name, buttons):
        self.name = name
        self.buttons = buttons
    
    def draw(self, canvas):
        for button in self.buttons:
            button.draw(canvas)

class Button:
    #creates buttons
    def __init__(self, position, size, image, destination):
        self.pos = position
        self.size = size
        self.image = image
        self.destination = destination
        self.enabled = True
        self.selected = False
    
    def draw(self,canvas):
        width, height = IMG_SIZES[self.image]
        canvas.draw_image(self.image,
                          (width / 2, height / 2),
                          (width, height),
                          (self.pos),
                          (self.size))
    
    def button_selected(self, click_position):
        #checks if button is selected
        global current_scene, current_lvl, lvl_1, lvl_2, world, w_kings, w_bishops, tutorial1
        global current_level, guidemenu, w_rooks, w_knights, block_list, piece_list, b_king
        global piece_positions, crate_list, b_kingtouchcount, lvl_3, door_list, pressure_plate_list
        global displayedmessage, displayedmessage2, tutorial_list2, cguidedialogues 
        global availablemoves, availablemovesanimated, w_queens, w_pawns, platform_list
        global upgrademenu, upgradeanimation
        self.selected = False
        #checks whether mouse is within left and right borders of button
        
        in_x = abs(click_position[0] - self.pos[0]) < self.size[0]/2
        
        #checks whether mouse is within top and bottom borders of button
        in_y = abs(click_position[1] - self.pos[1]) < self.size[1]/2
        if in_x and in_y:
            displayedmessage = ''
            displayedmessage2 = ''
            BUTTON_SOUND.rewind()
            BUTTON_SOUND.play()    
            #resets chess guide text position so the letters can appear one by one
            if self.destination in fulltutorial_list + tutorial_list4:
                for cguidedialogue in cguidedialogues:
                    if cguidedialogue != None:
                        cguidedialogue.dialoguepos = 0        
            if current_scene not in level_selects:
                if self.destination in levels_unlocked:
                    self.selected = True
                current_scene = self.destination

            elif current_scene in level_selects:
                if self.destination == 'menu' or self.destination in level_selects:
                    current_scene = self.destination

                elif self.destination in levels_unlocked:
                   
                    current_scene = self.destination
                    if self.pos == [WIDTH/2 - 305,HEIGHT/2]:
                        #checks if queen promotion button was clicked
                        for w_pawn in w_pawns:
                            if w_pawn.upgrade:
                                #replaces pawn with queen
                                w_queens.append(Piece(WHITE_QUEEN, w_pawn.pos,(TILE_SIZE))) 
                                for w_queen in w_queens:
                                    if w_queen not in piece_list:
                                        piece_list.append(w_queen)
                                for pawn in w_pawns:
                                    piece_list.remove(w_pawn)
                                w_pawns.remove(w_pawn)
                    elif self.pos == [WIDTH/2 - 96, HEIGHT/2]:
                        #checks if bishop promotion button was clicked
                        for w_pawn in w_pawns:
                            if w_pawn.upgrade:
                                #replaces pawn with bishop
                                w_bishops.append(Piece(WHITE_BISHOP, w_pawn.pos,(TILE_SIZE))) 
                                for w_bishop in w_bishops:
                                    if w_bishop not in piece_list:
                                        piece_list.append(w_bishop)
                                for pawn in w_pawns:
                                    piece_list.remove(w_pawn)
                                w_pawns.remove(w_pawn)
                    elif self.pos == [WIDTH/2 + 108, HEIGHT/2]:
                        #checks if rook promotion button was clicked
                        for w_pawn in w_pawns:
                            if w_pawn.upgrade:
                                #replaces pawn with rook
                                w_rooks.append(Piece(WHITE_ROOK, w_pawn.pos,(TILE_SIZE))) 
                                for w_rook in w_rooks:
                                    if w_rook not in piece_list:
                                        piece_list.append(w_rook)
                                for pawn in w_pawns:
                                    piece_list.remove(w_pawn)
                                w_pawns.remove(w_pawn)
                    elif self.pos == [WIDTH/2 + 312, HEIGHT/2]:
                        #checks if knight promotion button was clicked
                        for w_pawn in w_pawns:
                            if w_pawn.upgrade:
                                #replaces pawn with knight
                                w_knights.append(Piece(WHITE_HORSE, w_pawn.pos,(TILE_SIZE))) 
                                for w_knight in w_knights:
                                    if w_knight not in piece_list:
                                        piece_list.append(w_knight)
                                for pawn in w_pawns:
                                    piece_list.remove(w_pawn)
                                w_pawns.remove(w_pawn)

                #checks if the level the button is leading to is unlocked
                for level in levels:
                    if self.destination in levels:
                        if self.destination in levels_unlocked:
                            self.selected = True
                            current_scene = self.destination
            if upgrademenu:
                #makes sure restart button works during upgrade menu
                if self.destination in levels:
                    if self.pos == [190, 50]:
                        
                        current_scene = current_level
                        new_level()
                        load_level(current_scene)
                        upgrademenu = False
                        
                if self.destination in level_selects:
                    #makes sure level back button works during upgrade menu
                    if self.pos == [70, 50]:
                        w_pawns = []
                        current_scene = self.destination
                        upgrademenu = False
                        
            if upgrademenu == False:
                #resets the level before entering
                if self.destination in levels:
                    if current_scene not in tutorial_list4:
                        current_level = current_scene
                        new_level()
                        load_level(current_scene)
       
class Stage:
    def __init__(self, current_lvl):
        
        global wking, crate_list
        x = TILE_SIZE[0]/2
        y = TILE_SIZE[1]/2
        
        kingcount = 0
        rookcount = 0
        bishopcount = 0
        knightcount = 0 
        pawncount = 0
        queencount = 0
        
        for row in current_lvl:
            for tile in row:
                #spawns in pieces and blocks
                if tile == 1:
                    block_list.append(Block(GRASS, [x, y],(TILE_SIZE)))
                    
                if tile == 2:
                    block_list.append(Block(CONNECTED_DIRT, [x, y],(TILE_SIZE)))
                    
                if tile == 3:
                    block_list.append(Block(LEFT_GRASS, [x, y],(TILE_SIZE)))
                    
                if tile == 4:
                    block_list.append(Block(RIGHT_GRASS, [x, y],(TILE_SIZE)))
                
                if tile == 5:
                    block_list.append(Block(RIGHT_DIRT_SURFACELESS, [x, y],(TILE_SIZE)))
                
                if tile == 6:
                    block_list.append(Block(LEFT_DIRT_SURFACELESS, [x, y],(TILE_SIZE)))
                
                if tile == 7:
                    block_list.append(Block(LEFT_GRASS_FLOAT, [x, y],(TILE_SIZE)))
                
                if tile == 8:
                    block_list.append(Block(GRASS_FLOAT, [x, y],(TILE_SIZE)))
                
                if tile == 9:
                    block_list.append(Block(RIGHT_GRASS_FLOAT, [x, y],(TILE_SIZE)))
                
                if tile == 10:
                    block_list.append(Block(LEFT_WALL_GRASS, [x, y],(TILE_SIZE)))
                
                if tile == 11:
                    block_list.append(Block(RIGHT_WALL_GRASS, [x, y],(TILE_SIZE)))
                
                if tile == 12:
                    block_list.append(Block(BOTTOM_RIGHT_DIRT, [x, y],(TILE_SIZE)))
                    
                if tile == 13:
                    block_list.append(Block(BOTTOM_LEFT_DIRT, [x, y],(TILE_SIZE)))
                
                if tile == 14:
                    block_list.append(Block(FLOAT_BOTTOMLEFT_DIRT, [x, y],(TILE_SIZE)))
                
                if tile == 15:
                    block_list.append(Block(FLOAT_BOTTOM_DIRT, [x, y],(TILE_SIZE)))
                
                if tile == 16:
                    block_list.append(Block(FLOAT_BOTTOMRIGHT_DIRT, [x, y],(TILE_SIZE)))
                
                if tile == 17:
                    block_list.append(Block(SAND, [x, y], (TILE_SIZE)))
                
                if tile == 18:
                    block_list.append(Block(LEFT_SAND, [x, y], (TILE_SIZE)))
                 
                if tile == 19:
                    block_list.append(Block(RIGHT_SAND, [x, y], (TILE_SIZE)))
                
                if tile == 20:
                    block_list.append(Block(LEFT_SAND_SURFACELESS, [x, y], (TILE_SIZE)))
                    
                if tile == 21:
                    block_list.append(Block(RIGHT_SAND_SURFACELESS, [x, y], (TILE_SIZE)))
                
                if tile == 22:      
                    block_list.append(Block(LEFT_WALL_SAND, [x, y], (TILE_SIZE)))
                    
                if tile == 23:
                    block_list.append(Block(RIGHT_WALL_SAND, [x, y], (TILE_SIZE)))
                
                if tile == 24:
                    block_list.append(Block(BOTTOM_LEFT_SAND, [x, y], (TILE_SIZE)))
                
                if tile == 25:
                    block_list.append(Block(BOTTOM_RIGHT_SAND, [x, y], (TILE_SIZE)))
                
                if tile == 26:
                    block_list.append(Block(FLOAT_BOTTOMLEFT_SAND, [x, y], (TILE_SIZE)))
                
                if tile == 27:
                    block_list.append(Block(FLOAT_BOTTOMRIGHT_SAND, [x, y], (TILE_SIZE)))
                    
                if tile == 28:
                    block_list.append(Block(FLOAT_BOTTOM_SAND, [x, y], (TILE_SIZE)))
                
                if tile == 29:
                    block_list.append(Block(CONNECTED_SAND, [x, y], (TILE_SIZE)))
                
                if tile == 30:
                    platform_list.append(Block(SAND_PLATFORM, [x, y], (TILE_SIZE)))
                
                if tile == 31:
                    block_list.append(Block(FLOAT_SAND, [x, y], (TILE_SIZE)))
                
                if tile == 32:
                    block_list.append(Block(LEFT_FLOAT_SAND, [x, y], (TILE_SIZE)))
                
                if tile == 33:
                    block_list.append(Block(RIGHT_FLOAT_SAND, [x, y], (TILE_SIZE)))
                    
                if tile == '30p':
                    platform_list.append(Block(SAND_PLATFORM, [x, y], (TILE_SIZE)))
                    w_pawns.append(Piece(WHITE_PAWN, [x, y],(TILE_SIZE))) 
                    
                if tile == '30r':
                    platform_list.append(Block(SAND_PLATFORM, [x, y], (TILE_SIZE)))
                    w_rooks.append(Piece(WHITE_ROOK, [x, y],(TILE_SIZE)))
                    
                if tile == 'wk':
                    kingcount += 1
                    if len(w_kings) <= kingcount:
                       w_kings.append(Piece(WHITE_KING, [x, y],(TILE_SIZE)))  
                    
                if tile == 'wb':
                    bishopcount += 1
                    if len(w_bishops) <= bishopcount:
                        w_bishops.append(Piece(WHITE_BISHOP, [x, y],(TILE_SIZE)))  
                        
                if tile == 'wkt':
                    knightcount += 1
                    if len(w_knights) <= knightcount:
                        w_knights.append(Piece(WHITE_HORSE, [x, y],(TILE_SIZE)))  
                        
                if tile == 'wr':
                    rookcount += 1
                    if len(w_rooks) <= rookcount:
                        w_rooks.append(Piece(WHITE_ROOK, [x, y],(TILE_SIZE))) 
                
                if tile == 'wp':
                    pawncount += 1
                    if len(w_pawns) <= pawncount:
                        w_pawns.append(Piece(WHITE_PAWN, [x, y],(TILE_SIZE))) 
                
                if tile == 'wq':
                    queencount += 1
                    if len(w_queens) <= queencount:
                        w_queens.append(Piece(WHITE_QUEEN, [x, y],(TILE_SIZE))) 

                if tile == 'd':
                    door_list.append(Door([x -15, y], (TILE_SIZE)))
                
                if tile == 'p':
                    pressure_plate_list.append(Pressure_plate([x, y+10], (TILE_SIZE)))
                if tile == 'bk':
                    b_king.append(Black_king(BLACK_KING, [x, y + 5], (TILE_SIZE)))
                
                if tile == 'c2':
                    crate_list.append(Crate([x, y], (TILE_SIZE), 2))
                
                if tile == 'c3':
                    crate_list.append(Crate([x, y], (TILE_SIZE), 3))
                    
                if tile == 'c4':
                    crate_list.append(Crate([x, y], (TILE_SIZE), 4))
                
                if tile == 'c5':
                    crate_list.append(Crate([x, y], (TILE_SIZE), 5))
                x += TILE_SIZE[0]
            y += TILE_SIZE[1]
            x = TILE_SIZE[0]/2
                                        
class Block:
    
    def __init__(self, image, position, size):
        self.image = image
        self.pos = position
        self.size = size
    
    def draw(self, canvas):
        #spawns and draws the blocks
        canvas.draw_image(self.image,
                          (self.image.get_width()/2, self.image.get_width()/2),
                          (self.image.get_width(), self.image.get_width()),
                          self.pos,
                          self.size)
class Black_king:
    
    def __init__(self, image, position, size):
        self.image = image
        self.pos = position
        self.size = size
        self.death = False
        self.animated = False
        self.vel_y = 0
        self.rotation = 0
        self.animationdone = False
        self.collidable = True
        self.dead = False
    def draw(self, canvas):
        global current_scene, draw_scene, scene_lvlselect1, world, current_lvl, tutorial2
        global w_kings, w_bishops, w_rooks, w_knights, block_list, piece_list, crate_list
        global piece_positions, b_king
        #spawns and draws the blocks

        canvas.draw_image(self.image,
                          (BUTTON_SIZE[0]/2, BUTTON_SIZE[0]/2),
                          (BUTTON_SIZE[0], BUTTON_SIZE[0]),
                          self.pos,
                          self.size,
                          self.rotation)
    def update(self):
        global current_scene, positions
        if self.death == True:
            self.animated = True
            self.rotation += 0.1
            self.vel_y -= GRAVITY + 3
            self.pos[1] += self.vel_y
        if self.vel_y < - 8:
            self.death = False
            
        
        if self.animated == True and self.death == False:
            positions = []
            DEATH_SOUND.play()
            self.rotation += 0.1
            self.vel_y += GRAVITY
            self.pos[1] += self.vel_y
            
        if self.pos[1] > HEIGHT + 120:
            self.dead = True
            self.animated = False
            if current_scene not in fulltutorial_list:
                if current_scene in world_1:
                    current_scene = 'level select 1'
                elif current_scene in world_2:
                    current_scene = 'level select 2'
        
class Crate:
    
    def __init__(self, position, size, piecestobreak):
        self.pos = position
        self.size = size
        self.col = int(self.pos[0] // TILE_SIZE[0])
        self.row = int(self.pos[1] // TILE_SIZE[1])
        #pieces needed on the crate to break it
        self.limit = piecestobreak
        self.piecesoncrate = 0
        self.oneoncrate = False
    def draw(self, canvas):
        global CRATE_SIZE
        #spawns and draws the crates
        #normal crate
        if self.limit - self.piecesoncrate == 2:
            w,h = IMG_SIZES[CRATE1]
            canvas.draw_image(CRATE2,
                              (w/2, w/2),
                              (h, h),
                              self.pos,
                              self.size)
        #crate is cracked when a piece lands on it
        else:
            w,h = IMG_SIZES[CRATE1]
            canvas.draw_image(CRATE1,
                              (w/2, w/2),
                              (h, h),
                              self.pos,
                              self.size)
    def update(self):
        #crate gets removed when two pieces are on it at the same time
        global crate_list, piece_list
        self.piecesoncrate = 0
        if self.limit == 2:
            for crate in crate_list:
                for piece in piece_list:
                    if crate.row - 1 == piece.row and crate.col == piece.col:
                        self.piecesoncrate = 1
                        if self.oneoncrate == False:
                            self.oneoncrate = True
                        for piece in piece_list:
                            if crate.row - 2 == piece.row and crate.col == piece.col: 
                                crate_list.remove(crate)
                                CRATEBREAK.play()
                                
class Piece:
    
    def __init__(self, image, position, size):
        self.image = image
        self.pos = position
        self.size = size
        self.selected = False
        self.falling = True
        self.vel_y = 0
        self.x = self.pos[0]
        self.y = self.pos[1]
        self.col = int(self.pos[0] // TILE_SIZE[0])
        self.row = int(self.pos[1] // TILE_SIZE[1])
        self.newpos = False
        self.animated = False
        self.firstmove = True
        self.upgrade = False
        self.animationcount = 0
    def draw(self, canvas):
        #spawns and draws the bricks
        canvas.draw_image(self.image,
                          (self.image.get_width()/2, self.image.get_width()/2),
                          (self.image.get_width(), self.image.get_width()),
                          self.pos,
                          self.size)

    def update(self):
        global current_scene, b_kingtouchcount, pressure_plate_list
        #adds gravity
        self.col = int(self.pos[0] // TILE_SIZE[0])

        self.row = int(self.pos[1] // TILE_SIZE[1])

        self.pos[1] += self.vel_y
        if self.falling:
            self.vel_y += GRAVITY
        
        if self.newpos == True:
            self.size = [60, 60]
            self.newpos = False
        if self.size != TILE_SIZE:
            self.size[0] += 4
            self.size[1] += 4
        for block in block_list:
            #allows pieces to stack if on top of each other
            for piece in piece_list:
                if (self.pos,
                        self.size[0]/2,
                        self.size[0]/2,
                        self.size[1]/2,
                        self.size[1]/2) != (piece.pos,
                                            piece.size[0]/2,
                                            piece.size[0]/2,
                                            piece.size[1]/2,
                                            piece.size[1]/2):

                        if obj_collision(self.pos, self.size[0]/2, self.size[0]/2, 
                                         self.size[1]/2, self.size[1]/2, piece.pos, 
                                         piece.size[0]/2, piece.size[0]/2, piece.size[1]/2, 
                                         piece.size[1]/2) and self.pos[1] < piece.pos[1]:
                            self.vel_y = 0
                            self.pos[1] = piece.pos[1] - 80
                            self.falling = False
                            
            #checks if there is a block beneath the piece    
              
            if self.pos[0] == block.pos[0] and self.pos[1] + 75 != block.pos[1]:
                #checks if there is a piece beneath the piece
                if [self.pos[0], self.pos[1] + 80] not in piece_positions:
                    self.falling = True
            
            for crate in crate_list:
                if self.pos[0] == crate.pos[0] and self.pos[1] + 75 != crate.pos[1]:
                    #checks if there is a piece beneath the piece
                    if [self.pos[0], self.pos[1] + 80] not in piece_positions:
                        self.falling = True
            for platform in platform_list:

                if self.pos[0] == platform.pos[0] and self.pos[1] == platform.pos[1]:
                    if [self.pos[0], self.pos[1] + 80] not in piece_positions:
                        self.falling = True
            
        #checks if pieces are touching blocks
        for block in block_list:             
            if obj_collision(self.pos, self.size[0]/2, self.size[0]/2, 
                             self.size[1]/2, self.size[1]/2, block.pos, 
                             block.size[0]/2, block.size[0]/2, block.size[1]/2, 
                             block.size[1]/2):
                self.vel_y = 0
                self.pos[1] = block.pos[1] - 75
                self.falling = False
                
        for crate in crate_list:             
            if obj_collision(self.pos, self.size[0]/2, self.size[0]/2, 
                             self.size[1]/2, self.size[1]/2, crate.pos, 
                             crate.size[0]/2, crate.size[0]/2, crate.size[1]/2, 
                             crate.size[1]/2):
                self.vel_y = 0
                self.pos[1] = crate.pos[1] - 75
                self.falling = False
        #checks if piece is on a platform
        if self.row < 9:
            pieceposition = current_lvl[self.row+1][self.col]
            piece_y = int(self.pos[1])
            for platform in platform_list:
                if self.pos[1] == platform.pos[1]:
                    self.falling = True 
                if piece_y == platform.pos[1] + 6 or piece_y == platform.pos[1]:
                    if pieceposition == 30 or pieceposition == '30p':
                        self.pos[1] = platform.pos[1] + 6
                        self.vel_y = 0
                        self.falling = False

                

        for pressure_plate in pressure_plate_list:

            if [pressure_plate.pos[0], pressure_plate.pos[1] - 5] in piece_positions:
                pressure_plate.pressed = True
            else:
                pressure_plate.pressed = False

        #checks if piece touches black king
        if b_king != []:
            if obj_collision(self.pos, self.size[0]/2, self.size[0]/2, 
                            self.size[1]/2, self.size[1]/2, b_king[0].pos,
                            b_king[0].size[0]/2, b_king[0].size[0]/2, b_king[0].size[1]/2, 
                            b_king[0].size[1]/2) and b_king[0].collidable == True:
                b_king[0].death = True
                b_king[0].collidable = False
                if current_scene not in tutorial_list + tutorial_list2 + tutorial_list3:
                    #checks if level number is one digit
                    if len(current_scene) < 8:
                        lvlnumber_onedigit = str(int(current_scene[6]) + 1)
                        #unlocks the completed level added by one
                        if 'level' + current_scene[6] not in levels_completed:
                            levels_completed.append(current_scene)
                            levels_unlocked.append('level' + " " + lvlnumber_onedigit)
                    #checks if level number is 2 digits
                    elif len(current_scene) >= 8:
                        lvlnumber_twodigit = str(int(current_scene[6])) + str(int(current_scene[7]) + 1)
                        #unlocks the completed level added by one
                        if 'level' + current_scene[6] + current_scene[7] not in levels_completed:
                            levels_completed.append(current_scene)
                            levels_unlocked.append('level' + " " + lvlnumber_twodigit)
                        
                            
class Pressure_plate:
    def __init__(self, position, size):
        self.img = PRESSUREPLATE
        self.pos = position
        self.size = size
        self.pressed = False
        self.time = 0
        
    def draw(self, canvas):
        w,h = IMG_SIZES[PRESSUREPLATE]
        COLS = 21
        ROWS = 1
        col = self.time%COLS
        row = self.time//COLS
        canvas.draw_image(self.img, 
                         [w/2 + w*col,h/2 + h*row], 
                         [w,h], 
                         self.pos, 
                         self.size)
        
    def update(self):
        global door_list
        if self.pressed:
            #animates pressure plate being presssed down
            if self.time < 10:
                self.time += 2
            for door in door_list:
                door.activated = True
        else:
            #animated pressure plate being released
            if self.time > 0:
                self.time -= 2
            for door in door_list:
                door.activated = False
class Door:
    def __init__(self, position, size):
        self.img = DOORS
        self.pos = position
        self.size = size
        self.closed = True
        self.openanimation = False
        self.closeanimation = False
        self.time = 0
        self.activated = False
        
    def draw(self, canvas):
        if not self.openanimation:
            w,h = IMG_SIZES[DOORS]
            COLS = 1
            ROWS = 3
            canvas.draw_image(self.img, 
                                      [w/2,h/2], 
                                      [w,h], 
                                      self.pos, 
                                      self.size)
        if self.openanimation or self.closeanimation:
            w,h = IMG_SIZES[DOORS]
            COLS = 1
            ROWS = 3
            col = self.time%COLS
            row = self.time//COLS
            canvas.draw_image(self.img, 
                             [w/2 + w*col,h/2 + h*row], 
                             [w,h], 
                             self.pos, 
                             self.size)
    def update(self):
        COLS = 1
        ROWS = 3
        if self.activated:
            self.closeanimation = False
            self.openanimation = True
        elif self.time != 0:
            self.openanimation = False
            self.closeanimation = True
        else:
            self.openanimation = False
            self.closeanimation = False
        if self.openanimation:
            if self.time < 3:
                DOOR_OPEN.rewind()
                DOOR_OPEN.play()
                self.time += 1
                
        if self.closeanimation:
            if self.time > 0:
                self.time -= 1
                if self.time == 2:
                    DOOR_CLOSE.play()

class Dialogue:
    def __init__(self, position, message):
        self.message = message
        self.image = CHESS_GUIDE_DIALOGUE_BOX
        self.pos = position
        self.dialoguepos = 0
        self.counter = 0

    def draw(self, canvas):
        global displayedmessage
        canvas.draw_image(TUTORIAL_OVERLAY, 
                          (WIDTH / 2, HEIGHT / 2),
                          (WIDTH, HEIGHT),
                          (WIDTH / 2, HEIGHT / 2),
                          (WIDTH, HEIGHT))
        
        canvas.draw_image(CHESS_GUIDE_DIALOGUE_BOX, 
                          (WIDTH / 2, HEIGHT / 2),
                          (WIDTH, HEIGHT),
                          (self.pos[0], self.pos[1]),
                          (WIDTH, HEIGHT))
        
        canvas.draw_text(displayedmessage,
                         [self.pos[0] - 570, self.pos[1] + 180],
                         70,
                         'white', 'sans-serif')
        canvas.draw_text(displayedmessage2,
                         [self.pos[0] - 570, self.pos[1] + 280],
                         70,
                         'white', 'sans-serif')
        
    def update(self):
        global legalmove, displayedmessage, displayedmessage2, TALKING_SOUND
        line_1_limit = 31
        self.counter += 1
        #pauses talking sound when chess guide stops talking
        if self.dialoguepos == len(self.message)-1:
            TALKING_SOUND.pause()
        #displays the letters of the first line of dialogue one by one    
        elif self.dialoguepos <= line_1_limit and self.counter % 2 == 0:
            displayedmessage += self.message[self.dialoguepos]
            self.dialoguepos += 1
        #displays the letters of the second line of dialogue one by one    
        elif self.dialoguepos >= line_1_limit and self.counter % 2 == 0:
            if self.dialoguepos < len(self.message)-1:
                self.dialoguepos += 1
                displayedmessage2 += self.message[self.dialoguepos]
        #makes sure chess guide talks when text is still appearing               
        if self.dialoguepos != len(self.message)-1:
            TALKING_SOUND.play()
    
            for piece in piece_list:
                piece.falling = True
                

class Musicsfx:
    def __init__(self, sound, volume):
        self.sound = sound
        self.volume = volume
    
    def fadein(self):
        self.sound.play()
        if self.volume < 1:

            self.volume += 0.01
            self.sound.set_volume(self.volume)
            self.sound.play()
            if self.volume > 0.99:
                self.volume = 1


    def fadeout(self):
        if self.volume >= 0:
            self.sound.play()
            self.sound.set_volume(self.volume)
            self.volume -= 0.01
            if self.volume < 0.01:
                self.sound.rewind()
        
class Animated_circle:
    def __init__(self, position, time, delay):
        self.img = BLACK_CIRCLES
        self.pos = position
        self.size = (45, 45)
        self.pressed = False
        self.time = time
        self.delay = delay
        
    def draw(self, canvas):
        w,h = IMG_SIZES[BLACK_CIRCLES]
        COLS = 24
        ROWS = 1
        col = self.time%COLS
        row = self.time//COLS
        canvas.draw_image(self.img, 
                         [w/2 + w*col,h/2 + h*row], 
                         [w,h], 
                         self.pos, 
                         self.size)
        
    def update(self):
        #makes guide circles animated 
        global circle_time, delay
        COLS = 24
        self.delay += 1
        if self.delay % 3 == 0:
            self.time += 1
            if self.time >= 24:
                self.time = 0
        circle_time = self.time
        delay = self.delay
            
def mouse_click(pos):
    global TILE_SIZE, col, row, current_scene, sqselected, playerclicks, world
    global current_lvl, offsetx, offsety, legalmove, w_rookrow, piece_list, crates
    global positions, block_numbers, TILE_SIZE, circle_time, availablemoves
    
    for button in draw_scene.buttons:
            button.button_selected(pos)
            
    if current_scene in levels and current_scene != 'upgrade piece':
        #Divides the level grid into columns and rows
        col = pos[0]//TILE_SIZE[0]
        row = pos[1]//TILE_SIZE[1]
        #centers pieces in each grid
        offsetx = 40
        offsety = 45
        #stores the column and row that the pieces are currently in
        positions = []
        for piece in piece_list:
            if not piece.selected:
                positions.append([piece.row, piece.col])
        if w_kings != []:
            for w_king in w_kings:
                if [row, col] == [w_king.row, w_king.col]:
                    unselectpieces()
                    availablemoves = []
                    circle_time = 0
                    MOVE_SOUND.rewind()
                    MOVE_SOUND.play()
                    w_king.selected = True
                   
                if w_king.selected == True and w_king.falling == False:
                    #checks if the player click being moved to is solid or not
                    if current_lvl[row][col] not in block_numbers:
                        #king can only move one tile from all sides
                        if w_king.row in range(row - 1, row + 2) and w_king.col in range(col -1, col + 2):
                            positionpiece(w_king)
                            
        if w_bishops != []:
            for w_bishop in w_bishops:
                if [row, col] == [w_bishop.row, w_bishop.col]:
                    unselectpieces()
                    availablemoves = []
                    circle_time = 0
                    w_bishop.selected = True
                    if not w_bishop.falling:
                        MOVE_SOUND.rewind()
                        MOVE_SOUND.play()
                    
            
                if w_bishop != []:    
                    equal_dis = abs(row - w_bishop.row) == abs(col - w_bishop.col)
                    if w_bishop.selected == True and w_bishop.falling == False:
                        if current_lvl[row][col] not in block_numbers:
                            #checks if absolute value of horizontal and vertical displacement are equal for diagonal movement
                            if equal_dis and abs(row - w_bishop.row) > 0 or row == w_bishop.row and col == w_bishop.col:
                                positionpiece(w_bishop)
                                w_bishop.falling = True 
        
        if w_rooks != []:
            for w_rook in w_rooks:
                if [row, col] == [w_rook.row, w_rook.col]:
                    unselectpieces()
                    availablemoves = []
                    circle_time = 0
                    w_rook.selected = True
                    if not w_rook.falling:
                        MOVE_SOUND.rewind()
                        MOVE_SOUND.play()
                    

                if w_rook.selected == True and w_rook.falling == False:
                    #makes sure click position is not in a block
                    if current_lvl[row][col] not in block_numbers:
                        if row == w_rook.row or col == w_rook.col:   
                            positionpiece(w_rook)
                            w_rook.falling = True
        if w_queens != []:
            for w_queen in w_queens:
                if [row, col] == [w_queen.row, w_queen.col]:
                    unselectpieces()
                    availablemoves = []
                    circle_time = 0
                    w_queen.selected = True
                    if not w_queen.falling:
                        MOVE_SOUND.rewind()
                        MOVE_SOUND.play()
                    

                if w_queen.selected == True and w_queen.falling == False:
                    if current_lvl[row][col] not in block_numbers:
                        positionpiece(w_queen)
                        w_queen.falling = True

        if w_knights != []:       
            for w_knight in w_knights:
                if [row, col] == [w_knight.row, w_knight.col]:
                    unselectpieces()
                    availablemoves = []
                    circle_time = 0
                    w_knight.selected = True
                    if not w_knight.falling:
                        MOVE_SOUND.rewind()
                        MOVE_SOUND.play()
                    

                if w_knight.selected == True and w_knight.falling == False:
                    if current_lvl[row][col] not in block_numbers:
                        #checks if knight moves in an L pattern
                        if (col == w_knight.col + 1 or col == w_knight.col - 1) and (row == w_knight.row - 2 or row == w_knight.row + 2):
                            positionpiece(w_knight)
                            w_knight.falling = True
                        elif (row == w_knight.row - 1 or row == w_knight.row + 1) and (col == w_knight.col + 2 or col == w_knight.col - 2):
                            positionpiece(w_knight)
                            w_knight.falling = True
                        elif row == w_knight.row and col == w_knight.col:
                            positionpiece(w_knight)
                            w_knight.falling = True
                            
        if w_pawns != []:
           for w_pawn in w_pawns:
               if [row, col] == [w_pawn.row, w_pawn.col]:
                    unselectpieces()
                    availablemoves = []
                    circle_time = 0
                    w_pawn.selected = True
                    if not w_pawn.falling:
                        MOVE_SOUND.rewind()
                        MOVE_SOUND.play()
                    
                    
               if w_pawn.selected == True and w_pawn.falling == False:
                   positionpiece(w_pawn)
                   w_pawn.falling = True
                    
                       
        #updates piece column and row in case pieces fell when another one moved
        positions = []
        for piece in piece_list:
            if not piece.selected:
                positions.append([piece.row, piece.col])
                
def draw(canvas):
    global current_scene, draw_scene
    global SELECTIONBGRD, selectionbgrd_width, selectionbgrd_height, lvlbutton_x, lvlbutton_y, crates
    global IMG_SIZES, block_list, world, block_numbers, button_restartlvl, current_scene, scene_lvl, current_lvl
    global piece_list, level, w_kingrow, piece_positions, scene_lvlselect1, circle_time, delay, positions, upgradeanimation
    global crate_list, sound_volume, level_selection_effects, legalmove, availablemoves, availablemovesanimated
    global upgrademenu, button_bishop, button_queen, button_rook, button_knight

    update_buttons() 
    
    if current_scene == 'menu':
        fadeoutothers(menu_effects)
        TALKING_SOUND.rewind()
        canvas.draw_image(MENU_IMAGE, 
                      (WIDTH / 2, HEIGHT / 2),
                      (WIDTH, HEIGHT),
                      (WIDTH / 2, HEIGHT / 2),
                      (WIDTH, HEIGHT))
        draw_scene = scene_menu
    #draws background, draws buttons, and plays music depending on the world    
    if current_scene == 'level select 1':
        fadeoutothers(world_1_sfx)
        scene_lvlselect1 = Scene('level select 1', button_levels1 + [button_menu] + [button_next1])
        
        draw_scene = scene_lvlselect1
        canvas.draw_image(SELECTIONBGRD, 
                      (selectionbgrd_width / 2, selectionbgrd_height / 2),
                      (selectionbgrd_width, selectionbgrd_height),
                      (WIDTH / 2, HEIGHT / 2),
                      (WIDTH, HEIGHT))
    
    if current_scene == 'level select 2' or current_scene in world_2:
        fadeoutothers(world_2_sfx)
        canvas.draw_image(SELECTIONBGRD2, 
                      (selectionbgrd_width / 2, selectionbgrd_height / 2),
                      (selectionbgrd_width, selectionbgrd_height),
                      (WIDTH / 2, HEIGHT / 2),
                      (WIDTH, HEIGHT))
        
        scene_lvlselect2 = Scene('level select 2', button_levels2 + [button_lvlselect1])
        draw_scene = scene_lvlselect2
          
    if current_scene in levels:
        upgrademenu = False   
        if current_scene in world_1 or current_scene in fulltutorial_list:
            width, height = IMG_SIZES[WORLD1BGRD]
            canvas.draw_image(WORLD1BGRD, 
                      (width / 2, height / 2),
                      (width, height),
                      (WIDTH / 2, HEIGHT / 2),
                      (WIDTH, HEIGHT))
        
        elif current_scene in world_2 or current_scene == 'upgrade piece':
            canvas.draw_image(WORLD2BGRD, 
                      (selectionbgrd_width / 2, selectionbgrd_height / 2),
                      (selectionbgrd_width, selectionbgrd_height),
                      (WIDTH / 2, HEIGHT / 2),
                      (WIDTH, HEIGHT))
            fadeoutothers(world_2_sfx)
        #controls music fading in or out depending on the scene    
        if current_scene not in fulltutorial_list:    
            draw_scene = scene_lvl
            fadeoutothers(world_1_sfx)
        else:
            fadeoutothers(tutorial_sfx)
            
        if current_scene in world_2:
            fadeoutothers(world_2_sfx)
          
        for block in block_list:
            block.draw(canvas)
            
        for platform in platform_list:
            platform.draw(canvas)
            
        for door in door_list:
            door.draw(canvas)
            door.update()
            
        for crate in crate_list:
            crate.draw(canvas)
            crate.update()
            
        for pressure_plate in pressure_plate_list:
            pressure_plate.draw(canvas)
            pressure_plate.update()
        #updates piece positions    
        positions = []
        piece_positions = []    
        if w_kings != []:
            for w_king in w_kings:
                if w_king in piece_list:
                    piece_list.remove(w_king)
                positions.append([w_king.row, w_king.col])
                piece_list.append(w_king)
                piece_positions.append(w_king.pos)
   
        
        if w_bishops != []:
            for w_bishop in w_bishops:
                if w_bishop in piece_list:
                    piece_list.remove(w_bishop)               
                piece_list.append(w_bishop)
                positions.append([w_bishop.row, w_bishop.col])
                piece_positions.append(w_bishop.pos)
        
        if w_rooks != []:
            for w_rook in w_rooks:
                if w_rook in piece_list:
                    piece_list.remove(w_rook)
                positions.append([w_rook.row, w_rook.col])
                piece_list.append(w_rook)
                piece_positions.append(w_rook.pos)
                    

        if w_knights != []:
            for w_knight in w_knights:
                if w_knight in piece_list:
                    piece_list.remove(w_knight)
                positions.append([w_knight.row, w_knight.col])  
                piece_list.append(w_knight)
                piece_positions.append(w_knight.pos)
                
        if w_queens != []:
            for w_queen in w_queens:
                if w_queen in piece_list:
                    piece_list.remove(w_queen)
                positions.append([w_queen.row, w_queen.col])  
                piece_list.append(w_queen)
                piece_positions.append(w_queen.pos)
        
        if w_pawns != []:
            for w_pawn in w_pawns:
                if w_pawn in piece_list:
                    piece_list.remove(w_pawn)
                positions.append([w_pawn.row, w_pawn.col])  
                piece_list.append(w_pawn)
                piece_positions.append(w_pawn.pos)
            
        for piece in piece_list:
            piece.update()
        #finds available piece positions
        if w_rooks != []:
            for w_rook in w_rooks:
                if not w_rook.selected:
                    if [w_rook.row, w_rook.col] not in positions:
                        positions.append([w_rook.row, w_rook.col])
                w_rook.draw(canvas)
                if w_rook.selected == True:
                    availablemoves = []
                    availablemovesanimated = []
                    find_available_moves(w_rook)
                    if [w_rook.pos[0], w_rook.pos[1]-1] in availablemoves:
                               availablemoves.remove([w_rook.pos[0], w_rook.pos[1]-1])
        if w_bishops != []:
            for w_bishop in w_bishops:
                if not w_bishop.selected:
                    if [w_bishop.row, w_bishop.col] not in positions:
                        positions.append([w_bishop.row, w_bishop.col])
                w_bishop.draw(canvas)
                if w_bishop.selected == True:
                    if w_bishop.falling == True:
                        availablemoves = []
                        availablemovesanimated = []
                    elif w_bishop.falling == False:
                        if availablemoves == []:
                            availablemovesanimated = []
                            find_available_moves(w_bishop)
                        else:
                            availablemovesanimated = []
                            if [w_bishop.pos[0], w_bishop.pos[1]-1] in availablemoves:
                               availablemoves.remove([w_bishop.pos[0], w_bishop.pos[1]-1]) 
        if w_queens != []:
            for w_queen in w_queens:
                if not w_queen.selected:
                    if [w_queen.row, w_queen.col] not in positions:
                        positions.append([w_queen.row, w_queen.col])
                w_queen.draw(canvas)
                if w_queen.selected == True:
                    if w_queen.falling == True:
                        availablemoves = []
                        availablemovesanimated = []
                    elif w_queen.falling == False:
                        if availablemoves == []:
                            availablemovesanimated = []
                            find_available_moves(w_queen)
                        else:
                            availablemovesanimated = []
                            if [w_queen.pos[0], w_queen.pos[1]-1] in availablemoves:
                               availablemoves.remove([w_queen.pos[0], w_queen.pos[1]-1]) 
        if w_knights != []:
            for w_knight in w_knights:
                if not w_knight.selected:
                    if [w_knight.row, w_knight.col] not in positions:
                        positions.append([w_knight.row, w_knight.col])
                w_knight.draw(canvas)
                if w_knight.selected == True:
                    availablemoves = []
                    availablemovesanimated = []
                    find_available_moves(w_knight)
                    if [w_knight.pos[0], w_knight.pos[1]-1] in availablemoves:
                        availablemoves.remove([w_knight.pos[0], w_knight.pos[1]-1]) 
        
        if w_kings != []:
            for w_king in w_kings:
                if not w_king.selected:
                    if [w_king.row, w_king.col] not in positions:
                        availablemoves = []
                        availablemovesanimated = []
                        positions.append([w_king.row, w_king.col])
                w_king.draw(canvas)
                if w_king.selected == True:
                    find_available_moves(w_king)
                    if [w_king.pos[0], w_king.pos[1]-1] in availablemoves:
                               availablemoves.remove([w_king.pos[0], w_king.pos[1]-1])
        if w_pawns != []:
            for w_pawn in w_pawns:
                if not w_pawn.selected:
                    if [w_pawn.row, w_pawn.col] not in positions:
                        availablemoves = []
                        availablemovesanimated = []
                        positions.append([w_pawn.row, w_pawn.col])
                w_pawn.draw(canvas)
                #pawn upgrades if it is at the top of the screen
                if w_pawn.row == 0:
                    w_pawn.upgrade = True
                if w_pawn.selected:
                    find_available_moves(w_pawn)
        
        #makes sure pieces can go through door when it is open    
        if door_list != []:
            if crate_list != []:
                for door in door_list:
                    if door.activated == True:
                        block_numbers = list(range(1, 34)) + crates
                    else:
                        block_numbers = list(range(1, 34)) + crates + doors
            elif door.activated == True:
                block_numbers = list(range(1, 34))
            else:
                block_numbers = list(range(1, 34)) + doors
        #makes sure pieces can go to where the crate used to be after it is destroyed
        elif crate_list != []:
            block_numbers = list(range(1, 34)) + crates
        else:            
            block_numbers = list(range(1, 34))
        block_numbers.remove(30)
        if b_king != []:
            b_king[0].update()
            b_king[0].draw(canvas)
            
        for move in availablemoves:
            animatedmove = Animated_circle(move, circle_time, delay)
            availablemovesanimated.append(animatedmove)
            
        for moves in availablemovesanimated:
            moves.draw(canvas)
            moves.update()

        for piece in piece_list:
            if piece.falling == True:
                legalmove = False
        #makes squares the player can move the piece to visible          
        if current_scene != 'guide':
            for line in range(0, 20):
                canvas.draw_line((0, line * TILE_SIZE[0]), (WIDTH, line * TILE_SIZE[0]), 0.3, 'white')
                canvas.draw_line((line * TILE_SIZE[0], 0), (line * TILE_SIZE[0], HEIGHT), 0.3, 'white')
    if current_scene == 'guide':

        canvas.draw_image(CHESS_MOVES, 
                          (WIDTH / 2, HEIGHT / 2),
                          (WIDTH, HEIGHT),
                          (WIDTH / 2, HEIGHT / 2),
                          (WIDTH, HEIGHT))
            
        draw_scene = scene_guide1
        for piece in piece_list:
            piece.selected = False
    if current_scene == 'guide 2':
        canvas.draw_image(CHESS_MOVES2, 
                      (WIDTH / 2, HEIGHT / 2),
                      (WIDTH, HEIGHT),
                      (WIDTH / 2, HEIGHT / 2),
                      (WIDTH, HEIGHT))
        draw_scene = scene_guide2
 
    draw_scene.draw(canvas)
    
    #draws tutorial scenes in the game
    if "tutorial" in current_scene:
        scene_and_scene_number = current_scene.split()
        if len(scene_and_scene_number) == 2:
            scene_num = int(scene_and_scene_number[1])
            #displays dialogue depending on the scene the player is on
            if 1 <= scene_num <= 9 or scene_num == 12 or 26 <= scene_num <= 27 or 29 <= scene_num <= 31:
                
                draw_scene = scene_tutorials[scene_num]
                cguidedialogues[scene_num].draw(canvas)
                cguidedialogues[scene_num].update()
            
            elif scene_num == 10 or scene_num == 24:
                #tutorial levels the player can play on    
                draw_scene = scene_tutorials[scene_num]
                
                if b_king != []:    
                    if b_king[0].dead == True:
                            draw_scene = scene_tutorials[scene_num+1]
                            
                            cguidedialogues[scene_num+1].draw(canvas)
                            cguidedialogues[scene_num+1].update()
                    else:
                        TALKING_SOUND.rewind()
            elif scene_num == 13:
                draw_scene = scene_tutorials[scene_num+1]
                cguidedialogues[scene_num].draw(canvas)
                cguidedialogues[scene_num].update()
    
            elif scene_num == 15:
                draw_scene = scene_tutorials[scene_num]
                canvas.draw_image(CHESS_MOVES, 
                      (width / 2, height / 2),
                      (width, height),
                      (WIDTH / 2, HEIGHT / 2),
                      (WIDTH, HEIGHT))
                TALKING_SOUND.rewind()
                
                draw_scene = scene_tutorials[scene_num]
                draw_scene.draw(canvas)
            
            elif scene_num == 16:
                canvas.draw_image(CHESS_MOVES2, 
                                  (width / 2, height / 2),
                                  (width, height),
                                  (WIDTH / 2, HEIGHT / 2),
                                  (WIDTH, HEIGHT))
                draw_scene = scene_tutorials[scene_num]
                draw_scene.draw(canvas)
                
            elif 17 <= scene_num <= 23:
                draw_scene = scene_tutorials[scene_num]
                cguidedialogues[scene_num-2].draw(canvas)
                cguidedialogues[scene_num-2].update()
                
        
        elif len(scene_and_scene_number) == 3:
            unselectpieces()
            availablemoves = []
            availablemovesanimated = []
            unselectpieces()
            draw_scene = scene_tutorials[29]
            cguidedialogues[23].draw(canvas)
            cguidedialogues[23].update()
        else:
            unselectpieces()
            availablemoves = []
            availablemovesanimated = []
            draw_scene = scene_tutorials[30]
            cguidedialogues[24].draw(canvas)
            cguidedialogues[24].update()
    for pawn in w_pawns:
        if pawn.upgrade:
            upgrademenu = True
            #plays a pop in animation for the upgrade menu
            if upgradeanimation == 0:	
                PIECE_UPGRADE.rewind()
                PIECE_UPGRADE.play()
            if 320 + upgradeanimation < 640:    
                upgradeanimation += 30
            else:
                upgradeanimation = 320
            
            canvas.draw_image(CHOOSEPIECE,
                          (WIDTH/2, HEIGHT/2),
                          (WIDTH, HEIGHT),
                          (WIDTH/2, HEIGHT/2),
                          (320 + upgradeanimation * 2, 180 + upgradeanimation))
            button_queen = Button([WIDTH/2 - 305,HEIGHT/2],
                          (lvlbutton_width/4+15,
                           lvlbutton_height/4-30),
                          NOTHING, current_level)
    
            button_bishop = Button([WIDTH/2 - 96,HEIGHT/2],
                                   (lvlbutton_width/4+3,
                                    lvlbutton_height/4-30),
                                   NOTHING, current_level)

            button_rook = Button([WIDTH/2 + 108,HEIGHT/2],
                                 (lvlbutton_width/4+3,
                                  lvlbutton_height/4-30),
                                 NOTHING, current_level)

            button_knight = Button([WIDTH/2 + 312,HEIGHT/2],
                                   (lvlbutton_width/4+3,
                                    lvlbutton_height/4-30),
                                   NOTHING,
                                   current_level)
            button_upgradepieces = [button_queen, button_bishop, button_rook, button_knight]  
            scene_upgradepiece = Scene('upgrade piece', [button_restartlvl, button_levelback] + button_upgradepieces)
            current_scene = 'upgrade piece'
             
            for button in button_upgradepieces:
                button.draw(canvas)
                
            draw_scene = scene_upgradepiece
            
update_image_dictionary()
new_game()
frame = simplegui.create_frame("Chess Climb", WIDTH, HEIGHT)
frame.set_draw_handler(draw)
frame.set_mouseclick_handler(mouse_click)
frame.start()
