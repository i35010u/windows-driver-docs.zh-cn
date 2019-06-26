---
title: OID_WWAN_USSD
description: OID_WWAN_USSD 将非结构化补充服务数据 (USSD) 请求发送到基础的 MB 设备。
ms.assetid: 9DFAAABD-8213-4B83-8FE8-1EC2BB9F735B
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_USSD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b22ec43ce164fe35053af42a9b4d3e7e3628458e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385490"
---
# <a name="oidwwanussd"></a>OID\_WWAN\_USSD


OID\_WWAN\_USSD 将非结构化补充服务数据 (USSD) 请求发送到基础的 MB 设备。

不支持查询请求。

微型端口驱动程序必须处理集请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[NDIS\_状态\_WWAN\_USSD](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd)包含初始 USSD 请求的状态，当他们已完成事务的状态通知。

Windows 不会发送一个 OID\_WWAN\_USSD 请求到微型端口驱动程序如果上一个请求仍在进行，但通过设置取消挂起操作的请求除外[WWAN\_USSD\_请求](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_ussd_request) **RequestType**对的请求的成员*WwanUssdRequestCancel*。

取消请求时，微型端口驱动程序必须响应取消的请求并取消请求。

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
<td><p>支持从 Windows 8 开始。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[NDIS\_状态\_WWAN\_USSD](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd)

[WWAN\_USSD\_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_ussd_request)

 

 




