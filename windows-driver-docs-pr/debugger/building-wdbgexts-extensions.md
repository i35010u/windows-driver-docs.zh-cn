---
title: 构建 WdbgExts 扩展
description: 构建 WdbgExts 扩展
ms.assetid: a3923de6-bed5-40e0-a9cb-99e0f4354448
keywords:
- 生成实用工具 (build.exe) 构建 WdbgExts 扩展
- WdbgExts 扩展构建
- WdbgExts 扩展编译
ms.date: 10/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: d76e961f07cb4cedab340efcfd8b0f82d96c3527
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522397"
---
# <a name="building-wdbgexts-extensions"></a>构建 WdbgExts 扩展


## <span id="ddk_building_wdbgexts_extensions_dbwx"></span><span id="DDK_BUILDING_WDBGEXTS_EXTENSIONS_DBWX"></span>


所有调试器扩展应编译并被内置生成实用程序。 Windows Driver Kit (WDK) 中和在早期版本的 Windows DDK 中包含生成实用工具。

请注意以下几点：

-  WDK 具有多个不同的生成环境窗口。 每个已放入相应的快捷方式**启动**菜单安装 WDK 时。 若要生成调试器扩展，必须使用最新的 Windows 生成环境，而不考虑你将在运行该扩展哪些平台。

-  生成实用程序通常是不能位于包含空格的目录路径中的代码编译的。 扩展插件代码应位于其完整路径包含空格的目录。 (具体而言，这意味着，如果在默认位置-程序文件安装的 Windows 调试工具\\有关 Windows 调试工具-您将无法再生成的示例扩展插件。)

**若要生成调试程序扩展**

1. 打开最新的 Windows 生成环境窗口。 (您可以选择"免费"版本或"选中"版本-它们将产生相同的结果，除非已将 **\#ifdef DBG**在代码中的语句。)

2. 设置变量\_NT\_目标\_版本，以指示你想要运行该扩展的 Windows 的最早版本。 \_NT\_目标\_版本可以设置为以下值。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">值</th>
    <th align="left">Windows 版本</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>_NT_TARGET_VERSION_WIN2K</p></td>
    <td align="left"><p>Windows 2000 及更高版本。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>_NT_TARGET_VERSION_WINXP</p></td>
    <td align="left"><p>Windows XP 及更高版本。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>_NT_TARGET_VERSION_WS03</p></td>
    <td align="left"><p>Windows Server 2003 及更高版本。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>_NT_TARGET_VERSION_LONGHORN</p></td>
    <td align="left"><p>Windows Vista 及更高版本。</p></td>
    </tr>
    </tbody>
    </table>

     

 如果\_NT\_目标\_版本未设置，仅为 Windows 版本上运行该扩展，将生成窗口已打开 （和更高版本）。 例如，将以下行放在源文件将生成将在 Windows 运行的扩展：
    ```console
    _NT_TARGET_VERSION = $(_NT_TARGET_VERSION_WINXP) 
    ```

3. 设置 DBGSDK\_INC\_路径和 DBGSDK\_LIB\_路径环境变量，以分别指定调试程序 SDK 标头和调试器 SDK 库的路径。 如果 *%调试器 %* 表示根的您的 Windows 调试工具的安装，这些变量应设置，如下所示：

    ```console
    set DBGSDK_INC_PATH=%debuggers%\sdk\inc
    set DBGSDK_LIB_PATH=%debuggers%\sdk\lib
    ```

    如果具有这些标头和库移到其他位置，请改为指定该位置。

4. 将当前目录更改为包含扩展的目录文件或源文件的目录。

5. 运行生成实用程序：

    ```console
    build -cZMg
    ```

有关这些步骤的完整说明和有关如何创建目录文件和源文件的说明，请参阅 WDK 中的生成实用程序文档。

 

 





