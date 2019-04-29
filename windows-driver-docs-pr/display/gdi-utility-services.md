---
title: GDI 实用工具服务
description: GDI 实用工具服务
ms.assetid: 4ceec90d-5be2-4b79-87b3-1fdb6b0aea6b
keywords:
- GDI WDK Windows 2000 显示，实用程序服务
- 图形驱动程序 WDK Windows 2000 显示，实用程序服务
- 绘制 WDK GDI，实用程序服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a27e105c9544f9692427e654c7b2ddd73e53507c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374611"
---
# <a name="gdi-utility-services"></a>GDI 实用工具服务


## <span id="ddk_gdi_utility_services_gg"></span><span id="DDK_GDI_UTILITY_SERVICES_GG"></span>


下表列出了其他 GDI 实用程序服务。 这些服务包括调试支持、 获取和设置的最后一个错误，多个转换服务从一个字符编码到另一个类型、 排序例程和其他人该转换。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564187" data-raw-source="[&lt;strong&gt;EngBugCheckEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564187)"><strong>EngBugCheckEx</strong></a></p></td>
<td align="left"><p>关闭系统以可控方式时带来调用方发现发生了不可恢复的不一致。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564773" data-raw-source="[&lt;strong&gt;EngDebugBreak&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564773)"><strong>EngDebugBreak</strong></a></p></td>
<td align="left"><p>发生在当前进程中导致一个断点。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564779" data-raw-source="[&lt;strong&gt;EngDebugPrint&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564779)"><strong>EngDebugPrint</strong></a></p></td>
<td align="left"><p>打印到内核调试程序指定的调试消息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564940" data-raw-source="[&lt;strong&gt;EngGetLastError&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564940)"><strong>EngGetLastError</strong></a></p></td>
<td align="left"><p>返回由 GDI 记录调用线程的最后一个错误代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564958" data-raw-source="[&lt;strong&gt;EngHangNotification&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564958)"><strong>EngHangNotification</strong></a></p></td>
<td align="left"><p>通知系统指定的设备是不可操作或无响应。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564969" data-raw-source="[&lt;strong&gt;EngLpkInstalled&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564969)"><strong>EngLpkInstalled</strong></a></p></td>
<td align="left"><p>确定是否在系统上安装此语言包。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564978" data-raw-source="[&lt;strong&gt;EngMulDiv&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564978)"><strong>EngMulDiv</strong></a></p></td>
<td align="left"><p>将两个 32 位值相乘，然后除以第三个 32 位值的 64 位结果。 向上或向下最接近的整数，舍入的返回值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564979" data-raw-source="[&lt;strong&gt;EngMultiByteToUnicodeN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564979)"><strong>EngMultiByteToUnicodeN</strong></a></p></td>
<td align="left"><p>将使用当前 ANSI 代码页的 Unicode 字符串转换为指定的 ANSI 源字符串。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564980" data-raw-source="[&lt;strong&gt;EngMultiByteToWideChar&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564980)"><strong>EngMultiByteToWideChar</strong></a></p></td>
<td align="left"><p>将使用指定的代码页的宽字符字符串转换为 ANSI 源字符串。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564983" data-raw-source="[&lt;strong&gt;EngProbeForRead&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564983)"><strong>EngProbeForRead</strong></a></p></td>
<td align="left"><p>探测用于读取的辅助功能的结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564984" data-raw-source="[&lt;strong&gt;EngProbeForReadAndWrite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564984)"><strong>EngProbeForReadAndWrite</strong></a></p></td>
<td align="left"><p>探测的结构的读取和写入可访问性。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565015" data-raw-source="[&lt;strong&gt;EngSetLastError&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565015)"><strong>EngSetLastError</strong></a></p></td>
<td align="left"><p>使 GDI 来报告错误代码，可以通过应用程序来检索。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565022" data-raw-source="[&lt;strong&gt;EngSort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565022)"><strong>EngSort</strong></a></p></td>
<td align="left"><p>指定列表上执行快速排序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565038" data-raw-source="[&lt;strong&gt;EngUnicodeToMultiByteN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565038)"><strong>EngUnicodeToMultiByteN</strong></a></p></td>
<td align="left"><p>将使用当前 ANSI 代码页的 ANSI 字符串转换为指定的 Unicode 字符串。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565466" data-raw-source="[&lt;strong&gt;EngWideCharToMultiByte&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565466)"><strong>EngWideCharToMultiByte</strong></a></p></td>
<td align="left"><p>将宽字符字符串转换为 ANSI 的源字符串使用指定的代码页。</p></td>
</tr>
</tbody>
</table>

 

 

 





