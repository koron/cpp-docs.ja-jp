---
description: '詳細情報: message プラグマ'
title: message プラグマ
ms.date: 08/29/2019
f1_keywords:
- message_CPP
- vc-pragma.message
helpviewer_keywords:
- message pragma
- pragmas, message
ms.assetid: 67414f25-ed47-4079-a5dc-21d9d1a39754
ms.openlocfilehash: 82b8efa7e232c24402b7fb1cce0fd1e38ff8be29
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/11/2020
ms.locfileid: "97333385"
---
# <a name="message-pragma"></a>message プラグマ

コンパイルを終了せずに、標準出力に文字列リテラルを送信します。

## <a name="syntax"></a>構文

> **#pragma message (** *メッセージ文字列* **)**

## <a name="remarks"></a>解説

通常、 **`messsage`** プラグマは、コンパイル時に情報メッセージを表示するために使用されます。

*メッセージ文字列* パラメーターには、文字列リテラルに展開されるマクロを使用できます。また、このようなマクロは、任意の組み合わせで文字列リテラルと連結できます。

**`message`** プラグマで定義済みのマクロを使用する場合、マクロは文字列を返す必要があります。 それ以外の場合は、マクロの出力を文字列に変換する必要があります。

次のコード片では、 **`message`** プラグマを使用して、コンパイル中にメッセージを表示します。

```cpp
// pragma_directives_message1.cpp
// compile with: /LD
#if _M_IX86 >= 500
#pragma message("_M_IX86 >= 500")
#endif

#pragma message("")

#pragma message( "Compiling " __FILE__ )
#pragma message( "Last modified on " __TIMESTAMP__ )

#pragma message("")

// with line number
#define STRING2(x) #x
#define STRING(x) STRING2(x)

#pragma message (__FILE__ "[" STRING(__LINE__) "]: test")

#pragma message("")
```

## <a name="see-also"></a>関連項目

[プラグマ ディレクティブと __pragma キーワード](../preprocessor/pragma-directives-and-the-pragma-keyword.md)
