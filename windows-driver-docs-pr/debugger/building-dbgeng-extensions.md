---
title: 生成 DbgEng 扩展
description: 生成 DbgEng 扩展
ms.assetid: e2cf8a01-2099-4ad7-98ac-1a20c76a2e0a
keywords:
- DbgEng 扩展，生成
- '生成实用工具 ( # A0) ，生成 DbgEng 扩展'
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e8b318c496c6d3521ee61b275b932481b72312e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206121"
---
# <a name="building-dbgeng-extensions"></a>生成 DbgEng 扩展

## <span id="ddk_building_dbgeng_extensions_dbx"></span><span id="DDK_BUILDING_DBGENG_EXTENSIONS_DBX"></span>

所有调试器扩展都应该使用 Visual Studio 编译和生成。 生成实用工具不再用于调试器扩展。

有关在 Visual Studio 中生成项目的文档，请参阅 [Visual studio 项目-c + +](/cpp/build/creating-and-managing-visual-cpp-projects?view=vs-2017)。

若要生成扩展，请使用以下过程：

**生成调试器扩展**

1. 在 Visual Studio 中打开 **dbgsdk** 示例项目。

2. 检查包含文件和 lib 文件的项目设置。 如果 *% 调试器%* 代表用于 Windows 安装的调试工具的根，则应按如下所示进行设置：

```text
Include Path 
%debuggers%\sdk\inc
Library Path
%debuggers%\sdk\lib
```

 如果已将这些标头和库移到其他位置，请改为指定该位置。

3. 从 Visual Studio 菜单中选择 " **生成** "，然后选择 " **生成解决方案** "。