---
title: OID_WWAN_SMS_READ
description: OID_WWAN_SMS_READ 读取存储在 MB 设备或订阅服务器标识模块 (SIM 卡) 或任何其他辅助非易失性内存或内存中的短信文本消息。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SMS_READ 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c4b2994d1dc792b387bc6e9d4e0ce1c2c1f39fe0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812905"
---
# <a name="oid_wwan_sms_read"></a>OID \_ WWAN \_ SMS \_ 读取


OID \_ WWAN \_ SMS \_ READ 读取存储在 MB 设备或订阅服务器标识模块 (SIM 卡) 或任何其他辅助非易失性内存或内存的短信。

不支持设置请求。

微型端口驱动程序必须异步处理查询请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，稍后发送 [**ndis \_ 状态 \_ WWAN \_ Sms \_ 接收**](ndis-status-wwan-sms-receive.md) 状态通知，其中包含 [**ndis \_ WWAN \_ sms \_ 读取**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_read) 结构，以提供在完成查询请求时最初由调用方提供的 SMS 消息。

请求读取 SMS 文本消息的调用方提供 NDIS \_ WWAN \_ SMS \_ 读取结构，以指示调用方想要返回的短信消息。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅 [WWAN SMS 操作](./mb-sms-operations.md)。

当处理此 OID 时，微型端口驱动程序可以 (SIM 卡) 访问订阅服务器标识模块，但不应访问提供程序网络。

OID \_ WWAN \_ SMS \_ 读取支持读取 PDU 模式和 CDMA 模式短信，这取决于设备的功能。

微型端口驱动程序可能会收到根据索引读取 SMS 文本消息的请求，或读取所有 SMS 文本消息的请求。 读取请求可能包含任何一种基本筛选器，例如 new (未读) 消息、旧 (读取) 消息、草稿消息或发送消息。

实现 SMS 文本消息功能的微型端口驱动程序必须支持使用 *WwanSmsFlagNew* 的基本筛选器读取新消息。 所有其他筛选器类型都是可选的以支持。

微型端口驱动程序必须在逻辑上跨所有可用的物理不同 SMS 文本消息存储投影单个短信文本消息存储。

如果微型端口驱动程序 \_ 不 \_ \_ 支持短信，则它应返回不受支持的 NDIS 状态。

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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ WWAN \_ SMS \_ 读取**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_read)

[WWAN SMS 操作](./mb-sms-operations.md)

 

