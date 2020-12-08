---
title: WIA \_ IP \_ 支持 \_ 子 \_ 项目 \_ 创建
description: WIA \_ ip \_ 支持 \_ 子 \_ 项目 \_ 创建属性指示设备是否支持创建子项目。
keywords:
- WIA_IPS_SUPPORTS_CHILD_ITEM_CREATION 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_SUPPORTS_CHILD_ITEM_CREATION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffc34fe4b94f336fa3f1f0282dc64ae02632c81a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814413"
---
# <a name="wia_ips_supports_child_item_creation"></a>WIA \_ IP \_ 支持 \_ 子 \_ 项目 \_ 创建


WIA \_ ip \_ 支持 \_ 子 \_ 项目 \_ 创建属性指示设备是否支持创建子项目。 WIA 微型驱动程序创建并维护此属性

属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

支持 [**wia \_ ips \_ 分段**](wia-ips-segmentation.md) 属性和 WIA \_ 使用 \_ 分段 \_ 筛选器值的项还必须支持 WIA \_ ip \_ 支持 \_ 子 \_ 项目 \_ 创建属性，并将其设置为 **TRUE**。

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
<td><p>在 Windows Vista 和更高版本的操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA \_ IPS \_ 分段**](wia-ips-segmentation.md)

 

 






