---
title: OID_WWAN_PREFERRED_PROVIDERS
description: OID_WWAN_PREFERRED_PROVIDERS 返回信息的首选提供程序的基于 GSM 的设备的列表。
ms.assetid: fa70f1ac-5b14-44f8-a2c4-d2163fe81c5a
ms.date: 08/08/2017
keywords: -OID_WWAN_PREFERRED_PROVIDERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 10678081206be6ec9d1a53bcba787fddc1675109
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521109"
---
# <a name="oidwwanpreferredproviders"></a>OID\_WWAN\_首选\_提供程序


OID\_WWAN\_首选\_提供程序返回的列表信息的首选提供程序的基于 GSM 的设备。 基于 CDMA 的设备的微型端口驱动程序不需要支持此 OID。

微型端口驱动程序必须处理集和查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_PREFERRED\_提供程序**](ndis-status-wwan-preferred-providers.md)状态通知包含[ **NDIS\_WWAN\_首选\_提供程序**](https://msdn.microsoft.com/library/windows/hardware/ff567913)结构，以便提供而不考虑完成设置首选提供程序列表 (PPL) 有关的信息或查询请求。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN 提供程序操作](https://msdn.microsoft.com/library/windows/hardware/ff559101)。

微型端口驱动程序可以访问用户识别模块 （SIM 卡） 当处理查询请求，但不是应访问提供程序网络。

微型端口驱动程序可以访问用户识别模块 （SIM 卡） 或提供程序网络，处理时设置的请求。

处理 OID 时\_WWAN\_PREFERRED\_提供程序，微型端口驱动程序可能会将设置仅 WWAN\_提供程序\_状态\_首选或 WWAN\_提供程序\_状态\_禁止访问标志来标记的列表项。 请注意，已禁止的提供程序可能不会显示在列表中为基于 GSM 的设备。

应设置微型端口 driverrs **PreferredListHeader.ElementType**成员添加到*WwanStructProvider*。 微型端口驱动程序应设置**PreferredListHeader.ElementCount**成员为 0 时响应 OID\_WWAN\_首选\_提供程序将设置请求。

是否可以覆盖在设备上的 PPL 或未设置时处理请求取决于设备功能、 移动电话技术，和/或网络提供程序的策略。

微型端口驱动程序应返回 NDIS\_状态\_不\_如果它们不支持返回或设置 PPL 支持。

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
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_WWAN\_PREFERRED\_PROVIDERS**](https://msdn.microsoft.com/library/windows/hardware/ff567913)

[**NDIS\_STATUS\_WWAN\_PREFERRED\_PROVIDERS**](ndis-status-wwan-preferred-providers.md)

[WWAN 提供程序操作](https://msdn.microsoft.com/library/windows/hardware/ff559101)

 

 




