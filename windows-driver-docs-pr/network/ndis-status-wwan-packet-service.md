---
title: NDIS_STATUS_WWAN_PACKET_SERVICE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_PACKET_SERVICE 通知来告知 MB 服务数据包服务可用性的更改，包括要通知的当前使用的数据包数据服务的类型的更改时。
ms.assetid: 7a04b54e-e07b-43dc-ba76-086d7521ff60
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_PACKET_SERVICE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1cbbe32663674087b7e50ff607c01860efc55ab4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569415"
---
# <a name="ndisstatuswwanpacketservice"></a>NDIS\_状态\_WWAN\_数据包\_服务


微型端口驱动程序使用 NDIS\_状态\_WWAN\_数据包\_服务通知来通知 MB 服务数据包服务可用性的更改，包括要通知的数据包数据的类型的更改时当前使用的服务。

微型端口驱动程序还可以发送未经请求的事件与该通知。

使用此通知[ **NDIS\_WWAN\_数据包\_服务\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567910)结构。

<a name="remarks"></a>备注
-------

基于 CDMA 的微型端口驱动程序可以自动启动数据包附加服务是否存在任何资源分配/发布可能并可以向 MB 服务发送事件通知。

微型端口驱动程序应遵循以下准则的事件通知：

-   微型端口驱动程序应设置**AvailableDataClasses**设置为 WWAN\_数据\_类\_微型端口驱动程序初始化期间 NONE。 此后，微型端口驱动程序必须通知 MB 服务时没有任何更改**AvailableDataClasses**。

-   微型端口驱动程序应设置**CurrentDataClass**到 WWAN\_数据\_类\_微型端口驱动程序初始化期间 NONE。 此后，微型端口驱动程序必须通知 MB 服务时没有任何更改**CurrentDataClass** 。 微型端口驱动程序应发送 NDIS\_状态\_链接\_状态通知，如果对更改**CurrentDataClass**导致的更改的传输或接收链接速度。

-   微型端口驱动程序必须通知 MB 服务，只要有数据包服务中的任何更改将附加状态。

微型端口驱动程序应返回*查询*结果根据以下规则：

-   微型端口驱动程序必须返回 WWAN\_状态\_成功**WwanPacketServiceStateAttaching**每当设备尝试将数据包附加。

-   微型端口驱动程序应返回 WWAN\_状态\_成功**WwanPacketServiceStateDetaching**每当设备尝试数据包分离。

-   当设备处于最终状态时，微型端口驱动程序应返回 WWAN\_状态\_成功以及相应的当前状态 ( **WwanPacketServiceStateAttached**或**WwanPacketServiceStateDetached**)

-   微型端口驱动程序必须列出所有可用数据的类;不只是最高的数据的类可用。 这同时适用于*查询*操作以及事件通知。

微型端口驱动程序应返回*设置*结果根据以下规则：

-   返回 WWAN\_状态\_成功后，如果*设置*请求**WwanPacketServiceActionAttach**，由服务颁发和设备已处于数据包附加状态。

-   返回 WWAN\_状态\_成功后，如果*设置*请求**WwanPacketServiceActionDetach**，由服务颁发和设备已处于数据包分离状态。

-   永远不会返回暂时性状态*设置*请求。 只有最终状态**WwanPacketServiceStateAttached**或**WwanPacketServiceStateDetached**必须具有 WWAN的数据包服务操作的成功完成后返回\_状态\_成功

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
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_WWAN\_数据包\_服务\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567910)

[OID\_WWAN\_PACKET\_SERVICE](oid-wwan-packet-service.md)

 

 




