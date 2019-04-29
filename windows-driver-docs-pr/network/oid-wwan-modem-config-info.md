---
title: OID_WWAN_MODEM_CONFIG_INFO
description: OID_WWAN_MODEM_CONFIG_INFO 检索有关调制解调器配置信息的信息。
ms.assetid: 527B970C-09FC-4E49-A309-44D5C6A39778
ms.date: 08/08/2017
keywords:
- 从 Windows Vista 开始 OID_WWAN_MODEM_CONFIG_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1ee6dbf13c9a69f5a19b50463464ae22e26024df
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353735"
---
# <a name="oidwwanmodemconfiginfo"></a>OID\_WWAN\_调制解调器\_CONFIG\_信息


OID\_WWAN\_调制解调器\_CONFIG\_信息检索有关调制解调器配置信息的信息。

MBB 驱动程序必须处理查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_需要更高版本在发送之前对原始请求[NDIS\_状态\_WWAN\_调制解调器\_CONFIG\_信息](ndis-status-wwan-modem-config-info.md)状态通知包含[ **NDIS\_WWAN\_调制解调器\_配置\_INFO** ](https://msdn.microsoft.com/library/windows/hardware/07C2BAED-157A-459C-B558-115C0091ECE5)结构，其中又包含[ **WWAN\_调制解调器\_配置\_信息**](https://msdn.microsoft.com/library/windows/hardware/14FBFA51-F4A5-417A-8905-241CEA543774)结构，以提供有关调制解调器的配置信息。

不适用集发出的请求。

<a name="remarks"></a>备注
-------

MBB 驱动程序可能不具有有效信息尚未从调制解调器在早期的查询。 无效的信息将设置为零。

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
<td><p>下一步的重大更新到 Windows 10</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[NDIS\_状态\_WWAN\_调制解调器\_配置\_信息](ndis-status-wwan-modem-config-info.md)

[**NDIS\_WWAN\_调制解调器\_CONFIG\_信息**](https://msdn.microsoft.com/library/windows/hardware/07C2BAED-157A-459C-B558-115C0091ECE5)

[**WWAN\_调制解调器\_CONFIG\_信息**](https://msdn.microsoft.com/library/windows/hardware/14FBFA51-F4A5-417A-8905-241CEA543774)



