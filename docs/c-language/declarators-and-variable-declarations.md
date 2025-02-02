---
description: '詳細情報: 宣言子と変数宣言'
title: 宣言子と変数宣言
ms.date: 11/04/2016
helpviewer_keywords:
- declaring variables, declarators
- declarators, definition
- declaring variables, declaration statements
ms.assetid: 5fd67a6a-3a6a-4ec9-b257-3f7390a48d40
ms.openlocfilehash: 920c44e3345c6143489815de55ea81470e46d279
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/11/2020
ms.locfileid: "97306418"
---
# <a name="declarators-and-variable-declarations"></a>宣言子と変数宣言

このセクションの残りの部分では、次の一覧に示す変数型の宣言の形式とその意味について説明します。 特に、残りの各セクションでは、以下を宣言する方法について説明します。

|変数の種類|説明|
|----------------------|-----------------|
|[単純変数](../c-language/simple-variable-declarations.md)|整数型または浮動小数点型の単一値変数|
|[配列](../c-language/array-declarations.md)|同じ型の要素のコレクションで構成される変数|
|[ポインター](../c-language/pointer-declarations.md)|他の変数をポイントし、値の代わりに変数の場所を (アドレスの形式で) 含む変数|
|[列挙変数](../c-language/c-enumeration-declarations.md)|一連の名前付き整数定数の 1 つの値を保持する整数型の単純変数|
|[構造体](../c-language/structure-declarations.md)|異なる型を持つことができる値のコレクションで構成される変数|
|[共用体](../c-language/union-declarations.md)|同じストレージ領域を占有する異なる型の複数の値で構成される変数|

宣言子は、宣言に含まれる、プログラムに組み込まれる名前を指定する部分です。 <strong>\*</strong> (ポインター) などの修飾子と Microsoft の呼び出し規約キーワードを含めることができます。

**Microsoft 固有の仕様**

次のような宣言子があります。

```C
__declspec(thread) char *var;
```

**`char`** は型指定子、`__declspec(thread)` と `*` は修飾子、`var` は識別子の名前です。

**Microsoft 固有の仕様はここまで**

宣言子は、値の配列、値へのポインター、および指定された型の値を返す関数を宣言するために使用します。 宣言子は、このセクションで後述する配列およびポインターの宣言に記述されます。

## <a name="syntax"></a>構文

*declarator*:<br/>
&nbsp;&nbsp;*pointer*<sub>opt</sub> *direct-declarator*

*direct-declarator*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*identifier*<br/>
&nbsp;&nbsp;&nbsp;&nbsp; **(**  *declarator*  **)**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*direct-declarator*  **[**  *constant-expression*<sub>opt</sub> **]**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*direct-declarator*  **(**  *parameter-type-list*  **)**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*direct-declarator*  **(**  *identifier-list*<sub>opt</sub> **)**

*pointer*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>\*</strong> *type-qualifier-list*<sub>opt</sub><br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>\*</strong> *type-qualifier-list*<sub>opt</sub> *pointer*

*type-qualifier-list*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*type-qualifier*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*type-qualifier-list type-qualifier*

> [!NOTE]
> *declarator* を参照する構文については、「[宣言の概要](../c-language/overview-of-declarations.md)」または「[C 言語の構文概要](../c-language/c-language-syntax-summary.md)」にある *declaration* の構文を参照してください。

宣言子が修飾されていない識別子で構成される場合、宣言される項目は基本型を持ちます。 アスタリスク (<strong>\*</strong>) が識別子の左側にある場合、型はポインター型に変更されます。 識別子の後ろに角かっこ ( **[ ]** ) が続く場合、型は配列型に変更されます。 識別子の後ろにかっこが続く場合、型は関数型に変更されます。 宣言内での優先順位の解釈の詳細については、「[Interpreting More Complex Declarators](../c-language/interpreting-more-complex-declarators.md)」 (より複雑な宣言子の解釈) を参照してください。

各宣言は 1 つ以上の識別子を宣言します。 宣言子で完全な宣言をするには、型指定子を含める必要があります。 型指定子は、配列型の要素の型、ポインター型によってアドレス指定されるオブジェクトの型、または関数の戻り値の型を示します。

[配列](../c-language/array-declarations.md)と[ポインター](../c-language/pointer-declarations.md)の宣言については、このセクションの後半で詳しく説明します。 次の例に、宣言子の簡単な形式をいくつか示します。

```C
int list[20]; // Declares an array of 20 int values named list
char *cp;     // Declares a pointer to a char value
double func( void ); // Declares a function named func, with no
                     // arguments, that returns a double value
int *aptr[10] // Declares an array of 10 pointers
```

**Microsoft 固有の仕様**

Microsoft C コンパイラでは、数値型、構造体型、または共用体型を変更できる宣言子の数は制限されません。 数は、使用できるメモリ容量によってのみ制限されます。

**Microsoft 固有の仕様はここまで**

## <a name="see-also"></a>関連項目

[宣言と型](../c-language/declarations-and-types.md)
