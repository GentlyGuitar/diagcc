diagcc: y.tab.c lex.yy.c util.c
	gcc -w -std=c99 -o diagcc y.tab.c lex.yy.c util.c -lfl

y.tab.c: diagcc.y
	yacc -d -Wno-error diagcc.y

lex.yy.c: diagcc.l
	flex -w diagcc.l



	
