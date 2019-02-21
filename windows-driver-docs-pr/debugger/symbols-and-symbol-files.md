---
title: 符号和符号文件
description: 符号和符号文件
ms.assetid: b9ace4f0-8363-4dec-806f-798d30983dc1
keywords:
- 符号概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b3f616d83929319c21da3036f2633b346e79ac6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547405"
---
# <a name="symbols-and-symbol-files"></a>符号和符号文件


## <span id="ddk_symbol_files_overview_dbg"></span><span id="DDK_SYMBOL_FILES_OVERVIEW_DBG"></span>


链接器创建.exe 和.dll 文件的链接的应用程序、 库、 驱动程序或操作系统，还会创建一个名为其他文件数*符号文件*。

符号文件包含的各种数据的实际并不需要时运行的二进制文件，但这可能在调试过程中非常有用。

通常情况下，可能包含符号文件：

-   全局变量

-   本地变量

-   函数名称和其入口点的地址

-   帧指针省略 (FPO) 记录

-   源行号

这些项的每个调用时，分别*符号*。 例如，单个符号文件 Myprogram.pdb 可能包含多个几百个符号，包括全局变量和函数名称和数百个本地变量。 通常情况下，软件公司发布的每个符号文件的两个版本： 完整符号文件同时包含这两者*公共符号*并*私有符号*，和减少 （去除） 文件包含唯一公共符号。 有关详细信息，请参阅[公共和私有符号](public-and-private-symbols.md)。

在调试时，必须确保调试器可以访问与正在调试的目标相关联的符号文件。 实时调试和故障转储文件调试需要符号。 必须获取你想要调试的代码的正确符号，并将这些符号加载到调试器。

### <a name="span-idwindowssymbolsspanspan-idwindowssymbolsspanwindows-symbols"></a><span id="windows_symbols"></span><span id="WINDOWS_SYMBOLS"></span>Windows 符号

Windows 具有扩展名为.pdb 的文件中保留其符号。

编译器和链接器控制符号格式。 Visual c + + 链接器，将所有符号都放入.pdb 文件。

Windows 操作系统是内置的两个版本。 *免费生成*(或*零售生成*) 具有相对较小的二进制文件，并*已检验版本*(或*调试版本*) 具有更大的二进制文件与代码本身中更多的调试符号。 这些生成的每个有其自己的符号文件。 在调试时在 Windows 上的目标，必须使用与匹配的目标上的 Windows 生成的符号文件。

下表列出了几种标准的 Windows 符号树中存在的目录：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Directory</th>
<th align="left">包含符号文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ACM</p></td>
<td align="left"><p>Microsoft 音频压缩管理器文件</p></td>
</tr>
<tr class="even">
<td align="left"><p>COM</p></td>
<td align="left"><p>可执行文件 (.com)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CPL</p></td>
<td align="left"><p>控件面板程序</p></td>
</tr>
<tr class="even">
<td align="left"><p>DLL</p></td>
<td align="left"><p>动态链接库文件 (.dll)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DRV</p></td>
<td align="left"><p>驱动程序文件 (.drv)</p></td>
</tr>
<tr class="even">
<td align="left"><p>EXE</p></td>
<td align="left"><p>可执行文件 (.exe)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SCR</p></td>
<td align="left"><p>屏幕保护程序文件</p></td>
</tr>
<tr class="even">
<td align="left"><p>SYS</p></td>
<td align="left"><p>驱动程序文件 (.sys)</p></td>
</tr>
</tbody>
</table>

 

 

 





