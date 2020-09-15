---
title: GDI 实用工具服务
description: GDI 实用工具服务
ms.assetid: 4ceec90d-5be2-4b79-87b3-1fdb6b0aea6b
keywords:
- GDI WDK Windows 2000 显示，实用工具服务
- 图形驱动程序 WDK Windows 2000 显示，实用工具服务
- 绘制 WDK GDI，实用工具服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 378dd11f41bb9dd14560308eb23858b67c83cee5
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106868"
---
# <a name="gdi-utility-services"></a>GDI 实用工具服务


## <span id="ddk_gdi_utility_services_gg"></span><span id="DDK_GDI_UTILITY_SERVICES_GG"></span>


下表列出了其他 GDI 实用工具服务。 这些服务包括调试支持、获取和设置上一个错误、多个从一种字符编码类型转换为另一种字符编码类型的转换服务、排序例程等。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engbugcheckex" data-raw-source="[&lt;strong&gt;EngBugCheckEx&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engbugcheckex)"><strong>EngBugCheckEx</strong></a></p></td>
<td align="left"><p>当调用方发现不可恢复的不一致时，以控制的方式关闭系统。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engdebugbreak" data-raw-source="[&lt;strong&gt;EngDebugBreak&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engdebugbreak)"><strong>EngDebugBreak</strong></a></p></td>
<td align="left"><p>导致在当前进程中发生断点。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engdebugprint" data-raw-source="[&lt;strong&gt;EngDebugPrint&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engdebugprint)"><strong>EngDebugPrint</strong></a></p></td>
<td align="left"><p>向内核调试器打印指定的调试消息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-enggetlasterror" data-raw-source="[&lt;strong&gt;EngGetLastError&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-enggetlasterror)"><strong>EngGetLastError</strong></a></p></td>
<td align="left"><p>返回 GDI 针对调用线程记录的最后一个错误代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-enghangnotification" data-raw-source="[&lt;strong&gt;EngHangNotification&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-enghangnotification)"><strong>EngHangNotification</strong></a></p></td>
<td align="left"><p>通知系统指定的设备不可操作或无响应。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-englpkinstalled" data-raw-source="[&lt;strong&gt;EngLpkInstalled&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-englpkinstalled)"><strong>EngLpkInstalled</strong></a></p></td>
<td align="left"><p>确定系统上是否已安装语言包。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engmuldiv" data-raw-source="[&lt;strong&gt;EngMulDiv&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engmuldiv)"><strong>EngMulDiv</strong></a></p></td>
<td align="left"><p>将 2 32 位值相乘，然后将64位的结果除以第三个32位值。 返回值向上或向下舍入到最接近的整数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engmultibytetounicoden" data-raw-source="[&lt;strong&gt;EngMultiByteToUnicodeN&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engmultibytetounicoden)"><strong>EngMultiByteToUnicodeN</strong></a></p></td>
<td align="left"><p>使用当前 ANSI 代码页将指定的 ANSI 源字符串转换为 Unicode 字符串。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engmultibytetowidechar" data-raw-source="[&lt;strong&gt;EngMultiByteToWideChar&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engmultibytetowidechar)"><strong>EngMultiByteToWideChar</strong></a></p></td>
<td align="left"><p>使用指定的代码页将 ANSI 源字符串转换为宽字符字符串。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engprobeforread" data-raw-source="[&lt;strong&gt;EngProbeForRead&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engprobeforread)"><strong>EngProbeForRead</strong></a></p></td>
<td align="left"><p>探测用于读取可访问性的结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engprobeforreadandwrite" data-raw-source="[&lt;strong&gt;EngProbeForReadAndWrite&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engprobeforreadandwrite)"><strong>EngProbeForReadAndWrite</strong></a></p></td>
<td align="left"><p>探测用于读取和写入可访问性的结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engsetlasterror" data-raw-source="[&lt;strong&gt;EngSetLastError&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engsetlasterror)"><strong>EngSetLastError</strong></a></p></td>
<td align="left"><p>导致 GDI 报告错误代码，该代码可由应用程序检索。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engsort" data-raw-source="[&lt;strong&gt;EngSort&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engsort)"><strong>EngSort</strong></a></p></td>
<td align="left"><p>对指定列表执行快速排序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engunicodetomultibyten" data-raw-source="[&lt;strong&gt;EngUnicodeToMultiByteN&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engunicodetomultibyten)"><strong>EngUnicodeToMultiByteN</strong></a></p></td>
<td align="left"><p>使用当前 ANSI 代码页将指定的 Unicode 字符串转换为 ANSI 字符串。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engwidechartomultibyte" data-raw-source="[&lt;strong&gt;EngWideCharToMultiByte&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engwidechartomultibyte)"><strong>EngWideCharToMultiByte</strong></a></p></td>
<td align="left"><p>使用指定的代码页将宽字符字符串转换为 ANSI 源字符串。</p></td>
</tr>
</tbody>
</table>

 

