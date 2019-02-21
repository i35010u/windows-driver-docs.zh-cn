---
title: 打印机 Dirids
description: 打印机 Dirids
ms.assetid: 104af180-c739-4733-b21b-448cfe15ab71
keywords:
- INF 文件 WDK 打印，dirids
- dirids WDK
- 目录标识符 WDK 打印机
- 打印机 dirids WDK
- 标识符 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9f577dbc0ee727a9a379b129f8252d6d2c64d55
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544439"
---
# <a name="printer-dirids"></a>打印机 Dirids





指定目标目录 INF 文件、 目录标识符时 (`dirids`) 应使用。 有关详细信息，请参阅[使用 Dirids](https://msdn.microsoft.com/library/windows/hardware/ff553598)。

下表列出了特定于打印机的`dirids`和每个用途。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Dirid</th>
<th>用途</th>
<th>目录内容</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>66000</p></td>
<td><p>表示返回的目录路径<a href="https://go.microsoft.com/fwlink/p/?linkid=124454" data-raw-source="[GetPrinterDriverDirectory](https://go.microsoft.com/fwlink/p/?linkid=124454)">GetPrinterDriverDirectory</a>函数。</p></td>
<td><p>驱动程序文件和<a href="printer-inf-file-entries.md#ddk-dependent-files-gg" data-raw-source="[dependent files](printer-inf-file-entries.md#ddk-dependent-files-gg)">依赖文件</a>。</p></td>
</tr>
<tr class="even">
<td><p>66001</p></td>
<td><p>表示返回的目录路径<a href="https://go.microsoft.com/fwlink/p/?linkid=124455" data-raw-source="[GetPrintProcessorDirectory](https://go.microsoft.com/fwlink/p/?linkid=124455)">GetPrintProcessorDirectory</a>函数。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556325#wdkgloss-print-processor" data-raw-source="&lt;em&gt;Print processor&lt;/em&gt;"><em>打印处理器</em></a>文件。</p></td>
</tr>
<tr class="odd">
<td><p>66002</p></td>
<td><p>表示要复制到本地系统 \System32 的其他文件的目录路径。 请参阅此表后面的段落。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556325#wdkgloss-print-monitor" data-raw-source="&lt;em&gt;Print monitor&lt;/em&gt;"><em>打印监控器</em></a>文件。</p></td>
</tr>
<tr class="even">
<td><p>66003</p></td>
<td><p>表示返回的目录路径<a href="https://go.microsoft.com/fwlink/p/?linkid=124456" data-raw-source="[GetColorDirectory](https://go.microsoft.com/fwlink/p/?linkid=124456)">GetColorDirectory</a>函数。</p></td>
<td><p>ICM 颜色配置文件中。</p></td>
</tr>
<tr class="odd">
<td><p>66004</p></td>
<td><p>表示打印机特定于类型的 ASP 文件复制到的目录路径。</p></td>
<td><p>ASP 文件和关联的文件。</p></td>
</tr>
</tbody>
</table>

 

分配给目录中的文件`dirid`66002 都复制到 System32 子目录时的本机体系结构的打印机驱动程序正在安装在本地系统上，例如在 x86 本地安装驱动程序的 x86 系统。 如果驱动程序已安装到远程系统，将忽略此目录中的文件。

当打印机类安装程序调用后台处理程序的安装打印机驱动程序[AddPrinterDriverEx](https://go.microsoft.com/fwlink/p/?linkid=124457)函数。 此函数需要位于返回的目录中的所有驱动程序文件**GetPrinterDriverDirectory**函数。

 

 




