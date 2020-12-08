---
title: 'PcAllocateAndMapPages 规则 (音频) '
description: PcAllocateAndMapPages 规则指定 PortCls 微型端口驱动程序使用正确的参数 IPortWaveRTStream AllocatePagesForMdlIPortWaveRTStream AllocateContiguousPagesForMdl IPortWaveRTStream MapAllocatedPages 调用以下接口。
ms.date: 05/21/2018
keywords:
- 'PcAllocateAndMapPages 规则 (音频) '
topic_type:
- apiref
api_name:
- PcAllocateAndMapPages
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3ffd181a314ca2ac5399e043b184367e67bd7644
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791953"
---
# <a name="pcallocateandmappages-rule-audio"></a>PcAllocateAndMapPages 规则 (音频) 


PcAllocateAndMapPages 规则指定 PortCls 微型端口驱动程序使用正确的参数调用以下接口：

-   IPortWaveRTStream::AllocatePagesForMdl
-   IPortWaveRTStream::AllocateContiguousPagesForMdl
-   IPortWaveRTStream::MapAllocatedPages

**驱动程序模型：音频**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x00071009) 


<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>若要验证此规则，请打开 "命令提示符" 窗口。 输入 Driver Verifier 命令并指定 <strong>/domain 音频</strong>。</p>
<p>例如：</p>
<p><strong>verifier/domain 音频</strong>[<em>options</em>] <strong>/driver</strong> <em> &lt; yourdriver &gt; </em></p>
<p>有关详细信息，请参阅<a href="/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a>。</p></td>
</tr>
</tbody>
</table>

 

