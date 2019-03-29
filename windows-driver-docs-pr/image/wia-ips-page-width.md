---
title: WIA\_IPS\_页\_宽度
description: WIA\_IPS\_页\_宽度属性包含选定英寸为单位的千分之几秒中的当前页的宽度 (。 001)。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: b72d32bf-6f1b-4eb2-8f7c-f0de4e2caf26
keywords:
- WIA_IPS_PAGE_WIDTH 成像设备
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
ms.openlocfilehash: 15d587ea9ab9ff4985d8004e4024044999a77a3d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569529"
---
# <a name="wiaipspagewidth"></a>WIA\_IPS\_页\_宽度


WIA\_IPS\_页\_宽度属性包含选定英寸为单位的千分之几秒中的当前页的宽度 (。 001)。 WIA 微型驱动程序创建并维护此属性。

属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_IPS\_页\_宽度，以确定物理尺寸为正在扫描的页。 如果扩展盘区设置不同于已知的页面大小，此属性会将报告页的宽度其[ **WIA\_IPS\_页\_大小**](wia-ips-page-size.md)属性设置为WIA\_页\_自定义。

WIA\_IPS\_页面\_宽度必须是 WIA 的值与同步\_IP\_大 XEXTENT，报告的宽度，以像素为单位的页进行扫描。

**请注意**   WIA 服务中的兼容性层不会添加支持 WIA\_IP\_页\_宽度属性设置为仅当从 Windows XP WIA 设备翻译的 ADF 项属性不支持的设备的子项目。 应用程序不应期望 ADF 项始终支持 WIA\_IPS\_页\_宽度和应始终检查它是否在运行时支持。 （通常情况下，应用程序应检查任何属性，以进行协商的支持。）

 

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
<td><p>在 Windows Vista 和更高版本操作系统中可用。 对于 Windows XP 中，而是使用 WIA_DPS_PAGE_WIDTH 属性。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_DPS\_PAGE\_WIDTH**](wia-dps-page-width.md)

[**WIA\_IPS\_PAGE\_HEIGHT**](wia-ips-page-height.md)

[**WIA\_IPS\_PAGE\_SIZE**](wia-ips-page-size.md)

 

 






