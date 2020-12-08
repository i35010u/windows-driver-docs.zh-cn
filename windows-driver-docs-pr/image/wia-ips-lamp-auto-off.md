---
title: WIA \_ IPS \_ 灯 \_ 自动 \_ 关闭
description: "\"WIA \\_ ip \\_ 灯 \\_ 自动 \\_ 关闭\" 属性包含用于自动关闭扫描仪灯泡的当前配置设置。 WIA 微型驱动程序创建并维护此属性。"
keywords:
- WIA_IPS_LAMP_AUTO_OFF 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_LAMP_AUTO_OFF
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb040928eca8987a96748b67f88e2f026b4031b5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825975"
---
# <a name="wia_ips_lamp_auto_off"></a>WIA \_ IPS \_ 灯 \_ 自动 \_ 关闭


"WIA \_ ip \_ 灯 \_ 自动 \_ 关闭" 属性包含用于自动关闭扫描仪灯泡的当前配置设置。 WIA 微型驱动程序创建并维护此属性。

属性类型： VT \_ UI4

有效值： WIA 内容 \_ \_ 范围

访问权限：读/写

<a name="remarks"></a>备注
-------

使用 "WIA \_ IPS \_ 灯泡 \_ 自动关闭" 属性，可以以 \_ 编程方式控制在扫描仪未使用时要将其保留的时间; 此灯可能是透明适配器的专用灯具 () 或专用胶片扫描器) 的主要扫描仪灯泡 (。

\_ \_ \_ \_ 仅当设备支持自动灯泡功能时，才应实现 WIA IPS 灯自动关闭。

WIA \_ ip \_ 灯自动关闭的有效值 \_ \_ 范围为0到4095秒。

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

 

 





