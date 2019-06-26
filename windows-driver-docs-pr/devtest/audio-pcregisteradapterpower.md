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
ms.openlocfilehash: 5263ebd8c49dc9ab3351e30cca4512f6fee17352
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394021"
---
# <a name="pcregisteradapterpower-rule-audio"></a>PcRegisterAdapterPower 规则 （音频）


PcRegisterAdapterPower 规则指定 PortCls 微型端口驱动程序不应：

-   调用[ **PcRegisterAdapterPowerManagement** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisteradapterpowermanagement)两次而无需对的干预调用[ **PcUnregisterAdapterPowerManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcunregisteradapterpowermanagement)。
-   调用[ **PcUnregisterAdapterPowerManagement** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcunregisteradapterpowermanagement)而无需调用[ **PcRegisterAdapterPowerManagement** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisteradapterpowermanagement)第一个。

|              |       |
|--------------|-------|
| 驱动程序模型 | Audio |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x00071006) |

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
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 





