---
title: NDIS_STATUS_WWAN_PACKET_SERVICE
description: 当数据包服务可用性发生变化时，微型端口驱动程序使用 NDIS_STATUS_WWAN_PACKET_SERVICE 通知来通知 MB 服务，包括通知当前所使用的数据包数据服务类型的更改。
ms.assetid: 7a04b54e-e07b-43dc-ba76-086d7521ff60
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_PACKET_SERVICE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e12f5906cfad6030b88cd5615e289c6e19531597
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844759"
---
# <a name="ndis_status_wwan_packet_service"></a>WWAN\_数据包\_服务\_的 NDIS\_状态


小型端口驱动程序使用 NDIS\_状态\_WWAN\_数据包\_服务通知，以在数据包服务可用性发生更改时通知 MB 服务，包括通知当前所使用的数据包数据服务的类型发生更改。

小型端口驱动程序还可以通过此通知发送未经请求的事件。

此通知使用[**NDIS\_WWAN\_数据包\_服务\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state)结构。

<a name="remarks"></a>备注
-------

如果没有资源分配/发布，基于 CDMA 的微型端口驱动程序可以自动启动包附加服务，并可以将事件通知发送到 MB 服务。

小型端口驱动程序应遵守事件通知的以下准则：

-   小型端口驱动程序应将**AvailableDataClasses**设置为 WWAN\_数据\_类在微型端口驱动程序初始化期间\_NONE。 此后，每当**AvailableDataClasses**发生任何更改时，微型端口驱动程序都必须通知 MB 服务。

-   小型端口驱动程序应在微型端口驱动程序初始化过程中将**CurrentDataClass**设置为 WWAN\_数据\_类\_NONE。 此后，每当**CurrentDataClass**发生任何更改时，微型端口驱动程序都必须通知 MB 服务。 如果更改**CurrentDataClass**导致传输或接收链接速度发生变化，微型端口驱动程序应将 NDIS\_状态\_链接\_状态通知。

-   当数据包服务附加状态发生任何变化时，微型端口驱动程序必须通知 MB 服务。

微型端口驱动程序应根据以下规则返回*查询*结果：

-   每当设备尝试建立数据包时，微型端口驱动程序都必须返回 WWAN\_状态\_SUCCESS，并返回**WwanPacketServiceStateAttaching** 。

-   每当设备尝试进行数据包**分离时，** 微型端口驱动程序都应\_SUCCESS 返回 WWAN\_状态。

-   当设备处于最终状态时，微型端口驱动程序应将 WWAN\_状态连同适当的当前状态一起返回\_SUCCESS （ **WwanPacketServiceStateAttached**或**WwanPacketServiceStateDetached**）

-   微型端口驱动程序必须列出所有可用的数据类;不只是最高的可用数据类。 这同时适用于*查询*操作和事件通知。

微型端口驱动程序应根据以下规则返回*设置*的结果：

-   如果使用**WwanPacketServiceActionAttach***设置*请求，则返回 WWAN\_状态\_成功，该服务已在数据包附加状态下发出。

-   如果使用**WwanPacketServiceActionDetach***设置*请求，则返回 WWAN\_状态\_成功，该服务已在数据包分离状态下发出。

-   从不返回*设置*请求的暂时性状态。 只有在成功完成数据包服务操作和 WWAN\_状态\_成功后，才能返回最终状态**WwanPacketServiceStateAttached**或**WwanPacketServiceStateDetached**

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


[**NDIS\_WWAN\_数据包\_服务\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state)

[OID\_WWAN\_数据包\_服务](oid-wwan-packet-service.md)

 

 




