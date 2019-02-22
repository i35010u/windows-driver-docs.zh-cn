---
title: WIA\_IPS\_打印机\_印记签署器\_墨迹
description: WIA\_IPS\_打印机\_印记签署器\_墨迹属性用于报告的印刷器/印记签署器设备的当前墨迹缺墨状态。
ms.assetid: CCD7C10A-7739-4E75-B30C-2C2E7FE90B13
keywords:
- WIA_IPS_PRINTER_ENDORSER_INK 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_INK
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f00dcd70369a07020ad8fefe18436f8e42642578
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545044"
---
# <a name="wiaipsprinterendorserink"></a>WIA\_IPS\_打印机\_印记签署器\_墨迹


**WIA\_IPS\_打印机\_印记签署器\_墨迹**属性用于报告的印刷器/印记签署器设备的当前墨迹缺墨状态。 属性值指示剩余的可用手写内容，以占总容量。 例如，值为 50 指示有一半或 50%的剩余墨水。 此属性是初始化和维护的 WIA 微型驱动程序。 与 Windows 8 和更高版本的 Windows 提供了此功能。

属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读写

<a name="remarks"></a>备注
-------

**WIA\_IPS\_打印机\_印记签署器\_墨迹**属性是可选的印刷器/印记签署器项。 此属性的有效值为 0 到 100 (含) 之间。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





