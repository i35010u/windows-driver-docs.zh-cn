---
title: 日志记录例程和宏
description: 日志记录例程和宏
ms.assetid: 343605bc-7992-4e9c-a9af-f57bb958a38b
keywords:
- RDBSS WDK 文件系统，日志记录
- 重定向驱动器缓冲子系统 WDK 文件系统，日志记录
- 记录 WDK RDBSS
- RDBSSLOG 宏
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21026d5e215b0e16c343d0fa24fa0c243e247627
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104788"
---
# <a name="logging-routines-and-macros"></a>日志记录例程和宏


## <span id="ddk_logging_functions_and_macros_if"></span><span id="DDK_LOGGING_FUNCTIONS_AND_MACROS_IF"></span>


RDBSS 提供了许多用于日志记录的例程。 这些日志记录功能始终存在。 定义 RDBSSLOG 宏时，会启用对已检查生成的日志记录调用的生成。 如果未 \_ 设置 RDBSSLOG，则会禁用日志记录调用。

日志记录例程会创建存储在循环缓冲区中的日志记录。 每个记录都由记录描述符包围。 此记录描述符的长度为四个字节。

下表包括日志记录例程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程所返回的值</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect)"><strong>RxLogEventDirect</strong></a></p></td>
<td align="left"><p>调用此例程以便向 i/o 错误日志记录错误。</p>
<p>建议使用 <strong>RxLogFailure</strong> 或 <strong>RxLogEvent</strong> 宏，而不是直接调用此例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithannotation" data-raw-source="[&lt;strong&gt;RxLogEventWithAnnotation&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithannotation)"><strong>RxLogEventWithAnnotation</strong></a></p></td>
<td align="left"><p>此例程分配 i/o 错误日志记录，填充日志记录，并将此记录写入 i/o 错误日志。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithbufferdirect" data-raw-source="[&lt;strong&gt;RxLogEventWithBufferDirect&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithbufferdirect)"><strong>RxLogEventWithBufferDirect</strong></a></p></td>
<td align="left"><p>此例程分配 i/o 错误日志记录，填充日志记录，并将此记录写入 i/o 错误日志。 此例程将行号和状态编码为存储在 i/o 错误日志记录中的原始数据缓冲区。</p>
<p>建议使用 <strong>RxLogFailureWithBuffer</strong> 宏，而不是直接调用此例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog)"><strong>_RxLog</strong></a></p></td>
<td align="left"><p>如果启用了日志记录，则此例程采用格式字符串和可变数量的参数并将用于记录的输出字符串的格式设置为 i/o 错误日志项。</p>
<p>建议使用 <strong>RxLog</strong> 宏，而不是直接调用此例程。</p>
<p>此例程仅适用于在 Windows Server 2003、Windows XP 和 Windows 2000 上的 RDBSS 的已检查版本。</p></td>
</tr>
</tbody>
</table>

 

以下宏在 rxlog 和 rxprocs 头文件中定义，这些文件调用上表中列出的例程。 通常使用这些宏，而不是直接调用这些例程。

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
<td align="left"><p><strong>RxLog</strong> (<em>参数</em>) </p></td>
<td align="left"><p>在选中的生成上，此宏调用 <a href="/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog)"><strong>_RxLog</strong></a> 例程。</p>
<p>在零售版上，此宏不执行任何操作。</p>
<p>请注意， <strong>RxLog</strong> 的参数必须包含一对括号，以便在应关闭日志记录时允许转换为 null 调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxLogEvent</strong> (<em>_DeviceObject</em>、 <em>_OriginatorId</em>、 <em>_EventId</em>、 <em>_Status</em>) </p></td>
<td align="left"><p>此宏调用 <a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect)"><strong>RxLogEventDirect</strong></a> 例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxLogFailure</strong> (<em>_DeviceObject</em>、 <em>_OriginatorId</em>、 <em>_EventId</em>、 <em>_Status</em>) </p></td>
<td align="left"><p>此宏调用 <a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect)"><strong>RxLogEventDirect</strong></a> 例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxLogFailureWithBuffer</strong> (<em>_DeviceObject</em>、 <em>_OriginatorId</em>、 <em>_EventId</em>、 <em>_Status</em>、 <em>_Buffer</em>_Length <em>) </em></p></td>
<td align="left"><p>此宏调用 <a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithbufferdirect" data-raw-source="[&lt;strong&gt;RxLogEventWithBufferDirect&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithbufferdirect)"><strong>RxLogEventWithBufferDirect</strong></a> 例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxLogRetail</strong> (<em>参数</em>) </p></td>
<td align="left"><p>在选中的生成上，此宏调用 <a href="/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog)"><strong>_RxLog</strong></a> 例程。</p>
<p>在零售版上，此宏不执行任何操作。</p>
<p>请注意， <strong>RxLogRetail</strong> 的参数必须包含一对括号，以便在应关闭日志记录时允许转换为 null 调用。</p></td>
</tr>
</tbody>
</table>

 

