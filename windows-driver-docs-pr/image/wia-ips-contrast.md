---
title: WIA\_IP\_对比度
description: WIA\_IP\_对比度属性包含设备的当前硬件对比度设置。
ms.assetid: 7fecfd43-212c-40e6-8520-ef1819448895
keywords:
- WIA_IPS_CONTRAST 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_CONTRAST
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 806f6358df3fb4927f980b4cf6d33e7f9bba0b9c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544475"
---
# <a name="wiaipscontrast"></a>WIA\_IP\_对比度


WIA\_IP\_对比度属性包含设备的当前硬件对比度设置。

## <span id="ddk_wia_ips_contrast_si"></span><span id="DDK_WIA_IPS_CONTRAST_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_RANGE

访问权限：读取/写入

<a name="remarks"></a>备注
-------

应用程序设置 WIA\_IP\_对比度属性和硬件的对比度值。 WIA 微型驱动程序创建并维护此属性。

值为 WIA\_IP\_对比度应映射到 1000，其中 −1000 对应于最小对比度、 0 对应于正常对比度和 1000年对应于最大对比度 −1000 从范围中。

WIA\_IP\_对比度是所必需的所有图像获取项。

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

 

 





