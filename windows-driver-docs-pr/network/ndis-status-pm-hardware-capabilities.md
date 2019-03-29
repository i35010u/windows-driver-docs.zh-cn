---
title: NDIS_STATUS_PM_HARDWARE_CAPABILITIES
description: NDIS_STATUS_PM_HARDWARE_CAPABILITIES 状态指示过量发生了更改的网络适配器的电源管理 (PM) 硬件功能中的驱动程序。
ms.assetid: A4AACA48-DCD2-44FA-B016-52C37EE9A1D6
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_PM_HARDWARE_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 61ecf125922f6c318968941532b461de36a8d811
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565719"
---
# <a name="ndisstatuspmhardwarecapabilities"></a>NDIS\_状态\_PM\_硬件\_功能


**NDIS\_状态\_PM\_硬件\_功能**状态指示为过量驱动程序的电源管理 (PM) 硬件功能的网络中的更改发生了适配器。

<a name="remarks"></a>备注
-------

微型端口驱动程序将生成**NDIS\_状态\_PM\_硬件\_功能**状态指示时对先前报告的电源管理功能的更新是必需的。

802.11 网络适配器的微型端口驱动程序可以生成此状态指示。

提供负载平衡故障转移 (LBFO) 支持的 MUX 中间驱动程序还可以生成此状态指示。 MUX 驱动程序将聚合的基础网络适配器 LBFO 团队的一部分的 PM 功能。 如果 PM 功能更改，因为适配器已添加或从团队中删除，MUX 驱动程序必须生成此状态指示。 有关 LBFO MUX 中间驱动程序的详细信息，请参阅[NDIS MUX 中间驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff566498)。

**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构包含一个指向[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)结构的更新的电源管理功能。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)

[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

 

 




