---
title: Bug 检查 0x124 WHEA_UNCORRECTABLE_ERROR
description: WHEA_UNCORRECTABLE_ERROR bug 检查的值为0x00000124。 此 bug 检查表明发生了致命的硬件错误。
ms.assetid: b3b7c6dd-3891-4ccb-96d1-49e8a2de34c8
keywords:
- Bug 检查 0x124 WHEA_UNCORRECTABLE_ERROR
- WHEA_UNCORRECTABLE_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WHEA_UNCORRECTABLE_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d891e4291d171d477976d281a38e7f5001d3516c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837834"
---
# <a name="bug-check-0x124-whea_uncorrectable_error"></a>Bug 检查0x124： WHEA\_无法纠正\_错误


WHEA\_无法纠正\_错误 bug 检查的值为0x00000124。 此 bug 检查表明发生了致命的硬件错误。 此 bug 检查使用 Windows 硬件错误体系结构（WHEA）提供的错误数据。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="whea_uncorrectable_error-parameters"></a>WHEA\_无法纠正\_错误参数


<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 结构的地址。</p></td>
<td align="left"><p>出现错误的 MCA 银行的 MCi_STATUS 为高32位。</p></td>
<td align="left"><p>出现错误的 MCA 银行的 MCi_STATUS 为低32位。</p></td>
<td align="left"><p>发生了计算机检查异常。</p>
<p>如果处理器基于 x64 体系结构或具有 MCA 功能可用的 x86 体系结构（例如，Intel Pentium Pro、Pentium IV 或强处理器），则这些参数说明适用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 结构的地址。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>发生了已更正的计算机检查异常。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 结构的地址。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>发生了已更正的平台错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 结构的地址。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>出现不可屏蔽中断（NMI）错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 结构的地址。</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>出现无法纠正的 PCI Express 错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 结构的地址。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>出现一般硬件错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 结构的地址</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>出现初始化错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x7</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 结构的地址。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>出现启动错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 结构的地址</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>发生了可伸缩的连贯接口（科幻）一般错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 结构的地址。</p></td>
<td align="left"><p>SAL 日志的长度（以字节为单位）。</p></td>
<td align="left"><p>SAL 日志的地址。</p></td>
<td align="left"><p>发生了无法纠正的基于 Itanium 的计算机检查中止错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xA</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 结构的地址</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>发生了已更正的基于 Itanium 的计算机检查错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xB</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 结构的地址。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>发生了已更正的 Itanium 平台错误。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此 bug 检查通常与物理硬件故障有关。 它可以是热量相关的、缺陷的硬件、内存，甚至是开始出现故障或发生故障的处理器。 如果启用了超计时功能，请尝试禁用该功能。 确认任何冷却系统（如风扇）都正常工作。 运行系统诊断以确认系统内存没有缺陷。 这种情况不太可能，但驱动程序可能会导致硬件因此错误检查而失败。

有关其他常规错误检查的故障排除信息，请参阅[**蓝屏数据**](blue-screen-data.md)。

<a name="remarks"></a>备注
-------

[ **！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。

参数1标识报告错误的错误源的类型。 参数2保存说明错误情况\_记录结构中的 WHEA\_错误的地址。

发生硬件错误时，WHEA 会创建一个错误记录，用于存储与硬件错误条件相关的错误信息。 每个错误记录由 WHEA\_错误\_记录结构中进行描述。 Windows 内核包含错误记录，其中包含为响应错误而引发的 Windows 事件跟踪（ETW）硬件错误事件，以便在系统事件日志中保存错误记录。 WHEA 所使用的错误记录的格式基于常见平台错误记录，如2.2 版统一可扩展固件接口（UEFI）规范的附录 N 中所述。 有关详细信息，请参阅[WHEA\_错误\_记录](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_record)和[Windows 硬件错误体系结构（WHEA）](https://docs.microsoft.com/windows-hardware/drivers/whea)。

可以使用[ **！ errrec**](-errrec.md) &lt;addr&gt; 使用参数2中提供的地址显示 WHEA\_错误\_记录结构。 [ **！ Whea**](-whea.md)和[ **！ errpkt**](-errpkt.md)扩展可用于显示其他 whea 信息。

有关详细信息，请参阅以下主题：

[使用 Windows 调试器（WinDbg）进行故障转储分析](crash-dump-files.md)

[使用 WinDbg 分析内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)

[使用！分析扩展](using-the--analyze-extension.md)和[！分析](-analyze.md)

Windows Vista 之前的 Windows 版本不支持此 bug 检查。 相反，计算机检查异常通过[**bug 检查 0x9C**](bug-check-0x9c--machine-check-exception.md)进行报告。

 

 




