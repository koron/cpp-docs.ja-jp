---
description: '詳細情報: &lt; アクセス許可&gt;'
title: '&lt;アクセス許可> (C++ ドキュメントコメント)'
ms.date: 11/04/2016
f1_keywords:
- permission
- <permission>
helpviewer_keywords:
- <permission> C++ XML tag
- permission C++ XML tag
ms.assetid: 537ee2bc-95bd-48e4-9ce6-3420c3da87f4
ms.openlocfilehash: cd815b5df831632afd399e752e4525082f20b063
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/11/2020
ms.locfileid: "97226026"
---
# <a name="ltpermissiongt"></a>&lt;permission&gt;

\<permission> タグを使用すると、メンバーのアクセスをドキュメント化できます。 <xref:System.Security.PermissionSet> を使用すると、メンバーへのアクセスを指定できます。

## <a name="syntax"></a>構文

```
<permission cref="member">description</permission>
```

#### <a name="parameters"></a>パラメーター

*レプリカ*<br/>
現在のコンパイル環境からの呼び出しに利用できる、メンバーまたはフィールドへの参照。 コンパイラは、指定されたコード要素が存在し、出力の XML で `member` が正規要素名に変換されることを確認します。  名前は、一重引用符または二重引用符で囲みます。

コンパイラは、`member` が見つからない場合に警告を発行します。

ジェネリック型への cref 参照を作成する方法については、「」を参照してください [\<see>](see-visual-cpp.md) 。

*description*<br/>
メンバーへのアクセスの説明です。

## <a name="remarks"></a>Remarks

ドキュメントコメントをファイルに処理するために、 [/doc](doc-process-documentation-comments-c-cpp.md) を使用してコンパイルします。

MSVC コンパイラは、ドキュメントコメント内の1回のパスで cref 参照の解決を試みます。  したがって、C++ のルックアップ規則を使用する場合、コンパイラによってシンボルが見つからないと、参照が未解決としてマークされます。 詳細については、「」を参照してください [\<seealso>](seealso-visual-cpp.md) 。

## <a name="example"></a>例

```cpp
// xml_permission_tag.cpp
// compile with: /clr /doc /LD
// post-build command: xdcmake xml_permission_tag.dll
using namespace System;
/// Text for class TestClass.
public ref class TestClass {
   /// <permission cref="System::Security::PermissionSet">Everyone can access this method.</permission>
   void Test() {}
};
```

## <a name="see-also"></a>関連項目

[XML に関するドキュメント](xml-documentation-visual-cpp.md)
