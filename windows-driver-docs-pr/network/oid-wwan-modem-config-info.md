---
title: OID_WWAN_MODEM_CONFIG_INFO
description: OID_WWAN_MODEM_CONFIG_INFO 检索有关调制解调器配置信息的信息。
ms.assetid: 527B970C-09FC-4E49-A309-44D5C6A39778
ms.date: 08/08/2017
keywords:
- 从 Windows Vista 开始 OID_WWAN_MODEM_CONFIG_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3b9c66bbc96970ca5e80c59cdd07d2e8a16d7b24
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213762"
---
# <a name="oid_wwan_modem_config_info"></a>OID \_ WWAN \_ 调制解调器 \_ 配置 \_ 信息


OID \_ WWAN \_ 调制解调器 \_ 配置信息 \_ 检索有关调制解调器配置信息的信息。

MBB 驱动程序必须异步处理查询请求，最初返回 \_ \_ \_ 原始请求所需的 ndis 状态指示，然后再发送 [ndis \_ 状态 wwan 调制 \_ \_ 解调器 \_ \_ ](ndis-status-wwan-modem-config-info.md) 配置信息（包含 [**ndis \_ wwan \_ 调制 \_ \_ **](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_config_info) 解调器配置信息结构，后者又包含一个 [**wwan \_ 调制 \_ \_ **](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_modem_config_info) 解调器配置信息结构）来提供有关调制解调器配置的信息。

设置请求不适用。

<a name="remarks"></a>备注
-------

在早期查询期间，MBB 驱动程序可能不包含来自调制解调器的有效信息。 无效信息将设置为零。

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
<td><p>Windows 10 的下一个重大更新</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[NDIS \_ 状态 \_ WWAN \_ 调制解调器 \_ 配置 \_ 信息](ndis-status-wwan-modem-config-info.md)

[**NDIS \_ WWAN \_ 调制解调器 \_ 配置 \_ 信息**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_config_info)

[**WWAN \_ 调制解调器 \_ 配置 \_ 信息**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_modem_config_info)