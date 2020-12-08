---
title: WIA \_ DPS \_ 设备 \_ ID
description: WIA \_ DPS \_ 设备 \_ ID 属性包含 web 服务扫描仪设备的唯一函数实例标识符。
keywords:
- WIA_DPS_DEVICE_ID 图像设备
topic_type:
- apiref
api_name:
- WIA_DPS_DEVICE_ID
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fee0d82c6e14b1ecd4e46530f72425a2ad84d765
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820247"
---
# <a name="wia_dps_device_id"></a>WIA \_ DPS \_ 设备 \_ ID


WIA \_ DPS \_ 设备 \_ ID 属性包含 web 服务扫描仪设备的唯一函数实例标识符。 此标识符表示 WIA 微型驱动程序与之通信的扫描仪设备上的 web 服务。 不应建立有关此标识符的窗体的假设。 WIA 微型驱动程序创建并维护此属性。

WIA 应用程序可以使用 "WIA DPS 设备 ID" 的值， \_ \_ \_ 以使用函数发现 API （表示当前 WIA 会话中使用的 web 服务扫描仪设备的函数实例对象）查找。

属性类型： VT \_ BSTR

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

WIA 微型驱动程序通过 \_ \_ 从函数实例对象读取 PKEY PNPX ID 设备属性，在运行时初始化此属性。

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

## <a name="see-also"></a>请参阅


[**WIA \_ DPS \_ 全局 \_ 标识**](wia-dps-global-identity.md)

[**WIA \_ DPS \_ 服务 \_ ID**](wia-dps-service-id.md)

 

 






