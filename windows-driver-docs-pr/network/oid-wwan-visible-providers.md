---
title: OID_WWAN_VISIBLE_PROVIDERS
description: OID_WWAN_VISIBLE_PROVIDERS 返回当前在 MB 设备的范围内可见的网络提供商列表。
ms.assetid: 4dfd4477-6332-4163-8b3e-a1604b11d175
ms.date: 08/08/2017
keywords: -OID_WWAN_VISIBLE_PROVIDERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c89393ed05e71b34bc042167077da386607d814d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566103"
---
# <a name="oidwwanvisibleproviders"></a>OID\_WWAN\_VISIBLE\_提供程序


OID\_WWAN\_VISIBLE\_提供程序返回一系列网络提供商的 MB 设备的范围内当前可见。

不支持组的请求。

微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_VISIBLE\_提供程序**](ndis-status-wwan-visible-providers.md)状态通知包含[ **NDIS\_WWAN\_可见\_提供程序**](https://msdn.microsoft.com/library/windows/hardware/ff567948)结构，以完成查询请求时提供可见的网络提供程序的信息。

*查询*请求指定 NDIS\_WWAN\_获取\_VISIBLE\_作为输入提供程序结构。 当**操作**WWAN 中的成员\_获取\_VISIBLE\_提供程序设置为 WWAN\_获取\_VISIBLE\_提供程序\_所有微型端口应返回所有可见的提供程序。 当**操作**WWAN 中的成员\_获取\_VISIBLE\_提供程序设置为 WWAN\_获取\_VISIBLE\_提供程序\_多运营商微型端口应仅返回可以为家庭的提供程序设置的可见多运营商提供程序。

按设备应该提供程序的状态将设置正确的提供程序的每个返回可见的提供程序列表。 例如，多首选提供程序应标记为 WWAN\_提供程序\_状态\_PREFERRED\_多，当前主提供程序如果任何应标记为 WWAN\_提供程序\_状态\_主页，当前已注册的提供程序如果任何应标记为 WWAN\_提供程序\_状态\_已注册。

**Rssi**并**ErrorRate** WWAN 成员\_如果可用，应设置 PROVIDER2 结构。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN 提供程序操作](https://msdn.microsoft.com/library/windows/hardware/ff559101)。

微型端口驱动程序可以访问用户识别模块 （SIM 卡） 当处理查询操作，但不是应访问提供程序网络。

微型端口驱动程序应设置**VisibleListHeader.ElementType**成员添加到*WwanStructProvider*。

基于 CDMA 的网络，微型端口驱动程序应返回当前可见的任何网络中首选的漫游列表 (PRL) 是否仅家用供应商。 为基于 GSM 的网络，多个提供程序可能会出现在列表中可见的提供程序。

设备不支持扫描连接时可见的提供程序应返回 WWAN\_状态\_中的正忙错误值**uStatus** NDIS 成员\_WWAN\_可见\_提供程序结构。

同时基于 GSM 的和基于 CDMA 的设备必须支持扫描在已注册的模式中可见的提供程序。 但是，微型端口驱动程序不支持所需的数据包数据协议 (PDP) 上下文处于活动状态时扫描可见的提供程序 （例如，设备连接到提供程序的网络）。

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
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_WWAN\_VISIBLE\_提供程序**](https://msdn.microsoft.com/library/windows/hardware/ff567948)

[**NDIS\_状态\_WWAN\_VISIBLE\_提供程序**](ndis-status-wwan-visible-providers.md)

[WWAN 提供程序操作](https://msdn.microsoft.com/library/windows/hardware/ff559101)

 

 




