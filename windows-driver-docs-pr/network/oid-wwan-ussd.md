---
title: OID_WWAN_USSD
description: OID_WWAN_USSD 将非结构化补充服务数据 (USSD) 请求发送到基础的 MB 设备。
ms.assetid: 9DFAAABD-8213-4B83-8FE8-1EC2BB9F735B
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_USSD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7ac8ac570b99b641aa3b3833fc1a528eeae97a5f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383180"
---
# <a name="oidwwanussd"></a>OID\_WWAN\_USSD


OID\_WWAN\_USSD 将非结构化补充服务数据 (USSD) 请求发送到基础的 MB 设备。

不支持查询请求。

微型端口驱动程序必须处理集请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[NDIS\_状态\_WWAN\_USSD](https://msdn.microsoft.com/library/windows/hardware/hh439822)包含初始 USSD 请求的状态，当他们已完成事务的状态通知。

Windows 不会发送一个 OID\_WWAN\_USSD 请求到微型端口驱动程序如果上一个请求仍在进行，但通过设置取消挂起操作的请求除外[WWAN\_USSD\_请求](https://msdn.microsoft.com/library/windows/hardware/hh464138) **RequestType**对的请求的成员*WwanUssdRequestCancel*。

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


[NDIS\_状态\_WWAN\_USSD](https://msdn.microsoft.com/library/windows/hardware/hh439822)

[WWAN\_USSD\_REQUEST](https://msdn.microsoft.com/library/windows/hardware/hh464138)

 

 




