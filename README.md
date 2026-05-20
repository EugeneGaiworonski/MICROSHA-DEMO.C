#DEFINE LENGTH 7 /*dlina wwodimoj stroki*/
#DEFINE BEGIN [[
#DEFINE END ]]

CHAR *VAL;

MAIN () 
BEGIN
    CHAR BELL[LENGTH];
    INT DIN;
    DIN = 1;
    PUTCHAR('\C');
    PUTS("demonstracionnaq programma");
    NEWLINE();
    PUTS("SARATOV BEST-C COMPILER");
    NEWLINE();
    PUTS("dlq zawer{eniq programmy navatx [0]");
    WHILE(DIN) BEGIN
        NEWLINE();
        PUTS("~islo? ");
        WHILE(GETS(BELL,LENGTH)==0);
        DIN = GETDEC(BELL);
        IF (*VAL != 0) BEGIN
            PUTS("o{ibka");
            DIN = 1;
            CONTINUE;
        END
        PUTCHAR('=');
        PUTDEC(DIN);
    END
NEWLINE();
PUTS("konec raboty");
GETCHAR();
END

NEWLINE()
BEGIN
    PUTCHAR('\R');
    PUTCHAR('\N');
END

PUTDEC(NUM)
INT NUM;
BEGIN
    INT K, ZS;
    CHAR C;
    ZS = 0;
    K = 10000;
    IF (NUM < 0) BEGIN
        NUM = -NUM;
        PUTCHAR('-');
    END
    WHILE (K >= 1) BEGIN
        C = ABS(NUM / K) + '0';
        IF ((C != '0') ! (K == 1) ! (ZS)) BEGIN
            ZS = 1;
            PUTCHAR(C);
        END
        NUM = ABS(NUM % K);
        K = K / 10;
    END
END

ABS(NUM) 
INT NUM;
BEGIN
    IF (NUM < 0) NUM = -NUM;
    RETURN NUM;
END

PUTS(LINE) 
CHAR* LINE;
BEGIN
    INT K;
    K = 0;
    WHILE (LINE[K]) PUTCHAR(LINE[K++]);
END

GETS(LINE, NUM)
CHAR* LINE;
INT NUM;
BEGIN
    INT K;
    CHAR L;
    K = 0;
    WHILE ((L = GETCHAR()) != '\R') BEGIN
        IF ((L = 8) & (K != 0)) BEGIN
            --K;
            PUTCHAR(8);
            PUTCHAR(' ');
            PUTCHAR(8);
        END
        ELSE IF ((L < 32) ! (K >= NUM - 1)) CONTINUE;
        ELSE PUTCHAR(LINE[K++] = L);
    END
    LINE[K] = 0;
    RETURN K;
END

GETDEC(LINE)
CHAR* LINE;
BEGIN
    INT K, MINUS;
    CHAR C;
    VAL = LINE - 1;
    K = MINUS = 1;
    WHILE (K) BEGIN
        K = 0;
        SYMB();
        IF (*VAL == '+') K = 1;
        IF (*VAL == '-') BEGIN 
            K = 1;
            MINUS = -MINUS;
        END
    END
    IF ((*VAL < '0') ! (*VAL > '9')) RETURN 0;
    WHILE ((*VAL >= '0') & (*VAL <= '9')) BEGIN
        C = *VAL;
        SYMB();
        K = K *10 + (C - '0');
    END
    IF (MINUS < 0) K = -K;
    RETURN K;
END

SYMB() 
BEGIN
    WHILE (*(++VAL) == 32);
END
