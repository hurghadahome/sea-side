import random

x, x1, x2, x3, x4, x5, x6, x7, x8, x9, x10 = 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0
y, y1, y2, y3, y4, y5, y6, y7, y8, y9, y10 = 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0

# карта короблей робота
filedrobot = [[" "] * 7 for i in range(8)]

# карта короблей человека
filed = [[" "] * 7 for i in range(8)]

# карта короблей робота без короблей пустая
showbotempty = [[" "] * 7 for i in range(8)]

# координаты выстрелов
n = 0
m = 0
h = 0
h1 = 0

g1 = [[' ', ' ', ' ', ' ', ' ', ' ', ' '],
      [' ', ' ', 'Т', 'Ы', ' ', ' ', ' '],
      [' ', ' ', ' ', ' ', ' ', ' ', ' '],
      [' ', 'П', 'Р', 'О', 'И', 'Г', ' '],
      [' ', ' ', ' ', ' ', ' ', ' ', ' '],
      [' ', 'Р', 'А', 'Л', '!', '!', ' '],
      [' ', ' ', ' ', ' ', ' ', ' ', ' '],
      [' ', ' ', ' ', ' ', ' ', ' ', ' ']]

g = [[' ', ' ', ' ', ' ', ' ', ' ', ' '],
     ['П', 'О', 'Б', 'Е', 'Д', 'А', ' '],
     [' ', ' ', ' ', ' ', ' ', ' ', ' '],
     ['П', 'О', 'Б', 'Е', 'Д', 'А', ' '],
     [' ', ' ', ' ', ' ', ' ', ' ', ' '],
     ['П', 'О', 'Б', 'Е', 'Д', 'А', ' '],
     [' ', ' ', ' ', ' ', ' ', ' ', ' '],
     [' ', ' ', ' ', ' ', ' ', ' ', ' ']]

#..........................................................................................

# консоль проиграл
def showg1():
    print()
    print("   | 1 | 2 | 3 | 4 | 5 | 6 |")
    print(" --------------------------- ")
    for i, row in enumerate(g1):
        if i != 0 and i != 7:
            row_str = f" {i} | {' | '.join(map(str, row))} "
            print(row_str)
            print(" ---------------------------- ")

#..........................................................................................

# консоль выиграл
def showg():
    print()
    print("   | 1 | 2 | 3 | 4 | 5 | 6 |")
    print(" --------------------------- ")
    for i, row in enumerate(g):
        if i != 0 and i != 7:
            row_str = f" {i} | {' | '.join(map(str, row))} "
            print(row_str)
            print(" ---------------------------- ")

#..........................................................................................

# консоль робота
def showbot():
    print()
    print("   |1р |2о |3б |4о |5т | 6 |")
    print(" --------------------------- ")
    for i, row in enumerate(filedrobot):
        if i != 0 and i != 7:
            row_str = f" {i} | {' | '.join(map(str, row))} "
            print(row_str)
            print(" ---------------------------- ")

#..........................................................................................

# консоль робота пустая
def showshowbotempty():
    print()
    print("   |1р |2о |3б |4о |5т | 6 |")
    print(" --------------------------- ")
    for i, row in enumerate(showbotempty):
        if i != 0 and i != 7:
            row_str = f" {i} | {' | '.join(map(str, row))} "
            print(row_str)
            print(" ---------------------------- ")

#..........................................................................................


# консоль человека
def showhuman():
    print()
    print("  ч|1е |2л |3о |4в |5е |6к |")
    print(" --------------------------- ")
    for i, row in enumerate(filed):
        if i != 0 and i != 7:
            row_str = f" {i} | {' | '.join(map(str, row))} "
            print(row_str)
            print(" ---------------------------- ")

#..........................................................................................

# условия при которых выигрывает бот
def victorybot():
    global h
    h = 0
    for i in filed:
        for e in i:
            if e == 'X':
                h += 1
            if h == 10:
                showg()
                print("РОБОТ ПОБЕДИЛ!")

#..........................................................................................

# условия при которых выигрывает человек
def victory():
    global h1
    h1 = 0
    for i in filedrobot:
        for e in i:
            if e == 'X':
                h1 += 1
            if h1 == 10:
                showg()
            print("ТЫ МОЙ ГЕРОЙ! ТЫ ПОБЕДИЛ!")

#..........................................................................................

# выстрел робота и его поподания
def robotshot():
    global n
    global m

    showhuman()  # консоль человека три палубы

    victorybot()

    while True:

        n = random.randint(1, 6)
        m = random.randint(1, 6)

        m -= 1

        if filed[n][m] == 'O':
            print(" Вы сюда уже стреляли! ")
            continue
        if filed[n][m] == 'X':
            print(" Вы сюда уже стреляли! ")
            continue

        if filed[n][m] == "K":
            filed[n][m] = "X"
            showhuman()  # консоль человека три палубы
            print("Робот попал!")
            robotshot()
        else:
            filed[n][m] = "O"
            showhuman()  # консоль человека три палубы
            print("Робот не попал дальше стреляет человек!")
            humanshot()

#..........................................................................................

# вастрел человека и его поподания
def humanshot():

    showbot()

    showshowbotempty()  # консоль робота пустая
    print(f"Человек:{h1} Робот:{h}")
    showhuman()
    print("Робот не попал дальше стреляет человек!")

    victory()
    victorybot()

    global n
    global m

    while True:

        print("Введите координаты выстрела!")
        n = input("Номер строки x1:")
        m = input("Номер столбцаY1:")

        if not (n.isdigit()) or not (m.isdigit()):
            print(" Введите числа! ")
            continue

        n, m = int(n), int(m)

        if 1 > n or n > 6 or 1 > m or m > 6:
            print(" Координаты вне диапазона! ")
            continue

        m -= 1

        if filedrobot[n][m] == 'O':
            print(" Вы сюда уже стреляли! ")
            continue
        if filedrobot[n][m] == 'X':
            print(" Вы сюда уже стреляли! ")
            continue

        if filedrobot[n][m] == 'K':  # карта короблей робота
            filedrobot[n][m] = 'X'  # карта короблей робота
            showbotempty[n][m] = 'X'  # карта короблей робота без кораблей
            showshowbotempty()  # консоль робота пустая
            print("Вы попали вам разрешен еще выстрел!")
            humanshot()
        else:
            filedrobot[n][m] == ' '
            filedrobot[n][m] = 'O'  # карта короблей робота
            showbotempty[n][m] = 'O'  # карта короблей робота без кораблей
            print("Вы не попали, дальше стреляет робот!")
            robotshot()

#..........................................................................................

# построение ботом трехпалубного коробля
class Maxbot_bot():

    def __init__(self, x7, y7, x8, y8, x9, y9):
        self.x3 = x7
        self.y3 = y7
        self.x4 = x8
        self.y4 = y8
        self.x5 = x9
        self.y5 = y9

    def ask_maxbot_bot(self):

        global x7
        global y7

        while True:

            x7 = random.randint(1, 6)
            y7 = random.randint(1, 6)

            y7 -= 1

            if filedrobot[x7][y7 - 1] == " " \
                    and filedrobot[x7][y7 + 1] == " " \
                    and filedrobot[x7 - 1][y7] == " " \
                    and filedrobot[x7 + 1][y7] == " " \
                    and filedrobot[x7 - 1][y7 - 1] == " " \
                    and filedrobot[x7 + 1][y7 - 1] == " " \
                    and filedrobot[x7 + 1][y7 + 1] == " " \
                    and filedrobot[x7 - 1][y7 + 1] == " ":
                print()
            else:
                print()
                continue

            filedrobot[x7][y7] = 'K'

            global x8
            global y8

            x8 = random.randint(1, 6)
            y8 = random.randint(1, 6)

            if y8 == y7 or x8 == x7:
                print()
            else:
                print()
                filedrobot[x7][y7] = " "
                continue

            y8 -= 1

            if filedrobot[x8][y8] != " ":
                print()
                filedrobot[x7][y7] = " "
                continue

            if y7 == y8 and x8 == x7 + 1 \
                    and filedrobot[x8 + 1][y8 - 1] == " " \
                    and filedrobot[x8 + 1][y8] == " " \
                    and filedrobot[x8 - 1][y8 - 1] == " ":
                print()
            elif y7 == y8 and x8 == x7 - 1 \
                    and filedrobot[x8 - 1][y8 - 1] == " " \
                    and filedrobot[x8 - 1][y8] == " " \
                    and filedrobot[x8 - 1][y8 + 1] == " ":
                print()
            elif x7 == x8 and y8 == y7 - 1 \
                    and filedrobot[x8 - 1][y8 - 1] == " " \
                    and filedrobot[x8][y8 - 1] == " " \
                    and filedrobot[x8 + 1][y8 - 1] == " ":
                print()
            elif x7 == x8 and y8 == y7 + 1 \
                    and filedrobot[x8 - 1][y8 + 1] == " " \
                    and filedrobot[x8][y8 + 1] == " " \
                    and filedrobot[x8 - 1][y8 + 1] == " ":
                print()
            else:
                filedrobot[x7][y7] = " "
                print()
                continue

            filedrobot[x8][y8] = 'K'

            global x9
            global y9

            x9 = random.randint(1, 6)
            y9 = random.randint(1, 6)

            if y9 == y7 and y8 == y7 or x9 == x7 or y8 == y7:
                print()
            else:
                print()
                filedrobot[x7][y7] = " "
                filedrobot[x8][y8] = " "
                continue

            y9 -= 1

            if filedrobot[x9][y9] != " ":
                print()
                filedrobot[x7][y7] = " "
                filedrobot[x8][y8] = " "
                continue

            # ВНИЗ
            if y9 == y8 and x9 == x8 + 1 or y9 == y7 and x9 == x7 + 1 \
                    and filedrobot[x9 + 1][y9 - 1] == " " \
                    and filedrobot[x9 + 1][y9] == " " \
                    and filedrobot[x9 + 1][y9 + 1] == " ":
                print()

            # ВВЕРХ
            elif y9 == y8 and x9 == x8 - 1 or y9 == y7 and x9 == x7 - 1 \
                    and filedrobot[x9 - 1][y9 - 1] == " " \
                    and filedrobot[x9 - 1][y9] == " " \
                    and filedrobot[x9 - 1][y9 + 1] == " ":
                print()

            # ВЛЕВО
            elif x9 == x8 and y9 == y8 - 1 or x9 == x7 and y9 == y7 - 1 \
                    and filedrobot[x9 - 1][y9 - 1] == " " \
                    and filedrobot[x9][y9 - 1] == " " \
                    and filedrobot[x9 + 1][y9 - 1] == " ":
                print()

            # ВПРАВО
            elif x9 == x8 and y9 == y8 + 1 or x9 == x7 and y9 == y7 + 1 \
                    and filedrobot[x8 - 1][y8 + 1] == " " \
                    and filedrobot[x8][y8 + 1] == " " \
                    and filedrobot[x8 + 1][y8 + 1] == " ":
                print()

            else:
                filedrobot[x7][y7] = " "
                filedrobot[x8][y8] = " "
                print()
                continue

            filedrobot[x9][y9] = 'K'
            showshowbotempty()
            showhuman()
            break

# \\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\

# построение ботом двухпалубных короблей
class Averagebot_bot():

    def __init__(self, x3, y3, x4, y4, x5, y5, x6, y6):
        self.x3 = x3
        self.y3 = y3
        self.x4 = x4
        self.y4 = y4
        self.x5 = x5
        self.y5 = y5
        self.x6 = x6
        self.y6 = y6

    def ask_averagebot_bot(self):

        global x3
        global y3

        while True:

            x3 = random.randint(1, 6)
            y3 = random.randint(1, 6)

            y3 -= 1

            if filedrobot[x3][y3] != " ":
                print()
                continue

            if filedrobot[x3][y3 - 1] == " " \
                    and filedrobot[x3][y3 + 1] == " " \
                    and filedrobot[x3 - 1][y3] == " " \
                    and filedrobot[x3 + 1][y3] == " " \
                    and filedrobot[x3 - 1][y3 - 1] == " " \
                    and filedrobot[x3 + 1][y3 - 1] == " " \
                    and filedrobot[x3 + 1][y3 + 1] == " " \
                    and filedrobot[x3 - 1][y3 + 1] == " ":
                print()
            else:
                print()
                showbot()
                continue
            filedrobot[x3][y3] = 'K'

            global x4
            global y4

            x4 = random.randint(1, 6)
            y4 = random.randint(1, 6)

            y4 -= 1

            if filedrobot[x4][y4] != " ":
                print()
                filedrobot[x3][y3] = " "
                continue

            if y4 == y3 or x4 == x3:
                print()
            else:
                print()
                filedrobot[x3][y3] = " "
                continue

            if y3 == y4 and x4 == x3 + 1 \
                    and filedrobot[x4 + 1][y4 - 1] == " " \
                    and filedrobot[x4 + 1][y4] == " " \
                    and filedrobot[x4 - 1][y4 - 1] == " ":
                print()
            elif y3 == y4 and x4 == x3 - 1 \
                    and filedrobot[x4 - 1][y4 - 1] == " " \
                    and filedrobot[x4 - 1][y4] == " " \
                    and filedrobot[x4 - 1][y4 + 1] == " ":
                print()
            elif x3 == x4 and y4 == y3 - 1 \
                    and filedrobot[x4 - 1][y4 - 1] == " " \
                    and filedrobot[x4][y4 - 1] == " " \
                    and filedrobot[x4 + 1][y4 - 1] == " ":
                print()
            elif x3 == x4 and y4 == y3 + 1 \
                    and filedrobot[x4 - 1][y4 + 1] == " " \
                    and filedrobot[x4][y4 + 1] == " " \
                    and filedrobot[x4 - 1][y4 + 1] == " ":
                print()

            else:
                filedrobot[x3][y3] = " "

                print()
                continue

            filedrobot[x4][y4] = 'K'

            print()

            break

        while True:

            x5 = random.randint(1, 6)
            y5 = random.randint(1, 6)

            y5 -= 1

            if filedrobot[x5][y5] != " ":
                print()
                continue

            if filedrobot[x5][y5 - 1] == " " \
                    and filedrobot[x5][y5 + 1] == " " \
                    and filedrobot[x5 - 1][y5] == " " \
                    and filedrobot[x5 + 1][y5] == " " \
                    and filedrobot[x5 - 1][y5 - 1] == " " \
                    and filedrobot[x5 + 1][y5 - 1] == " " \
                    and filedrobot[x5 + 1][y5 + 1] == " " \
                    and filedrobot[x5 - 1][y5 + 1] == " ":
                print()
            else:
                print()
                showbot()
                continue
            filedrobot[x5][y5] = 'K'

            global x6
            global y6

            x6 = random.randint(1, 6)
            y6 = random.randint(1, 6)

            y6 -= 1

            if filedrobot[x6][y6] != " ":
                print()
                filedrobot[x5][y5] = " "
                continue

            if y6 == y5 or x6 == x5:
                print()
            else:
                print()
                filedrobot[x5][y5] = " "
                continue

            if y5 == y6 and x6 == x5 + 1 \
                    and filedrobot[x6 + 1][y6 - 1] == " " \
                    and filedrobot[x6 + 1][y6] == " " \
                    and filedrobot[x6 - 1][y6 - 1] == " ":
                print()
            elif y5 == y6 and x6 == x5 - 1 \
                    and filedrobot[x6 - 1][y6 - 1] == " " \
                    and filedrobot[x6 - 1][y6] == " " \
                    and filedrobot[x6 - 1][y6 + 1] == " ":
                print()
            elif x5 == x6 and y6 == y5 - 1 \
                    and filedrobot[x6 - 1][y6 - 1] == " " \
                    and filedrobot[x6][y6 - 1] == " " \
                    and filedrobot[x6 + 1][y6 - 1] == " ":
                print()
            elif x5 == x4 and y6 == y5 + 1 \
                    and filedrobot[x6 - 1][y6 + 1] == " " \
                    and filedrobot[x6][y6 + 1] == " " \
                    and filedrobot[x6 - 1][y6 + 1] == " ":
                print()

            else:
                filedrobot[x5][y5] = " "

                print()
                continue

            filedrobot[x6][y6] = 'K'
            showbot()
            showshowbotempty()
            print("Коробли робота расставлены!")
            break

# \\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\

# построение ботом однопалубных короблей
class Minibot_bot():

    def __init__(self, x, y, x1, y1, x2, y2):
        self.x = x
        self.y = y
        self.x1 = x1
        self.y1 = y1
        self.x2 = x2
        self.y2 = y2

    def ask_minibot_bot(self):

        global x
        global y

        while True:

            x = random.randint(1, 6)
            y = random.randint(1, 6)

            y -= 1

            if filedrobot[x][y] != " ":
                print()
                continue

            if filedrobot[x][y - 1] == " " \
                    and filedrobot[x][y + 1] == " " \
                    and filedrobot[x - 1][y] == " " \
                    and filedrobot[x + 1][y] == " " \
                    and filedrobot[x - 1][y - 1] == " " \
                    and filedrobot[x + 1][y - 1] == " " \
                    and filedrobot[x + 1][y + 1] == " " \
                    and filedrobot[x - 1][y + 1] == " ":
                print()
            else:
                print()
                continue

            filedrobot[x][y] = 'K'
            print()

            break

        global x1
        global y1

        while True:

            x1 = random.randint(1, 6)
            y1 = random.randint(1, 6)

            y1 -= 1

            if filedrobot[x1][y1] != " ":
                print()
                continue

            if filedrobot[x1][y1 - 1] == " " \
                    and filedrobot[x1][y1 + 1] == " " \
                    and filedrobot[x1 - 1][y1] == " " \
                    and filedrobot[x1 + 1][y1] == " " \
                    and filedrobot[x1 - 1][y1 - 1] == " " \
                    and filedrobot[x1 + 1][y1 - 1] == " " \
                    and filedrobot[x1 + 1][y1 + 1] == " " \
                    and filedrobot[x1 - 1][y1 + 1] == " ":
                print()
            else:
                print()
                continue

            filedrobot[x1][y1] = 'K'
            print()

            break

        global x2
        global y2

        while True:

            x2 = random.randint(1, 6)
            y2 = random.randint(1, 6)

            y2 -= 1

            if filedrobot[x2][y2] != " ":
                print()
                continue

            if filedrobot[x2][y2 - 1] == " " \
                    and filedrobot[x2][y2 + 1] == " " \
                    and filedrobot[x2 - 1][y2] == " " \
                    and filedrobot[x2 + 1][y2] == " " \
                    and filedrobot[x2 - 1][y2 - 1] == " " \
                    and filedrobot[x2 + 1][y2 - 1] == " " \
                    and filedrobot[x2 + 1][y2 + 1] == " " \
                    and filedrobot[x2 - 1][y2 + 1] == " ":
                print()
            else:
                print()
                continue

            filedrobot[x2][y2] = 'K'
            showbot()
            print(filedrobot)
            break

# \\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\

# построение трехпалубного коробля
class maxbot():

   def __init__(self, x7, y7, x8, y8, x9, y9):
            self.x3 = x7
            self.y3 = y7
            self.x4 = x8
            self.y4 = y8
            self.x5 = x9
            self.y5 = y9

   def ask_maxbot(self):

       global x7
       global y7

       while True:
           showhuman()
           print("Разместите палубу 1 трехпалубного корабля!")
           x7 = input("Номер строки x1:")
           y7 = input("Номер столбцаY1:")

           if not (x7.isdigit()) or not (y7.isdigit()):
               print(" Введите числа! ")
               continue

           x7, y7 = int(x7), int(y7)

           if 1 > x7 or x7 > 6 or 1 > y7 or y7 > 6:
               print(" Координаты вне диапазона! ")
               continue

           y7 -= 1

           if filed[x7][y7] == "K":

               print(" Клетка занята! ")
               continue

           filed[x7][y7] = "K"
           showhuman()
           print(" Палуба 1 трехпалубного коробля построена! ")

           global x8
           global y8

           print("Разместите палубу 2 трехпалубного корабля корабля!")
           x8 = input("Номер строки x1:")
           y8 = input("Номер столбцаY1:")

           if not (x8.isdigit()) or not (y8.isdigit()):
               print(" Введите числа! ")
               continue

           x8, y8 = int(x8), int(y8)

           if 1 > x8 or x8 > 6 or 1 > y8 or y8 > 6:
               print(" Координаты вне диапазона! ")
               continue

           y8 -= 1

           if filed[x8][y8] == "K":
               print(" Клетка занята! ")
               continue

           if y7 == y8 and x8 == x7 + 1 \
              and filed[x8 + 1][y8 - 1] != "K" \
              and filed[x8 + 1][y8] != "K" \
              and filed[x8 - 1][y8 - 1] != "K":
               print()
           elif y7 == y8 and x8 == x7 - 1 \
                and filed[x8 - 1][y8 - 1] != "K"\
                and filed[x8 - 1][y8] != "K" \
                and filed[x8 - 1][y8 + 1] != "K":
               print()
           elif x7 == x8 and y8 == y7 - 1 \
                and filed[x8 - 1][y8 - 1] != "K" \
                and filed[x8][y8 - 1] != "K" \
                and filed[x8 + 1][y8 - 1] != "K":
               print()
           elif x7 == x8 and y8 == y7 + 1 \
                and filed[x8 - 1][y8 + 1] != "K" \
                and filed[x8][y8 + 1] != "K" \
                and filed[x8 - 1][y8 + 1] != "K":
               print()

           else:
               filed[x7][y7] = " "
               showhuman()
               print( "ВЫСТАВЛЯЙ ПРАВИЛЬНО!" )
               continue

           filed[x8][y8] = "K"
           showhuman()
           print(" Палуба 2 трехпалубного коробля построена! ")
           global x9
           global y9

           print("Разместите палубу 3 трехпалубного корабля корабля!")
           x9 = input("Номер строки x1:")
           y9 = input("Номер столбцаY1:")

           if not (x9.isdigit()) or not (y9.isdigit()):
               print(" Введите числа! ")
               continue

           x9, y9 = int(x9), int(y9)

           if 1 > x9 or x9 > 6 or 1 > y9 or y9 > 6:
               print(" Координаты вне диапазона! ")
               continue

           y9 -= 1

           if filed[x9][y9] == "K":
               print(" Клетка занята! ")
               continue

           if y8 == y7 and y8 != y9 or x8 == x7 and x8 != x9:
               filed[x7][y7] = " "
               filed[x8][y8] = " "
               showhuman()
               print("ВЫСТАВЛЯЙ ПРАВИЛЬНО!")
               continue


           filed[x9][y9] = "K"
           showhuman()
           print(" Трехпалубный карабль построен! ")
           break

#\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\

# построение двухпалубных короблей
class averagebot():

   def __init__(self, x3, y3, x4, y4, x5, y5, x6, y6):
            self.x3 = x3
            self.y3 = y3
            self.x4 = x4
            self.y4 = y4
            self.x5 = x5
            self.y5 = y5
            self.x6 = x6
            self.y6 = y6

   def ask_averagebot(self):

       global x3
       global y3

       while True:
           showhuman()
           print("Разместите первую палубу двухпалубного корабля1!")
           x3 = input("Номер строки x1:")
           y3 = input("Номер столбцаY1:")


           if not (x3.isdigit()) or not (y3.isdigit()):
               print(" Введите числа! ")
               continue

           x3, y3 = int(x3), int(y3)

           if 1 > x3 or x3 > 6 or 1 > y3 or y3 > 6:
               print(" Координаты вне диапазона! ")
               continue

           y3 -= 1

           if filed[x3][y3] != " ":
               print(" Клетка занята! ")
               continue

           if filed[x3][y3 - 1] != "K" \
              and filed[x3][y3 + 1] != "K" \
              and filed[x3 - 1][y3] != "K" \
              and filed[x3 + 1][y3] != "K"  \
              and filed[x3 - 1][y3 - 1] != "K" \
              and filed[x3 + 1][y3 - 1] != "K" \
              and filed[x3 + 1][y3 + 1] != "K" \
              and filed[x3 - 1][y3 + 1] != "K":
               print()
           else:
               print(" Слишком близко к другому караблю! ")
               continue

           filed[x3][y3] = "K"
           showhuman()
           print(" Первая палубу двухпалубного карабля построена! ")

           global x4
           global y4

           print("Разместите вторую палубу двухпклубного корабля1!")
           x4 = input("Номер строки x1:")
           y4 = input("Номер столбцаY1:")

           if not (x4.isdigit()) or not (y4.isdigit()):
               print(" Введите числа! ")
               continue

           x4, y4 = int(x4), int(y4)

           if 1 > x4 or x4 > 6 or 1 > y4 or y4 > 6:
               print(" Координаты вне диапазона! ")
               continue

           y4 -= 1

           if filed[x4][y4] == "K":
               print(" Клетка занята! ")
               continue


           if y3 == y4 and x4 == x3 + 1 \
              and filed[x4 + 1][y4 - 1] != "K" \
              and filed[x4 + 1][y4] != "K" \
              and filed[x4 - 1][y4 - 1] != "K":
               print()
           elif y3 == y4 and x4 == x3 - 1 \
                and filed[x4 - 1][y4 - 1] != "K"\
                and filed[x4 - 1][y4] != "K" \
                and filed[x4 - 1][y4 + 1] != "K":
               print()
           elif x3 == x4 and y4 == y3 - 1 \
                and filed[x4 - 1][y4 - 1] != "K" \
                and filed[x4][y4 - 1] != "K" \
                and filed[x4 + 1][y4 - 1] != "K":
               print()
           elif x3 == x4 and y4 == y3 + 1 \
                and filed[x4 - 1][y4 + 1] != "K" \
                and filed[x4][y4 + 1] != "K" \
                and filed[x4 - 1][y4 + 1] != "K":
               print()

           else:
               filed[x3][y3] = " "
               showhuman()
               print( "ВЫСТАВЛЯЙ ПРАВИЛЬНО!" )
               continue

           filed[x4][y4] = "K"
           showhuman()
           print(" Первый двухпалубный карабль1 построен! ")
           break


       global x5
       global y5

       while True:

           print("Разместите первую палубу двухпалубного корабля2!")
           x5 = input("Номер строки x1:")
           y5 = input("Номер столбцаY1:")

           if not (x5.isdigit()) or not (y5.isdigit()):
               print(" Введите числа! ")
               continue

           x5, y5 = int(x5), int(y5)

           if 1 > x5 or x5 > 6 or 1 > y5 or y5 > 6:
               print(" Координаты вне диапазона! ")
               continue

           y5 -= 1

           if filed[x5][y5] != " ":
               print(" Клетка занята! ")
               continue

           if filed[x5][y5 - 1] != "K" \
                   and filed[x5][y5 + 1] != "K" \
                   and filed[x5 - 1][y5] != "K" \
                   and filed[x5 + 1][y5] != "K" \
                   and filed[x5 - 1][y5 - 1] != "K" \
                   and filed[x5 + 1][y5 - 1] != "K" \
                   and filed[x5 + 1][y5 + 1] != "K" \
                   and filed[x5 - 1][y5 + 1] != "K":
               print()
           else:
               print(" Слишком близко к другому караблю! ")
               continue

           filed[x5][y5] = "K"
           showhuman()
           print(" Первая палубу двухпалубного карабля построена! ")

           global x6
           global y6

           print("Разместите вторую палубу двухпклубного корабля2!")
           x6 = input("Номер строки x1:")
           y6 = input("Номер столбцаY1:")

           if not (x6.isdigit()) or not (y6.isdigit()):
               print(" Введите числа! ")
               continue

           x6, y6 = int(x6), int(y6)

           if 1 > x6 or x6 > 6 or 1 > y6 or y6 > 6:
               print(" Координаты вне диапазона! ")
               continue

           y6 -= 1

           if filed[x6][y6] == "K":
               print(" Клетка занята! ")
               continue

           if y5 == y6 and x6 == x5 + 1 \
                   and filed[x6 + 1][y6 - 1] != "K" \
                   and filed[x6 + 1][y6] != "K" \
                   and filed[x6 - 1][y6 - 1] != "K":
               print()
           elif y5 == y6 and x6 == x5 - 1 \
                   and filed[x6 - 1][y6 - 1] != "K" \
                   and filed[x6- 1][y6] != "K" \
                   and filed[x6 - 1][y6 + 1] != "K":
               print()
           elif x5 == x6 and y6 == y5 - 1 \
                   and filed[x6 - 1][y6 - 1] != "K" \
                   and filed[x6][y6 - 1] != "K" \
                   and filed[x6 + 1][y6 - 1] != "K":
               print()
           elif x5 == x6 and y6 == y5 + 1 \
                   and filed[x6 - 1][y6 + 1] != "K" \
                   and filed[x6][y6 + 1] != "K" \
                   and filed[x6 - 1][y6 + 1] != "K":
               print()

           else:
               filed[x5][y5] = " "
               showhuman()
               print("ВЫСТАВЛЯЙ ПРАВИЛЬНО!")
               continue

           filed[x6][y6] = "K"
           showhuman()
           print(" Первый двухпалубный карабль2 построен! ")
           break

#\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\

# построение однопалубных короблей
class minibot():

    def __init__(self, x, y, x1, y1, x2, y2):
        self.x = x
        self.y = y
        self.x1 = x1
        self.y1 = y1
        self.x2 = x2
        self.y2 = y2

    def ask_minibot(self):


       while True:
           showhuman()
           global x
           global y

           print("Разместите первый однопалубный корабль!")
           x = input("Номер строки x:")
           y = input("Номер столбцаY:")

           if not (x.isdigit()) or not (y.isdigit()):
               print(" Введите числа! ")
               continue

           x, y = int(x), int(y)

           if 1 > x or x > 6 or 1 > y or y > 6:
               print(" Координаты вне диапазона! ")
               continue

           y -= 1

           filed[x][y] = "K"
           showhuman()
           print(" Однопалубный карабль карабль построен! ")
           break

       while True:

           global x1
           global y1

           print("Разместите второй однопалубный корабль!")
           x1 = input("Номер строки x:")
           y1 = input("Номер столбцаY:")

           if not (x1.isdigit()) or not (y1.isdigit()):
               print(" Введите числа! ")
               continue

           x1, y1 = int(x1), int(y1)

           if 1 > x1 or x1 > 6 or 1 > y1 or y1 > 6:
               print(" Координаты вне диапазона! ")
               continue

           y1 -= 1

           if filed[x1][y1] == "K":
               print(" Клетка занята! ")
               continue

           if filed[x1][y1 - 1] != "K" \
              and filed[x1][y1 + 1] != "K" \
              and filed[x1 - 1][y1] != "K" \
              and filed[x1 + 1][y1] != "K" \
              and filed[x1 - 1][y1 - 1] != "K" \
              and filed[x1 + 1][y1 - 1] != "K" \
              and filed[x1 + 1][y1 + 1] != "K" \
              and filed[x1 - 1][y1 + 1] != "K":  # the central cell
              print("Да будет так!")
           else:
               print(" Слишком близко к другому караблю! ")
               continue

           filed[x1][y1] = "K"
           showhuman()
           print(" Второй однопалубный карабль карабль построен! ")
           break

       while True:

           global x2
           global y2

           print("Разместите третий однопалубный корабль!")
           x2 = input("Номер строки x:")
           y2 = input("Номер столбцаY:")

           if not (x2.isdigit()) or not (y2.isdigit()):
               print(" Введите числа! ")
               continue

           x2, y2 = int(x2), int(y2)

           if 1 > x2 or x2 > 6 or 1 > y2 or y2 > 6:
               print(" Координаты вне диапазона! ")
               continue

           y2 -= 1

           if filed[x2][y2] == "K":
               print(" Клетка занята! ")
               continue

           if filed[x2][y2 - 1] != "K" \
              and filed[x2][y2 + 1] != "K" \
              and filed[x2 - 1][y2] != "K" \
              and filed[x2 + 1][y2] != "K" \
              and filed[x2 - 1][y2 - 1] != "K" \
              and filed[x2 + 1][y2 - 1] != "K" \
              and filed[x2 + 1][y2 + 1] != "K" \
              and filed[x2 - 1][y2 + 1] != "K":  # the central cell
              print("Да будет так!")

           else:
              print(" Слишком близко к другому караблю! ")
              continue

           filed[x2][y2] = "K"

           showhuman()
           print(" Третий однопалубный карабль карабль построен! ")
           print(" Корабли готовы к бою! ")
           break

#\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\

maxbot_bot1 = Maxbot_bot(x7, y7, x8, y8, x9, y9)
maxbot_bot1.ask_maxbot_bot()

minibot_bot1 = Minibot_bot(x, y, x1, y1, x2, y2)
minibot_bot1.ask_minibot_bot()

averagebot_bot1 = Averagebot_bot(x3, y3, x4, y4, x5, y5, x6, y6)
averagebot_bot1.ask_averagebot_bot()

maxbot1 = maxbot(x7, y7, x8, y8, x9, y9)
maxbot1.ask_maxbot()

averagebot1 = averagebot(x3, y3, x4, y4, x5, y5, x6, y6)
averagebot1.ask_averagebot()

minibot1 = minibot(x, y, x1, y1, x2, y2)
minibot1.ask_minibot()

victory()
humanshot()
robotshot()
