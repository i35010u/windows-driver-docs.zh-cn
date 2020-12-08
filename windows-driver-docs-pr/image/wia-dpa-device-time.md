---
title: WIA \_ DPA \_ 设备 \_ 时间
description: WIA \_ DPA \_ 设备 \_ 时间属性包含设备上存储的当前时钟时间。 微型驱动程序创建并维护此属性。
keywords:
- WIA_DPA_DEVICE_TIME 图像设备
topic_type:
- apiref
api_name:
- WIA_DPA_DEVICE_TIME
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b69f67a9c1b900ebe9b73749c0312939f287fc8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808735"
---
# <a name="wia_dpa_device_time"></a>WIA \_ DPA \_ 设备 \_ 时间


WIA \_ DPA \_ 设备 \_ 时间属性包含设备上存储的当前时钟时间。 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_dpa_device_time_si"></span><span id="DDK_WIA_DPA_DEVICE_TIME_SI"></span>


属性类型： VT \_ UI2 |VT \_ 矢量

有效值： WIA " \_ \_ 无"

访问权限：读/写或只读

<a name="remarks"></a>备注
-------

\_读取 WIA DPA \_ 设备 \_ 时间属性时，微型驱动程序应检查设备的当前时钟时间，并始终返回当前时间。 只有具有内部时钟的设备才支持该属性。 如果可以设置设备时钟，则此属性是可读/写的;否则为只读。 WIA 设备报告 SYSTEMTIME 结构中的时间 (这在 Microsoft Windows SDK 文档) 中进行了介绍。

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
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





