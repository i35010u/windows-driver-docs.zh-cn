---
title: MB 接口模型
description: 本部分提供了基于移动宽带接口模型 (MBIM) 规范实现的移动宽带设备的信息。
ms.assetid: B1C6D5F4-63E2-4C46-8038-71B8144AB474
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 907eb83a0ddc9b27a179000e745bce9b4a19b0e8
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464287"
---
# <a name="mb-interface-model"></a>MB 接口模型


本部分提供了基于移动宽带接口模型 (MBIM) 规范实现的移动宽带设备的信息。

从 Windows 8 开始，Microsoft 提供的收件箱类驱动程序，称为 MBCD，MBIM 函数。 Microsoft 已经提供了复合设备收件箱驱动 USBCCGP。 本部分介绍移动宽带设备加载 USBCCGP 和 MBCD Windows 8 中的要求。

对分组接口使用 WMC UFD 到函数中的移动宽带的复合设备应实现 Microsoft 操作系统描述符，以加载 Windows 8 上的 USBCCGP，并指示 USBCCGP 分析 WMC UFD 创建函数。 将接口关联描述符 (Iad) 用于分组接口到函数中的移动宽带的复合设备不需要实现 Microsoft 操作系统描述符，以加载 USBCCGP。

MBIM 向后兼容的功能应实现 Microsoft 操作系统描述符，以加载 MBCD。 不能向后兼容的 MBIM 功能不需要实现 Microsoft 操作系统描述符，以加载 MBCD。

显示标识变形的移动宽带设备还应实现 Microsoft 操作系统描述符。

在 MB 接口模型主题更详细地讨论了这些方案。 下表汇总了所有这些子主题中所述的 Microsoft 操作系统兼容 Id。 有关详细信息请参阅[Microsoft OS 描述符](https://go.microsoft.com/fwlink/p/?linkid=308932)。

*Microsoft 操作系统兼容 Id*

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Microsoft OS Compatible ID</th>
<th align="left">Microsoft OS 子兼容 ID</th>
<th align="left">所需的方案</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>"CDC_WMC"</p></td>
<td align="left"><p></p></td>
<td align="left"><p>用于 WMC UFD 接口分组到函数中的复合设备上加载 USBCCGP</p></td>
</tr>
<tr class="even">
<td align="left"><p>"MBIM"</p></td>
<td align="left"><p></p></td>
<td align="left"><p>加载 MBCD MBIM 向后兼容函数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>"ALTRCFG"</p></td>
<td align="left"><p>ASCII 中配置编号</p></td>
<td align="left"><p>标识与 Iad 变形</p></td>
</tr>
<tr class="even">
<td align="left"><p>"WMCALTR"</p></td>
<td align="left"><p>ASCII 中配置编号</p></td>
<td align="left"><p>标识与 WMC UFD 变形</p></td>
</tr>
</tbody>
</table>

 

MB 接口模型中作了进一步介绍在以下子主题：

[MB 接口条款](mb-interface-terms.md)
[MB 联合功能描述符](mb-union-function-descriptors.md)
[MB 标识变形](mb-identity-morphing.md)
[MB 接口模型补充程序](mb-interface-model-supplement.md)
 

 





