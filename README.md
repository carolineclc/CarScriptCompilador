# CarScriptCompilador
Compilador da linguagem de programação CarScript.
BLOCK = { STATEMENT };

STATEMENT  = ("λ" | PRINT | WHILE | IF | SETGET | MATH), "\n";

WHILE = "loop", "if", BOOL_EXP, "\n", "λ", { ( STATEMENT ), "λ" }, "done";

IF = "if", BOOL_EXP, "\n", "λ", { ( STATEMENT ), "λ" }, ( "λ" | ( "else", "\n", "λ", { ( STATEMENT ), "λ" })), "done";

SETGET = (("set",SET) | ("get",GET)), "/n", "done";

SET = {"\n", LOCAL_VAL, ":", EXPRESSION}; 

GET = "get", ":",  LOCAL_VAL;

LOCAL_VAL =("OIL_LEVEL" | "WATER_LEVEL"| "VELOCITY" | "ACELERATION" | "HEADLIGHT");

MATH = MATH_NAME, "(",REL_EXP, ")";

MATH_NAME = 'sqrt' | 'sin' | 'cos' |'log' | 'exp' | 'pow';

PRINT = "console", "(", BOOL_EXP, ")";

BOOL_EXP = BOOL_TERM, { ("or"), BOOL_TERM } ;

BOOL_TERM = REL_EXP, { ("and"), REL_EXP } ;

REL_EXP = EXPRESSION, { ("==" | ">" | "<"), EXPRESSION } ;

EXPRESSION = TERM, { ("+" | "-"), TERM } ;

TERM = FACTOR, { ("*" | "/"), FACTOR } ;

FACTOR = NUMBER | IDENTIFIER | (("+" | "-" | "not"), FACTOR ) | "(", EXPRESSION, ")" | "read", "(", ")" ;

IDENTIFIER = LETTER, { LETTER | DIGIT | "_" } ;

NUMBER = DIGIT, { DIGIT } ;

LETTER = ( "a" | "..." | "z" | "A" | "..." | "Z" ) ;

DIGIT = ("1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"| "0");
