---
title: NDIS_STATUS_WWAN_PACKET_SERVICE
description: 当数据包服务可用性发生变化时，微型端口驱动程序使用 NDIS_STATUS_WWAN_PACKET_SERVICE 通知来通知 MB 服务，包括通知当前所使用的数据包数据服务类型的更改。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_PACKET_SERVICE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d1b879d9a1b06d4853af0faf5973eebaf812a930
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793437"
---
# <a name="ndis_status_wwan_packet_service"></a>NDIS \_ 状态 \_ WWAN \_ 数据包 \_ 服务


\_ \_ 当数据包服务可用性发生变化时，微型端口驱动程序使用 NDIS 状态 "WWAN \_ 数据包 \_ 服务通知" 通知 MB 服务，包括通知当前所使用的数据包数据服务类型的更改。

小型端口驱动程序还可以通过此通知发送未经请求的事件。

此通知使用 [**NDIS \_ WWAN \_ 数据包 \_ 服务 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state) 结构。

<a name="remarks"></a>备注
-------

如果没有资源分配/发布，基于 CDMA 的微型端口驱动程序可以自动启动包附加服务，并可以将事件通知发送到 MB 服务。

小型端口驱动程序应遵守事件通知的以下准则：

-   小型端口驱动程序 **AvailableDataClasses** \_ \_ \_ 在小型端口驱动程序初始化期间，应将 AvailableDataClasses 设置为 WWAN 数据类 NONE。 此后，每当 **AvailableDataClasses** 发生任何更改时，微型端口驱动程序都必须通知 MB 服务。

-   微型端口驱动程序初始化期间，微型端口驱动程序应将 **CurrentDataClass** 设置为 WWAN \_ 数据 \_ 类 \_ NONE。 此后，每当 **CurrentDataClass** 发生任何更改时，微型端口驱动程序都必须通知 MB 服务。 \_ \_ \_ 如果对 **CurrentDataClass** 的更改导致传输或接收链接速度发生变化，则微型端口驱动程序应发送 NDIS 状态链接状态通知。

-   当数据包服务附加状态发生任何变化时，微型端口驱动程序必须通知 MB 服务。

微型端口驱动程序应根据以下规则返回 *查询* 结果：

-   每当设备尝试建立数据包时，微型端口驱动程序都必须返回 \_ \_ 包含 **WwanPacketServiceStateAttaching** 的 WWAN 状态 SUCCESS。

-   \_ \_ 每次设备尝试进行数据包分离时，微型端口驱动程序都应将 WWAN 状态成功返回到 **WwanPacketServiceStateDetaching** 。

-   当设备处于最终状态时，微型端口驱动程序应同时返回 WWAN \_ 状态 \_ 成功以及适当的当前状态 ( **WwanPacketServiceStateAttached** 或 **WwanPacketServiceStateDetached**) 

-   微型端口驱动程序必须列出所有可用的数据类;不只是最高的可用数据类。 这同时适用于 *查询* 操作和事件通知。

微型端口驱动程序应根据以下规则返回 *设置* 的结果：

-   \_ \_ 如果使用 **WwanPacketServiceActionAttach***设置* 请求，则返回 WWAN 状态成功，该服务已在数据包附加状态下发出。

-   \_ \_ 如果使用 **WwanPacketServiceActionDetach***设置* 请求，则返回 WWAN 状态成功，该服务已在数据包分离状态下发出。

-   从不返回 *设置* 请求的暂时性状态。 只有在成功完成数据包服务操作并成功完成后，才必须返回最终状态 **WwanPacketServiceStateAttached** 或 **WwanPacketServiceStateDetached** \_ \_

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

## <a name="see-also"></a>请参阅


[**NDIS \_ WWAN \_ 数据包 \_ 服务 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state)

[OID \_ WWAN \_ 数据包 \_ 服务](oid-wwan-packet-service.md)

 

