---
layout: post
title: BASIC Computer Games (1973) Porting from BASIC to Python in 2022
date: 2022-07-07 18:19:00
tags: "Open Source"
---
## BASIC Computer Games (1973): Porting from BASIC to Python in 2022

The first programming language I learned was **BASIC** on **Microsoft's QBASIC IDE**.

When I was growing up in Cairo, I enjoyed sneaking into the computer lab at my school to run BASIC programs I would type up from books & magazines. If I didn't have a new program to test out, modify, and run, *I would be trying to play **DOOM II** instead.*

Those were simpler times.

The BASIC code I would run was also for simpler programs.

But parsing through BASIC code from back in the 80s was anything but simple - especially with the proliferation of GOTOs and unplanned and erratic program flow.

After what is probably 18 years since I last touched BASIC, I recently stumbled upon [Jeff Atwood's open source project](https://github.com/coding-horror/basic-computer-games) to convert David H. Ahl's *"BASIC Computer Games"* into modern memory-safe programming languages.

I resolved to port game #56 which was a modification of Conway's *"Game of Life"* to support 2 players. *"Life for Two"* is a refreshing simulation of competition, growth, death, and survival based on a simple ruleset with emergent outcomes.

The original BASIC code is reproduced as follows:

```basic
2 PRINT TAB(33);"LIFE2"
4 PRINT TAB(15);"CREATIVE COMPUTING  MORRISTOWN, NEW JERSEY"
6 PRINT: PRINT: PRINT
7 DIM N(6,6),K(18),A(16),X(2),Y(2)
8 DATA 3,102,103,120,130,121,112,111,12
9 DATA 21,30,1020,1030,1011,1021,1003,1002,1012
10 FOR M=1 TO 18: READ K(M): NEXT M
13 DATA -1,0,1,0,0,-1,0,1,-1,-1,1,-1,-1,1,1,1
14 FOR O1= 1 TO 16: READ A(O1): NEXT O1
20 GOTO 500
50 FOR J=1 TO 5
51 FOR K=1 TO 5
55 IF N(J,K)>99 THEN GOSUB 200
60 NEXT K
65 NEXT J
90 K=0: M2=0: M3=0
99 FOR J=0 TO 6: PRINT
100 FOR K=0 TO 6
101 IF J<>0 THEN IF J<>6 THEN 105
102 IF K=6 THEN PRINT 0;: GOTO 125
103 PRINT K;: GOTO 120
105 IF K<>0 THEN IF K<>6 THEN 110
106 IF J=6 THEN PRINT 0: GOTO 126
107 PRINT J;: GOTO 120
110 GOSUB 300
120 NEXT K
125 NEXT J
126 RETURN
200 B=1: IF N(J,K)>999 THEN B=10
220 FOR O1= 1 TO 15 STEP 2
230 N(J+A(O1),K+A(O1+1))=N(J+A(O1),K+A(O1+1))+B
231 NEXT O1
239 RETURN
300 IF N(J,K)<3 THEN 399
305 FOR O1=1 TO 18
310 IF N(J,K)=K(O1) THEN 350
315 NEXT O1
320 GOTO 399
350 IF O1>9 THEN 360
351 N(J,K)=100: M2=M2+1: PRINT " * ";
355 RETURN
360 N(J,K)=1000: M3=M3+1: PRINT " # ";
365 RETURN
399 N(J,K)=0: PRINT "   ";: RETURN
500 PRINT TAB(10);"U.B. LIFE GAME"
505 M2=0: M3=0
510 FOR J=1 TO 5
511 FOR K=1 TO 5
515 N(J,K)=0
516 NEXT K
517 NEXT J
519 FOR B=1 TO 2: P1=3: IF B=2 THEN P1=30
520 PRINT:PRINT "PLAYER";B;" - 3 LIVE PIECES."
535 FOR K1=1 TO 3: GOSUB 700
540 N(X(B),Y(B))=P1: NEXT K1
542 NEXT B
559 GOSUB 90
560 PRINT: GOSUB 50
570 IF M2=0 THEN IF M3=0 THEN 574
571 IF M3=0 THEN B=1: GOTO 575
572 IF M2=0 THEN B=2: GOTO 575
573 GOTO 580
574 PRINT: PRINT "A DRAW":GOTO 800
575 PRINT: PRINT "PLAYER";B;"IS THE WINNER":GOTO 800
580 FOR B=1 TO 2: PRINT: PRINT: PRINT "PLAYER";B;: GOSUB 700
581 IF B=99 THEN 560
582 NEXT B
586 N(X(1),Y(1))=100: N(X(2),Y(2))=1000
596 GOTO 560
700 PRINT "X,Y":PRINT"XXXXXX";CHR$(13);"$$$$$$";CHR$(13);"&&&&&&";
701 PRINT CHR$(13);: INPUT Y(B),X(B)
705 IF X(B)<=5 THEN IF X(B)>0 THEN 708
706 GOTO 750
708 IF Y(B)<=5 THEN IF Y(B)>0 THEN 715
710 GOTO 750
715 IF N(X(B),Y(B))<>0 THEN 750
720 IF B=1 THEN RETURN
725 IF X(1)=X(2) THEN IF Y(1)=Y(2) THEN 740
730 RETURN
740 PRINT "SAME COORD.  SET TO 0"
741 N(X(B)+1,Y(B)+1)=0: B=99: RETURN
750 PRINT "ILLEGAL COORDS. RETYPE": GOTO 700
999 END
```

This wasn't just a fantastic means of keeping a publication and the contribution to programming it had in the 80s alive, but also a unique project in historical game preservation.

It was a refreshing chance for me to sit down with a print out of the BASIC code and start dissecting all the subroutines and map out a coherent structure which I could then port.

The language I chose to port to in the end was Python, with the following being my own best attempt:

```python
'''
LIFE FOR TWO
Competitive Game of Life (two or more players).
Ported by Sajid Sarker (2022).
'''

from typing import List

# Global Variable Initialisation
gn: List[int] = []
gx: List[int] = []
gy: List[int] = []
gk: List[int] = [0, 3, 102, 103, 120, 130, 121, 112, 111, 12, 21, 30, 1020, 1030, 1011, 1021, 1003, 1002, 1012]
ga: List[int] = [0, -1, 0, 1, 0, 0, -1, 0, 1, -1, -1, 1, -1, -1, 1, 1, 1]
m2: int = 0
m3: int = 0

# Initialise the board
for j in range(6):
    gn.append([])
    for k in range(6):
        gn[j].append(0)

for i in range(3):
    gx.append(0)
    gy.append(0)

# Helper Functions
def tab(number : int) -> str:
    t = ""
    while len(t) < number:
        t += " "
    return t

def display_header() -> None:
    print("{}LIFE2".format(tab(33)))
    print("{}CREATIVE COMPUTING  MORRISTOWN, NEW JERSEY\n\n\n".format(tab(15)))
    print("{}U.B. LIFE GAME".format(tab(10)))

# Board Functions
def setup_board() -> None:
    # Players add symbols to initially setup the board
    for b in range(1, 3):
        p1 = 3 if b != 2 else 30
        print("\nPLAYER {} - 3 LIVE PIECES.".format(b))
        for k1 in range(1, 4):
            query_player(b)
            gn[gx[b]][gy[b]] = p1

def modify_board() -> None:
    # Players take turns to add symbols and modify the board
    for b in range(1, 3):
        print("PLAYER {} ".format(b))
        query_player(b)
        if b == 99:
            break
    if b <= 2:
        gn[gx[1]][gy[1]] = 100
        gn[gx[2]][gy[2]] = 1000

def simulate_board() -> None:
    # Simulate the board for one step
    for j in range(1, 6):
        for k in range(1, 6):
            if gn[j][k] > 99:
                b = 1 if gn[j][k] <= 999 else 10
                for o1 in range(1, 16, 2):
                    gn[j + ga[o1] - 1][k + ga[o1 + 1] - 1] = gn[j + ga[o1] - 1][k + ga[o1 + 1] - 1] + b
                    #gn[j + ga[o1]][k + ga[o1 + 1]] = gn[j + ga[o1]][k + ga[o1 + 1]] + b

def display_board() -> None:
    # Draws the board with all symbols
    m2, m3 = 0, 0
    for j in range(7):
        print("")
        for k in range(7):
            if j == 0 or j == 6:
                if k != 6:
                    print(" " + str(k) + " ", end="")
                else:
                    print(" 0 ", end="")
            elif k == 0 or k == 6:
                if j != 6:
                    print(" " + str(j) + " ", end="")
                else:
                    print(" 0\n")
            else:
                if gn[j][k] < 3:
                    gn[j][k] = 0
                    print("   ", end="")
                else:
                    for o1 in range(1, 19):
                        if gn[j][k] == gk[o1]:
                            break
                    if o1 <= 18:
                        if o1 > 9:
                            gn[j][k] = 1000
                            m3 += 1
                            print(" # ", end="")
                        else:
                            gn[j][k] = 100
                            m2 += 1
                            print(" * ", end="")
                    else:
                        gn[j][k] = 0
                        print("   ", end="")

# Player Functions
def query_player(b) -> None:
    # Query player for symbol placement coordinates
    while True:
        print("X,Y\nXXXXXX\n$$$$$$\n&&&&&&")
        a_: List[str] = input("??")
        b_: List[str] = input("???")
        x_: List[int] = [int(num) for num in a_.split() if num.isdigit()]
        y_: List[int] = [int(num) for num in b_.split() if num.isdigit()]
        x_ = [0] if len(x_) == 0 else x_
        y_ = [0] if len(y_) == 0 else y_
        gx[b] = y_[0]
        gy[b] = x_[0]
        if gx[b] in range(1, 6) and gy[b] in range(1, 6) and gn[gx[b]][gy[b]] == 0:
            break
        print("ILLEGAL COORDS. RETYPE")
    if b != 1:
        if gx[1] == gx[2] and gy[1] == gy[2]:
            print("SAME COORD. SET TO 0")
            gn[gx[b] + 1][gy[b] + 1] = 0
            b = 99

# Game Functions
def check_winner(m2 : int, m3 : int) -> None:
    # Check if the game has been won
    if m2 == 0 and m3 == 0:
        print("\nA DRAW\n")
        return
    if m3 == 0:
        print("\nPLAYER 1 IS THE WINNER\n")
        return
    if m2 == 0:
        print("\nPLAYER 2 IS THE WINNER\n")
        return

# Program Flow
def main() -> None:
    display_header()
    setup_board()
    display_board()
    while True:
        print("\n")
        simulate_board()
        display_board()
        check_winner(m2, m3)
        modify_board()

if __name__ == "__main__":
    main()
```

I anticipate there are certain bugs but for the life of me, I could not tell you the exact place where I went wrong. The GOTOs for this particular game was almost horrendous sifting through, but I do admire how much this game achieves in such few lines!

It's just fascinating to watch an old program come alive in the **Terminal**, with noticeably different code, [the same way it had done back in the day](https://coding-horror.github.io/basic-computer-games/).

Here's to hoping my pull request is approved, and others with a similar interest and curiosity (and far far more patience than I presently have) can contribute to patching it!
