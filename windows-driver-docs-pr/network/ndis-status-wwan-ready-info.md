---
title: NDIS_STATUS_WWAN_READY_INFO
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_READY_INFO 通知来告知设备已准备状态发生变化以响应 OID_WWAN_READY_INFO MB 服务 \ 160; 查询请求。
ms.assetid: 92ddf95f-8829-4259-b53a-c7ce56ee53f0
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_READY_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cb93eb3d2b2974d7fabe9a40c50ae90c237c609e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520620"
---
# <a name="ndisstatuswwanreadyinfo"></a>NDIS\_状态\_WWAN\_准备\_信息


微型端口驱动程序使用 NDIS\_状态\_WWAN\_准备\_信息通知来通知设备就绪状态发生变化以响应 MB 服务[OID\_WWAN\_准备好\_INFO](oid-wwan-ready-info.md) 查询请求。

微型端口驱动程序还可以发送未经请求的事件与该通知。

使用此通知[ **NDIS\_WWAN\_准备\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567916)结构。

<a name="remarks"></a>备注
-------

微型端口驱动程序必须报告所有设备就绪状态更改为未经请求的事件。 微型端口驱动程序微型端口驱动程序初始化时 MB 设备，必须设置 WWAN\_准备好\_信息**ReadyState**成员添加到**WwanReadyStateOff**。 此后，微型端口驱动程序必须向通过此通知 MB 服务报告的任何设备就绪状态更改。 例如，微型端口驱动程序必须报告设备的就绪状态更改时**ReadyState**从更改成员**WwanReadyStateOff**到**WwanReadyStateDeviceLocked**，或**WwanReadyStateBadSim**，或**WwanReadyStateSimNotInserted**，或任何其他不同的设备就绪状态。

大多数设备就绪状态更改发生时设备初始化单选堆栈和 SIM 卡 （如果需要）。 更改可以 MB 服务之间的微型端口驱动程序，例如更改 SIM 卡的用户会话期间也会发生。 MB 服务的行为应更改相应地基于新设备就绪的状态。

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
<td><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_WWAN\_READY\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff567916)

[OID\_WWAN\_READY\_INFO](oid-wwan-ready-info.md)

 

 




