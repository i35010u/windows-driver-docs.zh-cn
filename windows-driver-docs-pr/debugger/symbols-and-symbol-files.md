---
title: 符号和符号文件
description: 符号和符号文件
keywords:
- 符号，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84bf1f41ea220bd10adcf87875f0d1914bd46efc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825771"
---
# <a name="symbols-and-symbol-files"></a>符号和符号文件


## <span id="ddk_symbol_files_overview_dbg"></span><span id="DDK_SYMBOL_FILES_OVERVIEW_DBG"></span>


链接应用程序、库、驱动程序或操作系统时，创建 .exe 和 .dll 文件的链接器还会创建多个称为 *符号文件* 的附加文件。

符号文件保存多个数据，这些数据在运行二进制文件时实际上并不需要，但在调试过程中可能非常有用。

通常，符号文件可能包含：

-   全局变量

-   局部变量

-   函数名称和其入口点的地址

-   帧指针省略 (FPO) 记录

-   源行号

其中每个项分别称为一个 *符号*。 例如，单个符号文件 Myprogram.exe 可能包含几百个符号，包括全局变量和函数名以及数百个局部变量。 通常，软件公司会发布每个符号文件的两个版本：包含 *公共符号* 和 *私有符号* 的完整符号文件，以及减少的 (去除只包含公共符号) 文件。 有关详细信息，请参阅 [公共和私有符号](public-and-private-symbols.md)。

调试时，必须确保调试器能够访问与正在调试的目标关联的符号文件。 实时调试和调试崩溃转储文件都需要符号。 你必须获取要调试的代码的正确符号，并将这些符号加载到调试器中。

### <a name="span-idwindows_symbolsspanspan-idwindows_symbolsspanwindows-symbols"></a><span id="windows_symbols"></span><span id="WINDOWS_SYMBOLS"></span>Windows 符号

Windows 在扩展名为 .pdb 的文件中保留其符号。

编译器和链接器控制符号格式。 Visual C++ 链接器会将所有符号置于 .pdb 文件中。

Windows 操作系统内置于两个版本中。 *免费生成* (或 *零售版本*) 具有相对较小的二进制文件，并且已 *检查的生成* (或 *调试版本*) 具有更大的二进制文件，代码本身中的调试符号更多。 在 Windows 10 版本1803之前，已检查的生成在 windows 的早期版本上可用。 其中每个生成都有自己的符号文件。 在 Windows 上调试目标时，必须使用与目标上的 Windows 生成匹配的符号文件。

下表列出了标准 Windows 符号树中存在的几个目录：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Directory</th>
<th align="left">包含的符号文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ACM</p></td>
<td align="left"><p>Microsoft 音频压缩管理器文件</p></td>
</tr>
<tr class="even">
<td align="left"><p>COM</p></td>
<td align="left"><p>可执行文件 ( .com) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>CPL</p></td>
<td align="left"><p>控制面板程序</p></td>
</tr>
<tr class="even">
<td align="left"><p>DLL</p></td>
<td align="left"><p>动态链接库文件 ( .dll) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>WINSPOOL.DRV</p></td>
<td align="left"><p> ( 的驱动程序文件。 winspool.drv) </p></td>
</tr>
<tr class="even">
<td align="left"><p>EXE</p></td>
<td align="left"><p>可执行文件 ( .exe) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>SCR</p></td>
<td align="left"><p>屏幕保护程序文件</p></td>
</tr>
<tr class="even">
<td align="left"><p>SYS</p></td>
<td align="left"><p>驱动程序文件 ( .sys) </p></td>
</tr>
</tbody>
</table>

 

 

 





