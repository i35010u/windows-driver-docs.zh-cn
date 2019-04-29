---
title: OID_WWAN_SMS_DELETE
description: OID_WWAN_SMS_DELETE 删除存储在 MB 设备或用户识别模块 （SIM 卡），或任何其他辅助的非易失性内存或内存中的 SMS 文本消息。
ms.assetid: b80fae94-35cc-4709-8346-d5a500d3fd49
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SMS_DELETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6d2d971f74bc8996fe7f02e41204eae9f94f26ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387365"
---
# <a name="oidwwansmsdelete"></a>OID\_WWAN\_SMS\_DELETE


OID\_WWAN\_SMS\_删除： 删除存储在 MB 设备或用户识别模块 （SIM 卡），或任何其他辅助的非易失性内存或内存中的 SMS 文本消息。

不支持查询请求。

设置请求使用[ **NDIS\_WWAN\_SMS\_删除**](https://msdn.microsoft.com/library/windows/hardware/ff567938)结构。

微型端口驱动程序以异步方式处理此 OID，并应返回 NDIS\_状态\_指示\_必需临时响应任何集请求。 微型端口驱动程序应发送[ **NDIS\_状态\_WWAN\_SMS\_删除**](ndis-status-wwan-sms-delete.md)指示它们完成事务的时间。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN SMS 操作](https://msdn.microsoft.com/library/windows/hardware/ff559131)。

在处理此 OID 时，微型端口驱动程序可以访问用户识别模块 （SIM 卡），但不是应访问提供程序的网络。

微型端口驱动程序可能会收到请求删除索引，基于短信或删除所有短信。 删除请求可能包含的任何一种基本的筛选器等新的 （未读） 邮件、 旧 （读取） 的消息、 草稿消息或发送的消息。

微型端口驱动程序应返回 NDIS\_状态\_不\_如果它们不支持短信或删除短信的功能支持。

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


[**NDIS\_WWAN\_SMS\_DELETE**](https://msdn.microsoft.com/library/windows/hardware/ff567938)

[WWAN SMS 操作](https://msdn.microsoft.com/library/windows/hardware/ff559131)

 

 




