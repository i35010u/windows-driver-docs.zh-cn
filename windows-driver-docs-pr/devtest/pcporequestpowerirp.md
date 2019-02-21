---
title: PcPoRequestPowerIrp 规则 （音频）
description: 此规则验证 PortCls 微型端口驱动程序不应调用与 IRP PoRequestPowerIrp\_MN\_设置\_电源。
ms.assetid: 9AF26E98-CB8A-41F1-BF40-1B5FBFD04550
ms.date: 05/21/2018
keywords:
- PcPoRequestPowerIrp 规则 （音频）
topic_type:
- apiref
api_name:
- PcPoRequestPowerIrp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: abdd26de34c88a8f4a3db2bff35c8f67f653a59c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540802"
---
# <a name="pcporequestpowerirp-rule-audio"></a>PcPoRequestPowerIrp 规则 （音频）


此规则验证 PortCls 微型端口驱动程序不应调用[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)与[ **IRP\_MN\_设置\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551744)。

|              |       |
|--------------|-------|
| 驱动程序模型 | Audio |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x0007100A) |

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

 

 

 





