---
title: PcRegisterAdapterPower 规则 （音频）
description: PcRegisterAdapterPower 规则指定 PortCls 微型端口驱动程序不应调用两次都没有有干预性的 PcRegisterAdapterPowerManagement 调用的而无需 PcUnregisterAdapterPowerManagement.Call PcUnregisterAdapterPowerManagement 到第一次调用 PcRegisterAdapterPowerManagement。
ms.assetid: 8F6E6B1D-F19C-469A-BC5A-061996BEA532
ms.date: 05/21/2018
keywords:
- PcRegisterAdapterPower 规则 （音频）
topic_type:
- apiref
api_name:
- PcRegisterAdapterPower
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4bd4980b5b890db28179dab1b6009db07ca24d2f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343140"
---
# <a name="pcregisteradapterpower-rule-audio"></a>PcRegisterAdapterPower 规则 （音频）


PcRegisterAdapterPower 规则指定 PortCls 微型端口驱动程序不应：

-   调用[ **PcRegisterAdapterPowerManagement** ](https://msdn.microsoft.com/library/windows/hardware/ff537724)两次而无需对的干预调用[ **PcUnregisterAdapterPowerManagement**](https://msdn.microsoft.com/library/windows/hardware/ff537735)。
-   调用[ **PcUnregisterAdapterPowerManagement** ](https://msdn.microsoft.com/library/windows/hardware/ff537735)而无需调用[ **PcRegisterAdapterPowerManagement** ](https://msdn.microsoft.com/library/windows/hardware/ff537724)第一个。

|              |       |
|--------------|-------|
| 驱动程序模型 | Audio |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00071006) |

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

 

 

 





