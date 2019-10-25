---
title: OID_WWAN_SMS_READ
description: OID_WWAN_SMS_READ 读取存储在 MB 设备或订阅服务器标识模块（SIM 卡）或任何其他辅助非易失性内存或内存中的短信消息。
ms.assetid: f4dbb7e8-1348-4fa8-abac-f644a443df48
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SMS_READ 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a3b8fd7c35443f3dc1db96f0753ab5d453bcfe99
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843784"
---
# <a name="oid_wwan_sms_read"></a>OID\_WWAN\_SMS\_读取


OID\_WWAN\_SMS\_读取读取存储在 MB 设备或订阅服务器标识模块（SIM 卡）或任何其他辅助非易失性内存或内存中的 SMS 文本消息。

不支持设置请求。

微型端口驱动程序必须异步处理查询请求，最初返回 NDIS\_状态\_指示\_需要原始请求，稍后将[**ndis\_状态\_WWAN\_SMS 发送\_接收**](ndis-status-wwan-sms-receive.md)状态通知，包含[**NDIS\_WWAN\_SMS\_读取**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_read)结构，以提供在完成查询请求时最初由调用方提供的 sms 消息。

请求读取 SMS 文本消息的调用方提供一个 NDIS\_WWAN\_SMS\_READ 结构，以指示调用方想要返回的短信消息。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN SMS 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)。

当处理此 OID 时，微型端口驱动程序可以访问订阅服务器标识模块（SIM 卡），但不应访问提供程序网络。

OID\_WWAN\_SMS\_READ 支持读取 PDU 模式和 CDMA 模式短信，这取决于设备的功能。

微型端口驱动程序可能会收到根据索引读取 SMS 文本消息的请求，或读取所有 SMS 文本消息的请求。 读取请求可能包含任何一种基本筛选器，例如新的（未读）消息、旧的（读取）消息、草稿消息或发送的消息。

实现 SMS 文本消息功能的微型端口驱动程序必须支持使用*WwanSmsFlagNew*的基本筛选器读取新消息。 所有其他筛选器类型都是可选的以支持。

微型端口驱动程序必须在逻辑上跨所有可用的物理不同 SMS 文本消息存储投影单个短信文本消息存储。

如果不支持短信，微型端口驱动程序应返回 NDIS\_状态\_不\_支持。

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


[**NDIS\_WWAN\_SMS\_读取**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_read)

[WWAN SMS 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)

 

 




