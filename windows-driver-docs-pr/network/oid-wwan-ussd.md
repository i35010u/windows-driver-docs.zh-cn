---
title: OID_WWAN_USSD
description: OID_WWAN_USSD 将非结构化补充服务数据 (USSD) 请求发送到基础 MB 设备。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_USSD 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4050de27049597673c1a790d8fe365c4a4795ded
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825049"
---
# <a name="oid_wwan_ussd"></a>OID \_ WWAN \_ USSD


OID \_ WWAN \_ USSD 将非结构化补充服务数据 (USSD) 请求发送到基础 MB 设备。

不支持查询请求。

微型端口驱动程序必须异步处理设置请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，稍后发送 [NDIS \_ 状态 \_ WWAN \_ USSD](./ndis-status-wwan-ussd.md) 状态通知，其中包含初始 USSD 请求在完成该事务时的状态。

\_ \_ 如果以前的请求仍在进行，则 Windows 不会将 OID WWAN USSD 请求发送到微型端口驱动程序，而是通过将请求的 [WWAN \_ USSD \_ 请求](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_ussd_request) **RequestType** 成员设置为 *WwanUssdRequestCancel* 来取消挂起的操作。

当请求被取消时，微型端口驱动程序必须响应取消的请求和取消请求。

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
<td><p>从 Windows 8 开始支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[NDIS \_ 状态 \_ WWAN \_ USSD](./ndis-status-wwan-ussd.md)

[WWAN \_ USSD \_ 请求](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_ussd_request)

 

