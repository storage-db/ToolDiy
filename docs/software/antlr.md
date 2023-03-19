# Antlr

官网：<https://www.antlr.org/>

ANTLR(ANother-Tool-for-Language-Recognition)是一个功能强大的语法分析器生成器，用于读取、处理、执行或翻译结构化文本或二进制文件。它被广泛用于构建语言、工具和框架。ANTLR根据语法生成一个解析器，该解析器可以构建和遍历解析树

## 安装

- 官方指导
    [download guide](https://www.antlr.org/download.html)

## Example

example.g4
```antlr
// specific grammar name
grammar example;
// for non-terminal, star with lower-case letter

// '*' 代表该产生式出现0次或以上
// '+' 代表至少出现一次
// 下例将会被解析成vector<number>
addExp
    : number ('+' number)*
    ;

// 可以通过在产生式后 # nickname
// 创建一个别名用来分析同名的不同情况下的产生式
number
    : IntLiteral # number1
    | FloatLiteral # number2
    ;

// for terminal, star with lower-case letter
IntLiteral
    : [0-9]+
    | ('0x'|'0X')[0-9a-fA-F]+
    ;

// '?' 代表该产生式可能存在，若存在仅出现一次
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

## 参考

- 官方仓库
    [antlr repository](https://github.com/antlr)

- 官方文档
    [antlr official doc](https://github.com/antlr/antlr4/blob/master/doc/index.md)
