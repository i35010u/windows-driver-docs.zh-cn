---
title: NDIS_STATUS_WWAN_MODEM_CONFIG_INFO
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_MODEM_CONFIG_INFO 通知来通知 MB 服务完成了上一个 OID_WWAN_MODEM_CONFIG_INFO 查询请求。
keywords:
- NDIS_STATUS_WWAN_MODEM_CONFIG_INFO，从 Windows Vista 开始的网络驱动程序
topic_type:
- apiref
api_name:
- NDIS_STATUS_WWAN_MODEM_CONFIG_INFO
api_location:
- ndis.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4c79de695476359a932f60e8caa4552282b29de0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822911"
---
# <a name="ndis_status_wwan_modem_config_info"></a>NDIS_STATUS_WWAN_MODEM_CONFIG_INFO


MBB 驱动程序使用 **NDIS_STATUS_WWAN_MODEM_CONFIG_INFO** 通知来通知 MB 服务完成了上一个 [OID_WWAN_MODEM_CONFIG_INFO](oid-wwan-modem-config-info.md) 查询请求。

MBB 驱动程序必须仅在调制解调器的配置状态发生更改时发送未经请求的 **NDIS_STATUS_WWAN_MODEM_CONFIG_INFO** 。

此通知使用 [**NDIS_WWAN_MODEM_CONFIG_INFO**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_config_info) 结构。

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
<td><p>Windows 10 版本 1709</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID_WWAN_MODEM_CONFIG_INFO](oid-wwan-modem-config-info.md)

[**NDIS_WWAN_MODEM_CONFIG_INFO**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_config_info)
