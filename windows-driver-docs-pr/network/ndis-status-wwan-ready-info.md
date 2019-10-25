---
title: NDIS_STATUS_WWAN_READY_INFO
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_READY_INFO 通知来通知 MB 服务设备就绪状态更改，以响应 OID_WWAN_READY_INFO \ 160; 查询请求。
ms.assetid: 92ddf95f-8829-4259-b53a-c7ce56ee53f0
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_READY_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a8ac58f7e0c8680c9ec0a9fe6c34b30a15c503b8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844652"
---
# <a name="ndis_status_wwan_ready_info"></a>NDIS\_状态\_WWAN\_就绪\_信息


微型端口驱动程序使用 NDIS\_状态\_WWAN\_准备就绪的\_信息通知，通知 MB 服务设备就绪状态更改，以响应[OID\_WWAN\_就绪\_INFO](oid-wwan-ready-info.md) 查询请求。

小型端口驱动程序还可以通过此通知发送未经请求的事件。

此通知使用[**NDIS\_WWAN\_就绪\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ready_info)结构。

<a name="remarks"></a>备注
-------

微型端口驱动程序必须将所有设备就绪状态更改报告为一个未经请求的事件。 当微型端口驱动程序初始化 MB 设备时，微型端口驱动程序必须将 WWAN\_READY\_INFO **ReadyState**成员设置为**WwanReadyStateOff**。 此后，小型端口驱动程序必须通过此通知向 MB 服务报告任何设备就绪状态更改。 例如，微型端口驱动程序必须在**ReadyState**成员从**WwanReadyStateOff**更改为**WwanReadyStateDeviceLocked**或**WwanReadyStateBadSim**时报告设备就绪状态更改，或**WwanReadyStateSimNotInserted**或任何其他不同设备就绪状态。

如果设备初始化无线电堆栈和 SIM 卡（如果需要），则大多数设备就绪状态发生更改。 在 MB 服务和微型端口驱动程序之间的会话过程中，还会发生更改，例如用户更改 SIM 卡。 MB 服务的行为应根据新设备就绪状态进行相应的更改。

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
<td><p>在 windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_WWAN\_准备好\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ready_info)

[OID\_WWAN\_就绪\_信息](oid-wwan-ready-info.md)

 

 




