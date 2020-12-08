---
title: WIA \_ IP \_ XSCALING
description: WIA \_ IPS \_ XSCALING 属性指示是否应将 x 轴上的缩放应用于扫描。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_XSCALING 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_XSCALING
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95e4b4a907aeb8054ddf5f7797db0b14e6889243
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838281"
---
# <a name="wia_ips_xscaling"></a>WIA \_ IP \_ XSCALING


WIA \_ IPS \_ XSCALING 属性指示是否应将 x 轴上的缩放应用于扫描。 WIA 微型驱动程序创建并维护此属性。

属性类型： VT \_ I4

有效值： WIA "内容范围" 或 "WIA 内容" \_ \_ \_ \_ 列表

访问权限：读/写或只读

<a name="remarks"></a>备注
-------

WIA \_ IPS XSCALING 属性的有效值 \_ 范围为1到65535。

WIA \_ ip \_ XSCALING 指示仅沿 x 轴缩放。 若要统一缩放图像，必须在 WIA \_ ips \_ XSCALING 和 [**wia \_ ips \_ YSCALING**](wia-ips-yscaling.md) 属性中设置类似值。

请开考虑以下示例：

-   100，无 (1x，100% ) 缩放。 不会更改图像。

-   050，1/2 缩放 (1/2 倍，50% ) 。 图像大小将沿 x 轴减小 50% (1/2 的原始大小) 。

-   200，2x 缩放 (200% ) 。 图像大小沿 x 轴放大 200% (双) 。

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


[**WIA \_ IP \_ YSCALING**](wia-ips-yscaling.md)

 

 






