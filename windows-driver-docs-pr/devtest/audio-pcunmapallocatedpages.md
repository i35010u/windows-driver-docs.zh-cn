---
title: PcUnmapAllocatedPages 规则（音频）
description: PcUnmapAllocatedPages 规则指定 PortCls 微型端口驱动程序未映射当前映射的 MDL，而不先取消其映射。PortCls 微型端口驱动程序在使用 IMiniportWaveRTStream 接口释放内存之前 messagebox 取消内存。
ms.assetid: 0ADF523C-9480-4AD2-8B98-23C95571CB0B
ms.date: 05/21/2018
keywords:
- PcUnmapAllocatedPages 规则（音频）
topic_type:
- apiref
api_name:
- PcUnmapAllocatedPages
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 88add45091a4f03a9b733b4a5328e29266addeba
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916367"
---
# <a name="pcunmapallocatedpages-rule-audio"></a>PcUnmapAllocatedPages 规则（音频）


PcUnmapAllocatedPages 规则指定：

-   PortCls 微型端口驱动程序不会映射当前映射的 MDL，而不先取消其映射。
-   PortCls 微型端口驱动程序在使用[IMiniportWaveRTStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstream)接口释放内存之前 messagebox 取消内存。

**驱动程序模型：音频**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 找到了具有此规则的 Bug 检查 | [**Bug 检查0xC4：驱动程序 \_\_检测到 \_ 验证程序冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)（0x00071004） |

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
<td align="left"><p>若要验证此规则，请打开 "命令提示符" 窗口。 输入 Driver Verifier 命令并指定<strong>/domain 音频</strong>。</p>
<p>例如：</p>
<p><strong>verifier/domain 音频</strong>[<em>options</em>] <strong>/driver</strong> <em> &lt; yourdriver &gt; </em></p>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 





