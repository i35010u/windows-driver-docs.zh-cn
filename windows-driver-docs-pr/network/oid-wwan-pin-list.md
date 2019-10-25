---
title: OID_WWAN_PIN_LIST
description: OID_WWAN_PIN_LIST 返回 MB 设备支持的所有不同类型的个人标识号（Pin）的列表，以及每种 PIN 类型的其他详细信息，例如 PIN 长度（最小长度和最大长度）、PIN 格式、PIN 输入模式（启用/禁用/不可用）。 此 OID 还指定设备支持的每个 PIN 的当前模式。 不支持设置请求。 微型端口驱动程序必须异步处理查询请求，最初将 NDIS_STATUS_INDICATION_REQUIRED 返回到原始请求，稍后将包含 NDIS_WWAN_PIN_LIST 结构的 NDIS_STATUS_WWAN_PIN_LIST 状态通知发送到完成查询请求时，返回具有相应说明的 Pin 列表。
ms.assetid: 76a1181c-974e-472d-ad15-d9c6208aa2b4
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_PIN_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5f4c28923eee706ea830ac1e2f65ceed667255d5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843816"
---
# <a name="oid_wwan_pin_list"></a>OID\_WWAN\_固定\_列表


OID\_WWAN\_PIN\_列表返回 MB 设备支持的所有不同类型的个人标识号（Pin）的列表，以及每种 PIN 类型的其他详细信息，例如 PIN 长度（最小和最大长度）、PIN 格式、PIN 输入模式（启用/禁用/不可用）。 此 OID 还指定设备支持的每个 PIN 的当前模式。

不支持设置请求。

微型端口驱动程序必须异步处理查询请求，最初返回 NDIS\_状态\_指示\_需要请求原始请求，稍后再发送[**ndis\_状态\_WWAN\_PIN\_列出**](ndis-status-wwan-pin-list.md)状态通知，其中包含一个[**NDIS\_WWAN\_PIN\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list)结构，以便在完成查询请求时返回具有相应说明的 pin 列表。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN Pin 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-pin-operations)。

当处理查询操作时，微型端口驱动程序可以访问订阅服务器标识模块（SIM 卡），但不应访问提供程序网络。

微型端口驱动程序必须报告其设备支持的所有 Pin。 如果设备不支持列出 Pin，微型端口驱动程序必须从在微型端口驱动程序中为其支持的所有设备维护的静态（硬编码）列表中报告此列表。

任何提供设备电源验证或标识功能的 PIN 都应报告为 PIN1，并且必须符合 PIN1 指导原则。

当设备就绪状态更改为*WwanReadyStateInitialized*或设备就绪状态为*WwanReadyStateDeviceLocked* （PIN 锁定）时，微型端口驱动程序必须返回此信息。 小型端口驱动程序还应尽可能将此信息返回到其他设备就绪状态。

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


[**NDIS\_WWAN\_固定\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list)

[ **\_WWAN\_PIN\_列表的 NDIS\_状态**](ndis-status-wwan-pin-list.md)

[WWAN Pin 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-pin-operations)

 

 




