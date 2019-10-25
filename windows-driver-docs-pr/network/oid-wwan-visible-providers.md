---
title: OID_WWAN_VISIBLE_PROVIDERS
description: OID_WWAN_VISIBLE_PROVIDERS 返回当前在 MB 设备范围内可见的网络提供程序列表。
ms.assetid: 4dfd4477-6332-4163-8b3e-a1604b11d175
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_VISIBLE_PROVIDERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b061f28de86d13b47b7c5c8d74d63f467de36507
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843764"
---
# <a name="oid_wwan_visible_providers"></a>OID\_WWAN\_可见\_提供程序


OID\_WWAN\_可见\_提供程序返回当前在 MB 设备范围内可见的网络提供程序列表。

不支持设置请求。

微型端口驱动程序必须异步处理查询请求，最初返回 NDIS\_状态\_指示\_需要请求原始请求，稍后发送[**ndis\_状态\_WWAN\_可见\_提供程序**](ndis-status-wwan-visible-providers.md)状态通知，包含[**NDIS\_WWAN\_可见\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)结构，以便在完成查询请求时提供有关可见网络提供程序的信息。

*查询*请求指定 NDIS\_WWAN\_获取\_可见\_提供程序结构作为输入。 当 WWAN\_获取\_可见\_提供程序的**操作**成员设置为 WWAN 时\_获取\_显示\_提供程序\_所有微型端口都应返回所有可见的提供程序。 当 WWAN\_获取\_可见\_提供程序的**操作**成员设置为 WWAN 时\_获取\_可见\_提供程序\_多，微型端口应只返回可见的多运营商提供程序，这些提供程序可设置为 home 提供程序。

设备返回的可见提供程序列表应为每个提供程序正确设置提供程序状态。 例如，应将多首选提供程序标记为 WWAN\_提供程序\_状态\_首选\_多，当前 home 提供程序（如果有任何标记为 WWAN\_提供程序\_状态\_HOME，当前已注册的提供程序（如果有）标记为 WWAN\_提供程序\_状态\_已注册。

WWAN\_PROVIDER2 结构的**Rssi**和**ErrorRate**成员应设置为（如果可用）。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN 提供程序操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-provider-operations)。

当处理查询操作时，微型端口驱动程序可以访问订阅服务器标识模块（SIM 卡），但不应访问提供程序网络。

微型端口驱动程序应将**VisibleListHeader**成员设置为*WwanStructProvider*。

对于基于 CDMA 的网络，如果首选漫游列表（PRL）中的任何网络当前可见，则微型端口驱动程序应该只返回 home 提供商。 对于基于 GSM 的网络，可见提供程序列表中可能会出现多个提供程序。

如果设备在连接时不支持对可见提供程序进行扫描，则应在 NDIS\_WWAN\_可见\_提供程序结构的**uStatus**成员中返回 WWAN\_状态\_繁忙错误值。

在注册模式下，基于 GSM 和 CDMA 的设备必须支持扫描可见提供程序。 但是，无需使用微型端口驱动程序来支持扫描可见提供程序，同时数据包数据协议（PDP）上下文处于活动状态（例如，设备已连接到提供商的网络）。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_WWAN\_可见\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)

[ **\_WWAN\_可见\_提供程序的 NDIS\_状态**](ndis-status-wwan-visible-providers.md)

[WWAN 提供程序操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-provider-operations)

 

 




