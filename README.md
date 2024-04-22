# CarScriptCompilador
### Compilador da linguagem de programação CarScript.
## Introdução 
A linguagem CarScript serve para faculitar a programação de dispositivos smart dentro de carros que calculam e fazem o display de funcionalidades e status de carros atuais, incluindo a velocidade do carro atual, nivel de agua e oleo e muitos outros. Essa linguagem tem uma semantica muito intuitiva e facil de programar.

## EBNF

```

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

```

## EXEMPLOS
### Exemplo 1: Adicionando e Mudando valores em variaveis reservadas:
Neste exemplo demonstra como usar a linguagem para adicionar ou mudar o valor de variaveis reservadas especiais para o display de status do carro.
```
set
   OIL_LEVEL : OIL_LEVEL + 1
   WATER_LEVEL : WATER_LEVEL + 5
done

get
   oil_variable = OIL_LEVEL
done

console (oil_variable)
```
### Exemplo 2: Fazendo loops
Este exemplo demonstra a funcionalidade de loops. E possivel que o codigo precise estar contido em um loop constante para que os valores estejam constantemente sendo atualizados
```
x = 0
loop 1
  set
    WATER_LEVEL : WATER_LEVEL + x
    OIL_LEVEL   : 3
  done
  x = x  +  1
  if x > 10
    console (WATER_LEVEL)
  else
    consoke (OIL_LEVEL)
  done
done

```
