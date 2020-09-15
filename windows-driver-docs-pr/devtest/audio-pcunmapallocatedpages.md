---
title: 'PcUnmapAllocatedPages 规则 (音频) '
description: PcUnmapAllocatedPages 规则指定 PortCls 微型端口驱动程序未映射当前映射的 MDL，而不先取消其映射。PortCls 微型端口驱动程序在使用 IMiniportWaveRTStream 接口释放内存之前 messagebox 取消内存。
ms.assetid: 0ADF523C-9480-4AD2-8B98-23C95571CB0B
ms.date: 05/21/2018
keywords:
- 'PcUnmapAllocatedPages 规则 (音频) '
topic_type:
- apiref
api_name:
- PcUnmapAllocatedPages
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1e947559f527482d892c6e499c31a66fe2faa017
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103976"
---
# <a name="pcunmapallocatedpages-rule-audio"></a>PcUnmapAllocatedPages 规则 (音频) 


PcUnmapAllocatedPages 规则指定：

-   PortCls 微型端口驱动程序不会映射当前映射的 MDL，而不先取消其映射。
-   PortCls 微型端口驱动程序在使用 [IMiniportWaveRTStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstream) 接口释放内存之前 messagebox 取消内存。

**驱动程序模型：音频**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x00071004) 


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

 

