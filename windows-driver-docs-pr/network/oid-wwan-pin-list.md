---
title: OID_WWAN_PIN_LIST
description: OID_WWAN_PIN_LIST 返回所有不同类型的个人标识号 (Pin) 支持的 MB 设备的列表以及其他详细信息，对于每个插针类型，例如 PIN （最小和最大长度），PIN 格式 PIN 输入模式的长度（已启用/禁用/不可用）。 此 OID 还指定设备支持的每个 PIN 的当前模式。 不支持组的请求。 微型端口驱动程序必须查询请求进行异步处理，最初将 NDIS_STATUS_INDICATION_REQUIRED 恢复到原始请求，并更高版本将发送一封包含到 NDIS_WWAN_PIN_LIST 结构 NDIS_STATUS_WWAN_PIN_LIST 状态通知完成查询请求时，则返回与相应说明的图钉列表。
ms.assetid: 76a1181c-974e-472d-ad15-d9c6208aa2b4
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_PIN_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4ff9595dfb399a370d3c976febb8440cc20c9a45
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360765"
---
# <a name="oidwwanpinlist"></a>OID\_WWAN\_PIN\_LIST


OID\_WWAN\_PIN\_列表返回所有不同类型的个人标识号 (Pin) 支持的 MB 设备的列表以及其他详细信息，对于每个插针类型，例如 PIN 的长度 (最小和最大长度），PIN 格式，PIN 输入模式 （启用/禁用/不可用）。 此 OID 还指定设备支持的每个 PIN 的当前模式。

不支持组的请求。

微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_PIN\_列表**](ndis-status-wwan-pin-list.md)状态通知包含[ **NDIS\_WWAN\_PIN\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list)结构，以完成查询请求时返回的 Pin 与相应说明的列表。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN Pin 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-pin-operations)。

微型端口驱动程序可以访问用户识别模块 （SIM 卡） 当处理查询操作，但不是应访问提供程序网络。

微型端口驱动程序必须报告其设备支持的所有球瓶。 如果设备不支持列出的 Pin，微型端口驱动程序必须报告静态 （硬编码） 列表中的微型端口驱动程序本身支持的所有设备维护此列表。

提供设备电源的验证或标识的功能的任何 PIN 应作为 PIN1 报告，并且必须符合 PIN1 指导原则。

微型端口驱动程序必须返回此信息时在设备就绪状态更改为*WwanReadyStateInitialized*或者在设备就绪状态时*WwanReadyStateDeviceLocked* (锁定的 PIN)。 只要有可能，微型端口驱动程序还应在其他设备就绪的状态，返回此信息。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_WWAN\_PIN\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list)

[**NDIS\_STATUS\_WWAN\_PIN\_LIST**](ndis-status-wwan-pin-list.md)

[WWAN 固定操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-pin-operations)

 

 




