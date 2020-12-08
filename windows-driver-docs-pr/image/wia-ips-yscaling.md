---
title: WIA \_ IP \_ YSCALING
description: WIA \_ IPS \_ YSCALING 属性指示是否应将沿 y 轴的缩放应用于扫描。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_YSCALING 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_YSCALING
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdfa1055e5272cd01aa5358eaedf3279c53032d5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838271"
---
# <a name="wia_ips_yscaling"></a>WIA \_ IP \_ YSCALING


WIA \_ IPS \_ YSCALING 属性指示是否应将沿 y 轴的缩放应用于扫描。 WIA 微型驱动程序创建并维护此属性。

属性类型： VT \_ I4

有效值： WIA "内容范围" 或 "WIA 内容" \_ \_ \_ \_ 列表

访问权限：读/写或只读

<a name="remarks"></a>备注
-------

WIA \_ IPS YSCALING 属性的有效值 \_ 范围为1到65535。

WIA \_ ip \_ YSCALING 指示仅沿 y 轴缩放。 若要统一缩放图像，必须在 WIA \_ ips \_ YSCALING 和 [**wia \_ ips \_ XSCALING**](wia-ips-xscaling.md) 属性中设置类似值。

请开考虑以下示例：

-   100，无 (1x，100% ) 缩放。 不会更改图像。

-   050，1/2 缩放 (1/2 倍，50% ) 。 图像大小会在 y 轴上减小 50% (1/2 的原始大小) 。

-   200，2x 缩放 (200% ) 。 图像大小沿 y 轴放大 200% (双) 。

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


[**WIA \_ IP \_ XSCALING**](wia-ips-xscaling.md)

 

 






