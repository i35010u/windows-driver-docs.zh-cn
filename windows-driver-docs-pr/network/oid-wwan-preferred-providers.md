---
title: OID_WWAN_PREFERRED_PROVIDERS
description: OID_WWAN_PREFERRED_PROVIDERS 返回有关基于 GSM 的设备的首选提供程序列表的信息。
ms.assetid: fa70f1ac-5b14-44f8-a2c4-d2163fe81c5a
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_PREFERRED_PROVIDERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4bafac81046a5e112ef8f7814d645b8d1f99de4b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843809"
---
# <a name="oid_wwan_preferred_providers"></a>OID\_WWAN\_首选\_提供程序


OID\_WWAN\_首选\_提供程序返回有关基于 GSM 的设备的首选提供程序列表的信息。 基于 CDMA 的设备的微型端口驱动程序无需支持此 OID。

微型端口驱动程序必须异步处理集和查询请求，最初返回 NDIS\_状态\_指示\_需要原始请求，稍后发送[**ndis\_状态\_WWAN\_首选\_提供程序**](ndis-status-wwan-preferred-providers.md)状态通知，其中包含一个[**NDIS\_WWAN\_首选\_提供**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers)程序结构，以便提供有关首选提供程序列表（PPL）的信息，而不考虑完成的集合或查询请求。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN 提供程序操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-provider-operations)。

小型端口驱动程序可以在处理查询请求时访问订阅服务器标识模块（SIM 卡），但不应访问提供程序网络。

当处理设置请求时，微型端口驱动程序可以访问订阅服务器标识模块（SIM 卡）或提供程序网络。

当处理 OID\_WWAN\_首选\_提供程序时，微型端口驱动程序只能将 WWAN\_提供程序设置\_\_\_\_禁止标志来标记列表的状态\_日志. 请注意，对于基于 GSM 的设备，禁止的访问接口可能不会出现在列表中。

微型端口 driverrs 应将**PreferredListHeader**成员设置为*WwanStructProvider*。 \_WWAN\_首选\_提供程序设置请求时，微型端口驱动程序应将 Elementcount 多于成员设置为 0 **。**

处理设置请求时是否可以覆盖设备上的 PPL 取决于设备功能、移动电话技术和/或网络提供商的策略。

如果不支持返回或设置 PPL，微型端口驱动程序应返回 NDIS\_状态\_不\_支持。

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


[**NDIS\_WWAN\_首选\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers)

[ **\_WWAN\_首选\_提供程序的 NDIS\_状态**](ndis-status-wwan-preferred-providers.md)

[WWAN 提供程序操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-provider-operations)

 

 




