---
title: NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED
description: NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED
ms.assetid: 95AB3325-9AE7-4F10-8E00-88D502E1A5C9
ms.date: 04/02/2018
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 371bba94d65b738b4062cacab775fc2648783913
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968058"
---
# <a name="ndis_status_wdi_indication_cipher_key_updated"></a>NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED

微型端口驱动程序发送这一指示，指示已更新密码密钥。

仅当驱动程序未卸载 RSN GTK rekey （通过在[OID_WDI_SET_ADD_PM_PROTOCOL_OFFLOAD](oid-wdi-set-add-pm-protocol-offload.md)命令中存档[WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY](wdi-tlv-pm-protocol-offload-80211rsn-rekey.md) ）时，才会发送此指示。 如果驱动程序当前处于 Rsn GTK Rekey 的卸载状态，则它不应通过此方法指示，应允许在其退出卸载状态时通过[OID_WDI_GET_PM_PROTOCOL_OFFLOAD](oid-wdi-get-pm-protocol-offload.md)命令查询更新的密钥信息。

例如，如果驱动程序或固件在 WNM-睡眠模式响应中收到新的 GTK/iGTK，则该驱动程序将发送此通知。

## <a name="payload-data"></a>负载数据

| 类型 | 允许多个 TLV 实例 | 可选 | 说明 |
| --- | --- | --- | --- |
| [WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS](wdi-tlv-pm-protocol-rsn-offload-keys.md) |   |   | 当前配置的 Rsn Eapol 密钥信息。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10，版本1803

**支持的最低服务器**： Windows server 2016

**标头**： Dot11wdi

