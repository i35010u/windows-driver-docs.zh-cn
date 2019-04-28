---
title: PcAllocatedPages 规则 （音频）
description: PcAllocatedPages 规则指定 PortCls 微型端口驱动程序通过调用 AllocatePagesForMdl 或 AllocateContiguousPagesForMdl 方法释放以前分配的页。
ms.assetid: C27B8D30-AE94-4B17-A45B-EBECB8A7B132
ms.date: 05/21/2018
keywords:
- PcAllocatedPages 规则 （音频）
topic_type:
- apiref
api_name:
- PcAllocatedPages
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dd3f96278d50f946f81fb75b47f21bb94f41cf0e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343152"
---
# <a name="pcallocatedpages-rule-audio"></a>PcAllocatedPages 规则 （音频）


PcAllocatedPages 规则指定 PortCls 微型端口驱动程序通过调用 AllocatePagesForMdl 或 AllocateContiguousPagesForMdl 方法释放以前分配的页。

|              |       |
|--------------|-------|
| 驱动程序模型 | Audio |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00071005) |

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
<td align="left"><p>若要验证此规则，请打开命令提示符窗口。 输入驱动程序验证程序命令，并指定<strong>/domain 音频</strong>。</p>
<p>例如：</p>
<p><strong>verifier /domain audio</strong> [<em>options</em>] <strong>/driver</strong> <em>&lt;yourdriver&gt;</em></p>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 





