---
title: NDIS_STATUS_WWAN_DEVICE_CAPS_EX
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_CAPS_EX 通知来告知 MB 服务关于完成的上一个 OID_WWAN_DEVICE_CAPS_EX 查询请求。
ms.assetid: 7E596CB0-2A08-45E4-9932-5E951B880D62
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_DEVICE_CAPS_EX 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d3eda6be7161a70346333d55c24923f213edb9f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520038"
---
# <a name="ndisstatuswwandevicecapsex"></a>NDIS\_STATUS\_WWAN\_DEVICE\_CAPS\_EX


微型端口驱动程序使用**NDIS\_状态\_WWAN\_设备\_CAPS\_EX**通知来通知关于完成的上一MB服务[OID\_WWAN\_设备\_CAP\_EX](https://msdn.microsoft.com/library/windows/hardware/mt799830)查询请求。

微型端口驱动程序不能使用此通知将发送未经请求的事件。

使用此通知[ **NDIS\_WWAN\_设备\_CAPS\_EX** ](https://msdn.microsoft.com/library/windows/hardware/mt782401)结构。

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
<td><p>Windows 10，版本 1703</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID\_WWAN\_DEVICE\_CAPS\_EX](https://msdn.microsoft.com/library/windows/hardware/mt799830)

[**NDIS\_WWAN\_DEVICE\_CAPS\_EX**](https://msdn.microsoft.com/library/windows/hardware/mt782401)

 

 




