---
title: OID_WWAN_MODEM_CONFIG_INFO
description: OID_WWAN_MODEM_CONFIG_INFO 检索有关调制解调器配置信息的信息。
ms.assetid: 527B970C-09FC-4E49-A309-44D5C6A39778
ms.date: 08/08/2017
keywords:
- 从 Windows Vista 开始 OID_WWAN_MODEM_CONFIG_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9771208aa2f23f2fd8920b8c38521668c1c3e4c6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376757"
---
# <a name="oidwwanmodemconfiginfo"></a>OID\_WWAN\_调制解调器\_CONFIG\_信息


OID\_WWAN\_调制解调器\_CONFIG\_信息检索有关调制解调器配置信息的信息。

MBB 驱动程序必须处理查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_需要更高版本在发送之前对原始请求[NDIS\_状态\_WWAN\_调制解调器\_CONFIG\_信息](ndis-status-wwan-modem-config-info.md)状态通知包含[ **NDIS\_WWAN\_调制解调器\_配置\_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_config_info)结构，其中又包含[ **WWAN\_调制解调器\_配置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_modem_config_info)结构，以提供有关调制解调器的配置信息。

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

[**NDIS\_WWAN\_调制解调器\_CONFIG\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_config_info)

[**WWAN\_调制解调器\_CONFIG\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_modem_config_info)



