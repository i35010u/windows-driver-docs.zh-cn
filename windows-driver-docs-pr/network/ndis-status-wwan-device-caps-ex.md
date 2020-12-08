---
title: NDIS_STATUS_WWAN_DEVICE_CAPS_EX
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_CAPS_EX 通知来通知 MB 服务完成了上一个 OID_WWAN_DEVICE_CAPS_EX 查询请求。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_DEVICE_CAPS_EX 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 65f321801c6e366b76a22c76f8c06fb6dd152d25
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841171"
---
# <a name="ndis_status_wwan_device_caps_ex"></a>NDIS \_ 状态 \_ WWAN \_ 设备 \_ CAP \_ EX


微型端口驱动程序使用 **NDIS \_ 状态 \_ WWAN \_ 设备 \_ CAP \_ ex** 通知来通知 MB 服务完成了上一个 [OID \_ WWAN \_ 设备 \_ cap \_ ex](./oid-wwan-device-caps-ex.md) 查询请求。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用 [**NDIS \_ WWAN \_ 设备 \_ cap \_ EX**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps_ex) 结构。

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
<td><p>Windows 10 版本 1703</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID \_ WWAN \_ 设备 \_ CAP \_ EX](./oid-wwan-device-caps-ex.md)

[**NDIS \_ WWAN \_ 设备 \_ CAP \_ EX**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps_ex)

 

