---
title: NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED
description: NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED
ms.date: 04/02/2018
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 3031e047fef4256b0c5ad3b914c0002bd9a4048b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801419"
---
# <a name="ndis_status_wdi_indication_cipher_key_updated"></a>NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED

微型端口驱动程序发送这一指示，指示已更新 () 的密码密钥。

仅当驱动程序未通过[OID_WDI_SET_ADD_PM_PROTOCOL_OFFLOAD](oid-wdi-set-add-pm-protocol-offload.md)命令) 中的[WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY](wdi-tlv-pm-protocol-offload-80211rsn-rekey.md)存档来卸载 RSN GTK rekey (时，才会发送此指示。 如果驱动程序当前处于 Rsn GTK Rekey 的卸载状态，则它不应通过此方法指示，应允许在其退出卸载状态时通过 [OID_WDI_GET_PM_PROTOCOL_OFFLOAD](oid-wdi-get-pm-protocol-offload.md) 命令查询更新的密钥信息。

例如，如果驱动程序或固件在 WNM-Sleep 模式响应中收到新的 GTK/iGTK，则该驱动程序将发送此通知。

## <a name="payload-data"></a>负载数据

| 类型 | 允许多个 TLV 实例 | 可选 | 说明 |
| --- | --- | --- | --- |
| [WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS](wdi-tlv-pm-protocol-rsn-offload-keys.md) |   |   | 当前配置的 Rsn Eapol 密钥信息。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10，版本1803

**支持的最低服务器**： Windows server 2016

**标头**： Dot11wdi

