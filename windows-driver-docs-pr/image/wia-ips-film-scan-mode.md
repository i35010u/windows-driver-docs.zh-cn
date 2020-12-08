---
title: WIA \_ IPS \_ 胶片 \_ 扫描 \_ 模式
description: "\"WIA \\_ IPS \\_ 胶片 \\_ 扫描 \\_ 模式\" 属性包含当前的电影扫描配置设置。 WIA 微型驱动程序创建并维护此属性。"
keywords:
- WIA_IPS_FILM_SCAN_MODE 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_FILM_SCAN_MODE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d87d7508c7efdd874f84271be05f9ab42d9bde75
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825983"
---
# <a name="wia_ips_film_scan_mode"></a>WIA \_ IPS \_ 胶片 \_ 扫描 \_ 模式


"WIA \_ IPS \_ 胶片 \_ 扫描 \_ 模式" 属性包含当前的电影扫描配置设置。 WIA 微型驱动程序创建并维护此属性。

属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了在 WIA \_ IPS \_ 胶片 \_ 扫描 \_ 模式属性中有效的常量

| 扫描类型                  | 定义                                         |
|----------------------------|----------------------------------------------------|
| WIA \_ 胶卷 \_ 彩色 \_ 幻灯片    | 扫描将是一种颜色扫描。                     |
| WIA \_ 胶片 \_ 颜色 \_ 负数 | 扫描将为负值的颜色扫描。       |
| WIA \_ 胶片 \_ BW \_ 负数    | 扫描将为黑色、白色 (灰度) 扫描。 |

 

胶片扫描器和透明度适配器的 WIA 项树中的根项需要此属性。

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

 

 





