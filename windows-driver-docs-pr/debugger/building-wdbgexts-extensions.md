---
title: 生成 WdbgExts 扩展
description: 生成 WdbgExts 扩展
keywords:
- '生成实用工具 ( # A0) ，生成 WdbgExts 扩展'
- WdbgExts 扩展，生成
- WdbgExts 扩展，编译
ms.date: 10/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8017363f0747a6139d931f290800f12921454b36
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817551"
---
# <a name="building-wdbgexts-extensions"></a>生成 WdbgExts 扩展


## <span id="ddk_building_wdbgexts_extensions_dbwx"></span><span id="DDK_BUILDING_WDBGEXTS_EXTENSIONS_DBWX"></span>


所有调试器扩展都应该用生成实用工具编译和生成。 "生成" 实用程序包含在 Windows 驱动程序工具包 (WDK) 和早期版本的 Windows DDK 中。

请注意以下几点：

-  WDK 具有几个不同的生成环境窗口。 安装 WDK 时，其中每个都有一个对应的快捷方式放置在 " **开始** " 菜单中。 若要生成调试器扩展，则必须使用最新的 Windows 生成环境，而不管将在哪个平台上运行扩展。

-  生成实用工具通常无法编译位于包含空格的目录路径中的代码。 你的扩展代码应位于其完整路径不包含空格的目录中。 具体 (，这意味着如果将 Windows 调试工具安装到默认位置--Program Files \\ 调试工具（适用于 windows），则将无法生成示例扩展。 ) 

**生成调试器扩展**

1. 打开最新 Windows 生成环境的窗口。  (可以选择 "免费" 版本或 "checked" 版本--它们将生成相同的结果，除非你在代码中放置了 **\# ifdef DBG** 语句。 ) 

2. 设置变量 \_ NT \_ 目标 \_ 版本以指示要在其上运行扩展的最早版本的 Windows。 \_\_ \_ 可以将 NT 目标版本设置为以下值。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">“值”</th>
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
    <td align="left"><p>Windows XP 和更高版本。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>_NT_TARGET_VERSION_WS03</p></td>
    <td align="left"><p>Windows Server 2003 及更高版本。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>_NT_TARGET_VERSION_LONGHORN</p></td>
    <td align="left"><p>Windows Vista 和更高版本。</p></td>
    </tr>
    </tbody>
    </table>

     

 如果 \_ \_ \_ 未设置 NT 目标版本，则扩展将仅在打开生成窗口 (和更高版本) 的 Windows 版本上运行。 例如，在源文件中放置以下行将生成将在 Windows 上运行的扩展：
    ```console
    _NT_TARGET_VERSION = $(_NT_TARGET_VERSION_WINXP) 
    ```

3. 设置 DBGSDK \_ inc. 路径 \_ 和 DBGSDK \_ LIB \_ 路径环境变量，分别指定指向调试器 sdk 标头和调试器 sdk 库的路径。 如果 *% 调试器%* 代表用于 Windows 安装的调试工具的根，则应按如下所述设置这些变量：

    ```console
    set DBGSDK_INC_PATH=%debuggers%\sdk\inc
    set DBGSDK_LIB_PATH=%debuggers%\sdk\lib
    ```

    如果已将这些标头和库移到其他位置，请改为指定该位置。

4. 将当前目录更改为包含扩展的目录文件或源文件的目录。

5. 运行生成实用工具：

    ```console
    build -cZMg
    ```

有关这些步骤的完整说明，以及有关如何创建目录文件和源文件的说明，请参阅 WDK 中的生成实用工具文档。

 

 





