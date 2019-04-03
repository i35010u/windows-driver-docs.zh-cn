---
title: 生成 DbgEng 扩展
description: 生成 DbgEng 扩展
ms.assetid: e2cf8a01-2099-4ad7-98ac-1a20c76a2e0a
keywords:
- DbgEng 扩展构建
- 生成实用工具 (build.exe) 构建 DbgEng 扩展
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff9ee79cf61232803594e082f269360753a24d63
ms.sourcegitcommit: 1a1a78575e89bf8cd713bf1dac8a698db3cddfe2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2019
ms.locfileid: "58845529"
---
# <a name="building-dbgeng-extensions"></a>生成 DbgEng 扩展

## <span id="ddk_building_dbgeng_extensions_dbx"></span><span id="DDK_BUILDING_DBGENG_EXTENSIONS_DBX"></span>

应该编译并使用 Visual Studio 生成的所有调试器扩展。 生成实用工具不能再用于调试器扩展。

有关在 Visual Studio 中生成项目的文档，请参阅[Visual Studio 项目的 c + +](https://docs.microsoft.com/cpp/build/creating-and-managing-visual-cpp-projects?view=vs-2017)。

若要生成扩展，请使用以下过程：

**若要生成调试程序扩展**

1. 打开**dbgsdk.sln** Visual Studio 中的示例项目。

2. 检查 include 和 lib 文件的项目设置。 如果 *%调试器 %* 表示根的您的 Windows 调试工具的安装，它们应设置，如下所示：

```text
Include Path 
%debuggers%\sdk\inc
Library Path
%debuggers%\sdk\lib
```

 如果具有这些标头和库移到其他位置，请改为指定该位置。

3. 选择**构建**，然后**生成解决方案**从 Visual Studio 中的菜单。
