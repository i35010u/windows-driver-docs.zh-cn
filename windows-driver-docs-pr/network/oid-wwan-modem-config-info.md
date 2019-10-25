---
title: OID_WWAN_MODEM_CONFIG_INFO
description: OID_WWAN_MODEM_CONFIG_INFO 检索有关调制解调器配置信息的信息。
ms.assetid: 527B970C-09FC-4E49-A309-44D5C6A39778
ms.date: 08/08/2017
keywords:
- OID_WWAN_MODEM_CONFIG_INFO 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f5551743122d0393efc0d8ce3f9c6e6857e0c074
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843835"
---
# <a name="oid_wwan_modem_config_info"></a>OID\_WWAN\_调制解调器\_CONFIG\_信息


OID\_WWAN\_调制解调器\_CONFIG\_信息检索有关调制解调器配置信息的信息。

MBB 驱动程序必须异步处理查询请求，最初返回 NDIS\_状态\_指示\_需要请求原始请求，然后再发送[ndis\_状态\_WWAN\_调制解调器\_配置\_信息](ndis-status-wwan-modem-config-info.md)状态通知，其中包含一个[**NDIS\_wwan\_调制解调器\_配置\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_config_info)结构，后者又包含一个[**wwan\_调制解调器\_配置\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_modem_config_info)结构，用于提供有关调制解调器配置的信息。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[NDIS\_状态\_WWAN\_调制解调器\_配置\_信息](ndis-status-wwan-modem-config-info.md)

[**NDIS\_WWAN\_调制解调器\_配置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_config_info)

[**WWAN\_调制解调器\_CONFIG\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_modem_config_info)



