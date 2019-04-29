---
title: OID_WWAN_SMS_READ
description: OID_WWAN_SMS_READ 读取存储在 MB 设备或用户识别模块 （SIM 卡），或任何其他辅助的非易失性内存或内存中的 SMS 文本消息。
ms.assetid: f4dbb7e8-1348-4fa8-abac-f644a443df48
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SMS_READ 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c9df125aa1d4117581d83ba156fb0a7660e8f33d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387362"
---
# <a name="oidwwansmsread"></a>OID\_WWAN\_SMS\_READ


OID\_WWAN\_SMS\_读取读取存储在 MB 设备或用户识别模块 （SIM 卡），或任何其他辅助的非易失性内存或内存中的 SMS 文本消息。

不支持组的请求。

微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_SMS\_接收**](ndis-status-wwan-sms-receive.md)状态通知包含[ **NDIS\_WWAN\_SMS\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff567941)结构提供的短信请求时完成查询请求最初由调用方中提供。

调用方请求读取 SMS 文本消息提供 NDIS\_WWAN\_SMS\_读取结构，以指示哪些短信调用方想要返回的微型端口。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN SMS 操作](https://msdn.microsoft.com/library/windows/hardware/ff559131)。

在处理此 OID 时，微型端口驱动程序可以访问用户识别模块 （SIM 卡），但不是应访问提供程序网络。

OID\_WWAN\_SMS\_读取支持读取 PDU 模式和 CDMA 模式 SMS 文本消息，具体取决于设备的功能。

微型端口驱动程序可能会收到请求读取基于索引，短信或读取所有短信。 读取请求可能包含的任何一种基本的筛选器等新的 （未读） 邮件、 旧 （读取） 的消息、 草稿消息或发送的消息。

实现 SMS 文本消息功能的微型端口驱动程序必须支持使用的基本筛选器的新消息的读取*WwanSmsFlagNew*。 所有其他筛选器类型是可选的支持。

微型端口驱动程序必须以逻辑方式跨所有可用物理不同的 SMS 文本消息存储项目的单个 SMS 文本消息存储区。

微型端口驱动程序应返回 NDIS\_状态\_不\_如果它们不支持短信支持。

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


[**NDIS\_WWAN\_SMS\_READ**](https://msdn.microsoft.com/library/windows/hardware/ff567941)

[WWAN SMS 操作](https://msdn.microsoft.com/library/windows/hardware/ff559131)

 

 




