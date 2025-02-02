---
description: '詳細情報: 方法:ターゲット フレームワークおよびプラットフォームのツールセットを変更する'
title: '方法: ターゲット フレームワークおよびプラットフォームのツールセットを変更する'
ms.custom: conceptual
ms.date: 07/24/2019
helpviewer_keywords:
- 'msbuild (c++), howto: modify target framework and platform toolset'
ms.assetid: 031b1d54-e6e1-4da7-9868-3e75a87d9ffe
ms.openlocfilehash: 8b3de299652efcdd8fd94622b890b6cec7b059e8
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/11/2020
ms.locfileid: "97156256"
---
# <a name="how-to-modify-the-target-framework-and-platform-toolset"></a>方法: ターゲット フレームワークおよびプラットフォームのツールセットを変更する

Visual Studio C++ プロジェクト ファイルを編集して、別のバージョンの C++ プラットフォーム ツールセット、Windows SDK、および .NET Framework (C++/CLI プロジェクトのみ) をターゲットにすることができます。 既定では、プロジェクト システムは、プロジェクトの作成に使用する Visual Studio のバージョンに対応する .NET Framework のバージョンおよびツールセットのバージョンを使用します。 .vcxproj ファイルでこれらのすべての値を変更して、すべてのコンパイル ターゲットで同じコード ベースを使用できるようにすることができます。

## <a name="platform-toolset"></a>プラットフォームのツールセット

プラットフォームのツールセットは、C++ コンパイラ (cl.exe) とリンカー (link.exe)、そして C/C++ 標準ライブラリで構成されます。 Visual Studio 2015 以降、ツールセットのメジャー バージョンは 14 のままです。つまり、Visual Studio 2019 または Visual Studio 2017 でコンパイルされたプロジェクトは、Visual Studio 2015 でコンパイルされたプロジェクトとの ABI 下位互換性があります。 マイナー バージョンは、Visual Studio 2015 以降、バージョンごとに 1 ずつ更新されています。

- Visual Studio 2015: v140
- Visual Studio 2017: v141
- Visual Studio 2019: v142

これらのツールセットでは、.NET Framework 4.5 以降がサポートされています。

Visual Studio では、C++ プロジェクトの複数バージョン対応もサポートされています。 Visual Studio IDE を使用して、以前のバージョンの Visual Studio で作成されたプロジェクトを編集およびビルドできます。新しいバージョンのツールセットを使用するようにアップグレードする必要はありません。 コンピューターに以前のツールセットがインストールされている必要があります。 詳細については、[Visual Studio でネイティブの複数バージョン対応を使用する方法](../porting/use-native-multi-targeting.md)に関する記事を参照してください。 たとえば、Visual Studio 2015 では、.NET Framework 2.0 を *ターゲット* にできますが、それをサポートする以前のツールセットを使用する必要があります。

## <a name="target-framework-ccli-project-only"></a>ターゲット フレームワーク (C++/CLI プロジェクトのみ)

ターゲット フレームワークを変更すると、プラットフォーム ツールセットのバージョンもそのターゲット フレームワークをサポートするように変更されます。 たとえば、.NET Framework 4.5 を対象とする場合、Visual Studio 2015 (v140)、Visual Studio 2013 (v120)、Visual Studio 2012 (v110) のような互換性のあるプラットフォーム ツールセットを使用する必要があります。 [Windows 7.1 SDK](https://www.microsoft.com/download/details.aspx?id=8279) プラットフォーム ツールセットを使用すると、.NET Framework 2.0、3.0、3.5、4、および x86/x64 プラットフォームをターゲットにすることができます。

カスタム プラットフォーム ツールセットを作成することで、さらにターゲット フレームワークを拡張できます。 詳細については、Visual C++ チーム ブログの [C++ Native Multi-Targeting (C++ ネイティブ マルチ ターゲット)](https://devblogs.microsoft.com/cppblog/c-native-multi-targeting/) をご覧ください。

### <a name="to-change-the-target-framework"></a>ターゲット フレームワークを変更するには

1. Visual Studio の **ソリューション エクスプローラー** で、プロジェクトを選びます。 メニュー バーで **[プロジェクト]** メニューを開き、 **[プロジェクトのアンロード]** を選択します。 これによって、プロジェクトのプロジェクト (.vcxproj) ファイルをアンロードします。

   > [!NOTE]
   >  Visual Studio ではプロジェクト ファイルの変更中には、C ++ プロジェクトを読み込むことはできません。 ただし、プロジェクトが Visual Studio に読み込まれるとき、メモ帳などの別のエディターを使用して、プロジェクト ファイルを変更することができます。 Visual Studio はプロジェクト ファイルが変更されたことを検知して、プロジェクトを再度読み込むように求めるメッセージが表示されます。

1. メニュー バーで、 **[ファイル]** 、 **[開く]** 、 **[ファイル]** の順に選択します。 **[ファイルを開く]** のダイアログ ボックスで、プロジェクトのフォルダーに移動し、プロジェクト (.vcxproj) ファイルを開きます。

1. プロジェクト ファイルで、ターゲット フレームワークのバージョンに対するエントリを見つけます。 たとえば、.NET Framework 4.5 を使用するプロジェクトの場合は、 `<TargetFrameworkVersion>v4.5</TargetFrameworkVersion>` 要素の `<PropertyGroup Label="Globals">` 要素の中の `<Project>` を探します。 `<TargetFrameworkVersion>` 要素が存在しない場合には、プロジェクトは .NET Framework を使用しないため、変更の必要はありません。

1. その値を、使用するフレームワークのバージョン (v3.5 または v4.6 など) に更新します。

1. 変更を保存してエディターを閉じます。

1. **ソリューション エクスプローラー** で、プロジェクトのショートカット メニューを開き、 **[プロジェクトの再読み込み]** をクリックします。

1. 変更内容を確認するには、 **ソリューション エクスプローラー** で、右クリックして (ソリューションではなく) プロジェクトのショートカット メニューを開き、 **[プロパティ]** を選択してプロジェクトの **[プロパティ ページ]** ダイアログ ボックスを開きます。 ダイアログ ボックスの左ペインで、 **[構成プロパティ]** を展開し、 **[全般]** を選択します。 **.NET Target 対象バージョン** が新しいバージョンのフレームワークを示していることを確認します。

### <a name="to-change-the-platform-toolset"></a>プラットフォームのツールセットを変更するには

1. Visual Studio の **ソリューション エクスプローラー** で、(ソリューションではなく) プロジェクトのショートカット メニューを開き、 **[プロパティ]** を選択してプロジェクトの **[プロパティ ページ]** ダイアログ ボックスを開きます。

1. **[プロパティ ページ]** ダイアログ ボックスで、 **[構成]** ドロップダウン リストを開き、 **[すべての構成]** を選択します。

1. ダイアログ ボックスの左ペインで、 **[構成プロパティ]** を展開し、 **[全般]** を選択します。

1. 右ペインで、 **[プラットフォーム ツールセット]** をクリックして、ドロップダウン リストから使用するツールセットを選択します。 たとえば、Visual Studio 2010 ツール セットをインストールした場合は、 **[Visual Studio 2010 (v100)]** を選択してプロジェクト用に使います。

1. **[OK]** を選択します。

## <a name="see-also"></a>関連項目

[コマンド ラインでの MSBuild - C++](msbuild-visual-cpp.md)
