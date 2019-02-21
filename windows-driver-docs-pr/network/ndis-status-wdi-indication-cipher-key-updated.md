---
title: NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED
description: NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED
ms.assetid: 95AB3325-9AE7-4F10-8E00-88D502E1A5C9
ms.date: 04/02/2018
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c2e2f5abfc24f40b5ee495065ebbc3760d638334
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555975"
---
# <a name="ndisstatuswdiindicationcipherkeyupdated"></a>NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED

微型端口驱动程序发送这种指示，指示已更新密钥的密码。

该驱动程序有不卸载 RSN GTK 重新生成密钥时才发送此指示 (通过[WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY](wdi-tlv-pm-protocol-offload-80211rsn-rekey.md)字段中[OID_WDI_SET_ADD_PM_PROTOCOL_OFFLOAD](oid-wdi-set-add-pm-protocol-offload.md)命令)。 如果该驱动程序目前处于卸载状态的 Rsn GTK 重新生成，则它应表示通过此方法，但应允许更新密钥的信息，以通过查询[OID_WDI_GET_PM_PROTOCOL_OFFLOAD](oid-wdi-get-pm-protocol-offload.md)命令时从卸载状态中。

例如，如果它或固件 WNM 睡眠模式下响应中收到新的 GTK/iGTK 驱动程序将发送此通知。

| 对象 |
| --- |
| 端口 |

## <a name="payload-data"></a>有效负载数据

| 在任务栏的搜索框中键入 | 允许多个 TLV 实例 | 可选 | 描述 |
| --- | --- | --- | --- |
| [WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS](wdi-tlv-pm-protocol-rsn-offload-keys.md) |   |   | 当前配置的 Rsn Eapol 密钥信息。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1803 |
| 最低受支持的服务器 | Windows Server 2016 |
| 标头 | Dot11wdi.h |
