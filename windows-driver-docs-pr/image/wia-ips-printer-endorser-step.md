---
title: WIA\_IPS\_打印机\_印记签署器\_步骤
description: 默认情况下印刷器/印记签署器 imprints 或扫描每个文档页面上予以认可。
ms.assetid: A4455204-6502-4BE7-9EE3-B5616089FA05
keywords:
- WIA_IPS_PRINTER_ENDORSER_STEP 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_STEP
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6a0b583f55276e4dd246f66a7c9a8d74e7a8a943
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545041"
---
# <a name="wiaipsprinterendorserstep"></a>WIA\_IPS\_打印机\_印记签署器\_步骤


默认情况下印刷器/印记签署器 imprints 或扫描每个文档页面上予以认可。 可以通过使用客户端更改此必需的默认行为**WIA\_IPS\_打印机\_印记签署器\_步骤**属性。 例如，客户端应用程序可以将当前值设置为 2，以具有每个其他扫描的页面印刷/认可 （0、 2、 4、 6，...）。WIA 微型驱动程序创建并维护此属性。




属性类型：VT\_UI4

有效值：WIA\_PROP\_RANGE

访问权限：读/写

<a name="remarks"></a>备注
-------

必需的默认值为**WIA\_IPS\_打印机\_印记签署器\_步骤**属性为 1 （每个页面）。 值为 0 是无效的。

与大多数 WIA\_PROP\_范围属性 WIA 微型驱动程序可以实现包含一个单个值、 最小等的最大值和步骤值为零的范围。

此属性必须受所有印刷器/印记签署器数据源项。 值为 1 （每个页面） 是必需的。

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

 

 





