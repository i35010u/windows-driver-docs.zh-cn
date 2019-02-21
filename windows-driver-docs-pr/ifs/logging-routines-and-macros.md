---
title: 日志记录例程和宏
description: 日志记录例程和宏
ms.assetid: 343605bc-7992-4e9c-a9af-f57bb958a38b
keywords:
- RDBSS WDK 文件系统中，日志记录
- 重定向驱动器缓冲子系统 WDK 的文件系统，日志记录
- 日志记录 WDK RDBSS
- RDBSSLOG 宏
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 686a8a93e2190d0a347746876f4862629ad4a7e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542410"
---
# <a name="logging-routines-and-macros"></a>日志记录例程和宏


## <span id="ddk_logging_functions_and_macros_if"></span><span id="DDK_LOGGING_FUNCTIONS_AND_MACROS_IF"></span>


RDBSS 为日志记录提供大量的例程。 这些日志记录工具始终都存在。 当定义 RDBSSLOG 宏时，启用检查生成的日志记录调用生成。 如果未\_RDBSSLOG 设置，则将禁用日志记录调用。

日志记录例程创建存储在一个循环缓冲区中的日志记录。 每条记录上受限于任何一侧记录说明符。 此记录描述符是四个字节长。

下表包含日志记录例程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554515" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554515)"><strong>RxLogEventDirect</strong></a></p></td>
<td align="left"><p>此例程称为到 I/O 错误日志记录的错误。</p>
<p>建议<strong>RxLogFailure</strong>或<strong>RxLogEvent</strong>而不是直接调用该例程使用宏。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554519" data-raw-source="[&lt;strong&gt;RxLogEventWithAnnotation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554519)"><strong>RxLogEventWithAnnotation</strong></a></p></td>
<td align="left"><p>此例程分配了 I/O 错误的日志记录、 填充的日志记录，并将此记录写入到 I/O 错误日志。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554524" data-raw-source="[&lt;strong&gt;RxLogEventWithBufferDirect&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554524)"><strong>RxLogEventWithBufferDirect</strong></a></p></td>
<td align="left"><p>此例程分配了 I/O 错误的日志记录、 填充的日志记录，并将此记录写入到 I/O 错误日志。 此例程编码为存储在 I/O 错误日志记录的原始数据缓冲区的行号和状态。</p>
<p>建议<strong>RxLogFailureWithBuffer</strong>而不是直接调用该例程使用宏。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557368" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557368)"><strong>_RxLog</strong></a></p></td>
<td align="left"><p>此例程采用格式字符串和可变数量的参数，并设置用于记录为一个 I/O 错误日志条目，如果启用日志记录的输出字符串的格式。</p>
<p>建议<strong>RxLog</strong>而不是直接调用该例程使用宏。</p>
<p>此例程才可用的 Windows Server 2003、 Windows XP 和 Windows 2000 上 RDBSS checked 版本。</p></td>
</tr>
</tbody>
</table>

 

以下宏的调用上表中列出的例程的 rxlog.h 和 rxprocs.h 标头文件中定义。 而不是直接调用这些例程通常使用这些宏。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">宏</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>RxLog</strong>(<em>Args</em>)</p></td>
<td align="left"><p>此宏调用检查内部版本号<a href="https://msdn.microsoft.com/library/windows/hardware/ff557368" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557368)"> <strong>_RxLog</strong> </a>例程。</p>
<p>在零售版本，此宏没有任何影响。</p>
<p>请注意，参数<strong>RxLog</strong>必须为括在一对括号，若要启用翻译为 null 的调用时应关闭日志记录。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxLogEvent</strong> (<em>_DeviceObject</em>, <em>_OriginatorId</em>, <em>_EventId</em>, <em>_Status</em>)</p></td>
<td align="left"><p>此宏将调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff554515" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554515)"> <strong>RxLogEventDirect</strong> </a>例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxLogFailure</strong> (<em>_DeviceObject</em>, <em>_OriginatorId</em>, <em>_EventId</em>, <em>_Status</em>)</p></td>
<td align="left"><p>此宏将调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff554515" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554515)"> <strong>RxLogEventDirect</strong> </a>例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxLogFailureWithBuffer</strong> (<em>_DeviceObject</em>, <em>_OriginatorId</em>, <em>_EventId</em>, <em>_Status</em>, <em>_Buffer</em>, <em>_Length</em>)</p></td>
<td align="left"><p>此宏将调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff554524" data-raw-source="[&lt;strong&gt;RxLogEventWithBufferDirect&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554524)"> <strong>RxLogEventWithBufferDirect</strong> </a>例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxLogRetail</strong>(<em>Args</em>)</p></td>
<td align="left"><p>此宏调用检查内部版本号<a href="https://msdn.microsoft.com/library/windows/hardware/ff557368" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557368)"> <strong>_RxLog</strong> </a>例程。</p>
<p>在零售版本，此宏没有任何影响。</p>
<p>请注意，参数<strong>RxLogRetail</strong>必须为括在一对括号，若要启用翻译为 null 的调用时应关闭日志记录。</p></td>
</tr>
</tbody>
</table>

 

 

 




