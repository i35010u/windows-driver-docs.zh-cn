---
title: Bug 检查 0x124 WHEA_UNCORRECTABLE_ERROR
description: WHEA_UNCORRECTABLE_ERROR bug 检查具有 0x00000124 值。 此 bug 检查指示发生致命硬件错误。
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
ms.openlocfilehash: d6d0a0bffdc0d067be7bf742c727e159be8ab30a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358133"
---
# <a name="bug-check-0x124-wheauncorrectableerror"></a>Bug 检查 0x124：WHEA\_无法纠正\_错误


WHEA\_无法纠正\_错误 bug 检查的值为 0x00000124。 此 bug 检查指示发生致命硬件错误。 此 bug 检查使用提供的 Windows 硬件错误体系结构 (WHEA) 的错误数据。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="wheauncorrectableerror-parameters"></a>WHEA\_无法纠正\_错误参数


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
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 结构地址。</p></td>
<td align="left"><p>发生了错误 MCA bank MCi_STATUS MSR 的高 32 位。</p></td>
<td align="left"><p>发生了错误 MCA bank MCi_STATUS MSR 低 32 位。</p></td>
<td align="left"><p>计算机检查异常发生。</p>
<p>这些参数说明应用如果处理器基于 x64 体系结构或 x86 体系结构具有 MCA 提供的功能 （例如，Intel Pentium Pro、 Pentium IV 或 Xeon）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 结构地址。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>更正后的计算机检查异常发生。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 结构地址。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>已更正的平台出错。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 结构地址。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>不可屏蔽中断 (NMI) 错误出现。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 结构地址。</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>无法纠正 PCI Express 时出错。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 结构地址。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>出现一般的硬件错误。</p></td>
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
<td align="left"><p>WHEA_ERROR_RECORD 结构地址。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>发生了启动错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 结构的地址</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>可缩放一致接口 (SCI) 发生一般性错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 结构地址。</p></td>
<td align="left"><p>长度，以字节为单位，SAL 日志。</p></td>
<td align="left"><p>SAL 日志的地址。</p></td>
<td align="left"><p>出现了无法纠正的基于 Itanium 的计算机检查中止错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xA</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 结构的地址</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>已更正的基于 Itanium 的计算机检查出错。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xB</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 结构地址。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"><p>已更正的 Itanium 平台错误出现。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

检查此错误通常与物理硬件故障。 它可以是相关的热、 有故障的硬件、 内存或甚至开始出现故障或已失败的处理器。 如果已启用过度计时，请尝试禁用它。 确认等赛事的球迷们任何冷却系统功能。 运行系统诊断，以确认系统内存未损坏。 它是不太可能，但可能驱动程序导致了与此 bug 检查失败的硬件。

有关故障排除信息的其他常规错误检查，请参阅[**蓝色屏幕数据**](blue-screen-data.md)。

<a name="remarks"></a>备注
-------

[ **！ 分析**](-analyze.md)调试扩展显示有关错误检查的信息，有助于在确定根本原因。

参数 1 标识报告了错误的错误源的类型。 参数 2 保留的地址 WHEA\_错误\_描述错误条件的记录结构。

出现硬件错误时，WHEA 会创建错误记录来存储与硬件错误条件相关联的错误信息。 每个错误记录描述 WHEA\_错误\_记录结构。 Windows 内核包含与，它会发出错误响应，以便在系统事件日志中保存错误记录的事件跟踪 Windows (ETW) 的硬件错误事件的错误记录。 由 WHEA 错误记录的格式基于常见的平台错误记录版本 2.2 的统一可扩展固件接口 (UEFI) 规范的附录 N 中所述。 有关详细信息，请参阅[WHEA\_错误\_记录](https://msdn.microsoft.com/library/windows/hardware/ff560483)并[Windows 硬件错误体系结构 (WHEA)](https://msdn.microsoft.com/library/windows/hardware/ff559509)。

可以使用[ **！ errrec** ](-errrec.md) &lt;addr&gt;以显示 WHEA\_错误\_记录结构使用参数 2 中提供的地址。 [ **！ Whea** ](-whea.md)并[ **！ errpkt** ](-errpkt.md)扩展可用于显示 WHEA 的其他信息。

有关详细信息，请参阅以下主题：

[故障转储分析使用 Windows 调试器 (WinDbg)](crash-dump-files.md)

[分析具有 WinDbg 的内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)

[使用 ！ 分析扩展](using-the--analyze-extension.md)和[！ 分析](-analyze.md)

在 Windows Vista 之前的 Windows 版本不支持此 bug 检查。 相反，通过报告计算机检查异常[ **bug 检查 0x9C**](bug-check-0x9c--machine-check-exception.md)。

 

 




