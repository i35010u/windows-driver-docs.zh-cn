---
title: WIA \_ IP \_ 页面 \_ 宽度
description: "\"WIA \\_ ip \\_ 页面 \\_ 宽度\" 属性包含所选当前页面的宽度（以英寸为单位的千分之几） ( 001) 。 WIA 微型驱动程序创建并维护此属性。"
keywords:
- WIA_IPS_PAGE_WIDTH 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PAGE_WIDTH
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: de21536cfee6af93299af07dfb99bc7611e8c85f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823131"
---
# <a name="wia_ips_page_width"></a>WIA \_ IP \_ 页面 \_ 宽度


"WIA \_ ip \_ 页面 \_ 宽度" 属性包含所选当前页面的宽度（以英寸为单位的千分之几） ( 001) 。 WIA 微型驱动程序创建并维护此属性。

属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

应用程序将读取 WIA \_ ip \_ 页面 \_ 宽度，以确定所扫描页面的物理尺寸。 如果范围设置不同于已知页面大小，则此属性会报告其 " [**wia \_ ip \_ 页面 \_ 大小**](wia-ips-page-size.md) " 属性设置为 "wia \_ 页面自定义" 的页面的宽度 \_ 。

WIA \_ ip \_ 页面 \_ 宽度必须与 WIA ips XEXTENT 的值同步 \_ \_ ，后者报告要扫描的页面的宽度（以像素为单位）。

**注意**   如果设备的子项目不支持属性，则 WIA 服务中的兼容性层不会将对 "WIA \_ ip 页面宽度" 属性的支持添加 \_ \_ 到从 Windows XP WIA 设备转换的 ADF 项。 应用程序不应期望 ADF 项始终支持 WIA \_ ip \_ 页 \_ 宽，并且应始终检查它是否在运行时受支持。  (通常情况下，应用程序应检查是否支持要协商的任何属性。 ) 

 

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
<td><p>在 Windows Vista 和更高版本的操作系统中可用。 对于 Windows XP，请改用 WIA_DPS_PAGE_WIDTH 属性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA \_ DPS \_ 页面 \_ 宽度**](wia-dps-page-width.md)

[**WIA \_ IP \_ 页面 \_ 高度**](wia-ips-page-height.md)

[**WIA \_ IP \_ 页面 \_ 大小**](wia-ips-page-size.md)

 

 






