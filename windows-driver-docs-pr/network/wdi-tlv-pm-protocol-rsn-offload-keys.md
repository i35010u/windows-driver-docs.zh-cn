---
title: WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS
description: WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS 是 TLV，其中包含当前配置的 Rsn Eapol 密钥信息。
ms.assetid: DFF81CBD-1B10-456F-AD8D-1163DD80C981
ms.date: 04/02/2018
keywords:
- 从 Windows Vista 开始 WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 72a812bd7b11c7f1118ec14a7f2a934ba0c09b56
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380693"
---
# <a name="wditlvpmprotocolrsnoffloadkeys"></a>WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS

WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS 是 TLV，其中包含当前配置的 Rsn Eapol 密钥信息。 在中使用此 TLV [NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED](ndis-status-wdi-indication-cipher-key-updated.md)状态指示。

## <a name="tlv-type"></a>TLV 类型

0x149

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| WDI_RSN_OFFLOAD_KEYS_CONTAINER | 当前配置的 Rsn Eapol 密钥信息。 |

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1803 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
