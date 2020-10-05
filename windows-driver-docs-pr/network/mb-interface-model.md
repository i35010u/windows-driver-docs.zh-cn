---
title: MB 接口模型概述
description: 本部分提供基于移动宽带接口模型（ (MBIM) 规范）实现的移动宽带设备的信息。
ms.assetid: B1C6D5F4-63E2-4C46-8038-71B8144AB474
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ea41c6e010784316f6c7315e066019077eaf10d
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733909"
---
# <a name="mb-interface-model-overview"></a>MB 接口模型概述


本部分提供基于移动宽带接口模型（ (MBIM) 规范）实现的移动宽带设备的信息。

从 Windows 8 开始，Microsoft 为 MBIM 函数提供了一个收件箱类驱动程序（称为 MBCD）。 Microsoft 已为复合设备提供了一个收件箱驱动程序 USBCCGP。 本部分介绍移动宽带设备在 Windows 8 中加载 USBCCGP 和 MBCD 所需的要求。

使用 WMC UFD 将接口分组到函数的移动宽带复合设备应该实现 Microsoft OS 描述符，以便在 Windows 8 上加载 USBCCGP，并指示 USBCCGP 分析 WMC UFD 以创建函数。 使用接口关联描述符 (IADs) 将接口分组到函数中的移动宽带复合设备无需实现 Microsoft OS 描述符即可加载 USBCCGP。

向后兼容的 MBIM 函数应实现 Microsoft OS 描述符以加载 MBCD。 不向后兼容的 MBIM 函数不需要实现 Microsoft OS 描述符来加载 MBCD。

显示标识变形的移动宽带设备还应实现 Microsoft OS 描述符。

这些方案在整个 MB 接口模型主题中进行了更详细的讨论。 下表总结了这些子主题中提到的所有 Microsoft 操作系统兼容 Id。 有关详细信息，请参阅 [MICROSOFT OS 描述符](/previous-versions/gg463179(v=msdn.10))。

*Microsoft 操作系统兼容 Id*

<table>  
<colgroup> <col width="33%" /> <col width="33%" /> <col width="33%" /> </colgroup>  
<thead>  
<tr class="header">  
<th align="left">Microsoft OS 兼容 ID</th>
<th align="left">Microsoft 操作系统子兼容 ID</th>
<th align="left">对于方案是必需的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>"CDC_WMC"</p></td>
<td align="left"><p></p></td>
<td align="left"><p>正在加载复合设备上的 USBCCGP，这些设备使用 WMC UFD 将接口分组到函数</p></td>
</tr>
<tr class="even">
<td align="left"><p>MBIM</p></td>
<td align="left"><p></p></td>
<td align="left"><p>正在 MBIM 向后兼容的函数上加载 MBCD</p></td>
</tr>
<tr class="odd">
<td align="left"><p>"ALTRCFG"</p></td>
<td align="left"><p>ASCII 中的配置编号</p></td>
<td align="left"><p>标识变形与 IADs</p></td>
</tr>
<tr class="even">
<td align="left"><p>"WMCALTR"</p></td>
<td align="left"><p>ASCII 中的配置编号</p></td>
<td align="left"><p>标识变形与 WMC UFD</p></td>
</tr>
</tbody>
</table>

 

以下子主题中进一步描述了 MB 接口模型：

[MB 接口条款](mb-interface-terms.md) 
[MB 联合函数描述符](mb-union-function-descriptors.md) 
[MB 标识变形](mb-identity-morphing.md) 
[MB 接口型号补充](mb-interface-model-supplement.md)
 

