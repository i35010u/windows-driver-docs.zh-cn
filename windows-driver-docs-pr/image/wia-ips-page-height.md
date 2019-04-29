---
title: WIA\_IPS\_页\_高度
description: WIA\_IPS\_页\_高度属性包含的高度，以英寸为单位的千分之几秒 (。 001)，当前所选页面。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: f8721f87-641c-4da8-ad3a-a38bf18d3111
keywords:
- WIA_IPS_PAGE_HEIGHT 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PAGE_HEIGHT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 572747fc78b38c0af4ea6c04d4166b0c3430eba1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353314"
---
# <a name="wiaipspageheight"></a>WIA\_IPS\_页\_高度


WIA\_IPS\_页\_高度属性包含的高度，以英寸为单位的千分之几秒 (。 001)，当前所选页面。 WIA 微型驱动程序创建并维护此属性。

属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_IPS\_页\_高度，以确定正在扫描的页的物理尺寸。 如果扩展盘区设置不同于已知的页面大小，此属性会将报告页面的高度其[ **WIA\_IPS\_页\_大小**](wia-ips-page-size.md)属性设置为 WIA\_页\_自定义。

WIA\_IPS\_页面\_高度必须提供英寸为单位，它等效于报告的像素值的千分之几秒的度量[ **WIA\_IP\_YEXTENT** ](wia-ips-yextent.md)，报告的高度，以像素为单位，页后，可以进行扫描。

**请注意**  WIA 服务中的兼容性层不会添加支持 WIA\_IP\_页\_高度属性设置为仅当从 Windows XP WIA 设备翻译的 ADF 项属性不支持的设备的子项目。 应用程序不应期望 ADF 项将始终支持 WIA\_IPS\_页\_高度和应始终检查它是否在运行时支持。 （应用程序应通常情况下检查此支持进行协商的任何属性。）

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 Windows Vista 和更高版本操作系统中可用。 对于 Windows XP 中，而是使用 WIA_DPS_PAGE_HEIGHT 属性。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_DPS\_PAGE\_HEIGHT**](wia-dps-page-height.md)

[**WIA\_IPS\_PAGE\_SIZE**](wia-ips-page-size.md)

[**WIA\_IPS\_PAGE\_WIDTH**](wia-ips-page-width.md)

[**WIA\_IPS\_YEXTENT**](wia-ips-yextent.md)

 

 






