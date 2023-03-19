# Antlr

Official website: <https://www.antlr.org/>

ANTLR (ANother Tool for Language Recognition) is a powerful parser generator for reading, processing, executing, or translating structured text or binary files. It's widely used to build languages, tools, and frameworks. From a grammar, ANTLR generates a parser that can build and walk parse trees

## DownLoad

- DownLoad Guide
    [download guide](https://www.antlr.org/download.html)

## Example

example.g4
```antlr
// specific grammar name
grammar example;
// for non-terminal, star with lower-case letter

//'*' represents 0 or more occurrences of the production
//'+' represents at least one occurrence
//The following example will be parsed as vector<number>
addExp
    : number ('+' number)*
    ;

//You can use # nickname after the production
//Create an alias to analyze the production of different situations with the same name
number
    : IntLiteral # number1
    | FloatLiteral # number2
    ;

// for terminal, star with lower-case letter
IntLiteral
    : [0-9]+
    | ('0x'|'0X')[0-9a-fA-F]+
    ;

// '?' Indicates that the production may exist, if it exists, it only occurs once
FloatLiteral
    : ([0-9]+|[0-9]*'.'[0-9]*)([eE]('+'|'-')?[0-9]+)?[fFlL]?
    | ('0x'|'0X')([0-9a-fA-F]*'.'[0-9a-fA-F]*)([pP]('+'|'-')?[0-9]+)?[fFlL]?
    ;
```

shell command
``` sh
antlr -Dlanguage=Cpp -no-listener -visitor example.g4
```

exampleVisitor.h
``` cpp
#include "exampleBaseVisitor.h"

class ExampleVisitor : public exampleBaseVisitor {
    virtual antlrcpp::Any visitAddExp(exampleParser::AddExpContext *ctx) override;
    virtual antlrcpp::Any visitNumber(exampleParser::NumberContext *ctx) override;
};
// Access string of current node by `ctx->getText()`
// Visit `number` node of `addExp` by `ctx->number()`
// then you can override visit-function to build your own parser !
```

## Reference

- Antlr Repository
    [antlr repository](https://github.com/antlr)

- Antlr Document
    [antlr official doc](https://github.com/antlr/antlr4/blob/master/doc/index.md)