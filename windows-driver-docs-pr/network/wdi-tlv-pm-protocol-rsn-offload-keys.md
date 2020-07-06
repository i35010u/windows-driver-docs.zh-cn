---
title: WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS
description: WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS 是包含当前配置的 Rsn Eapol 密钥信息的 TLV。
ms.assetid: DFF81CBD-1B10-456F-AD8D-1163DD80C981
ms.date: 04/02/2018
keywords:
- 从 Windows Vista 开始 WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a6e2eceea6140f3449bed66b0ae2aa960ffb5ed1
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968308"
---
# <a name="wdi_tlv_pm_protocol_rsn_offload_keys"></a>WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS

WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS 是包含当前配置的 Rsn Eapol 密钥信息的 TLV。 此 TLV 用于[NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED](ndis-status-wdi-indication-cipher-key-updated.md)状态指示。

## <a name="tlv-type"></a>TLV 类型

0x149

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| WDI_RSN_OFFLOAD_KEYS_CONTAINER | 当前配置的 Rsn Eapol 密钥信息。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10，版本1803

**支持的最低服务器**： Windows server 2016

**标头**： Wditypes. hpp

