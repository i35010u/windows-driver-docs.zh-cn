---
title: WDI_TLV_SAE_STATUS
description: WDI_TLV_SAE_STATUS 是 TLV，其中包含同时进行身份验证的等于 (SAE) 身份验证失败错误状态。
ms.assetid: 7B6B8D4B-35B4-4AEA-A969-4BB514AB968E
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_STATUS 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: ac6d86e9fcfd81c3ec98da9b331938434845f5d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359034"
---
# <a name="wditlvsaestatus"></a>WDI_TLV_SAE_STATUS

**WDI_TLV_SAE_STATUS**是 TLV，其中包含同时进行身份验证的等于 (SAE) 身份验证失败错误状态。

中的命令参数使用此 TLV [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)和中的有效负载数据[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)。

## <a name="tlv-type"></a>TLV 类型

0x14C

## <a name="length"></a>长度

UINT32 大小 （以字节为单位）。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| [**WDI_SAE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_sae_status) | SAE 身份验证失败错误状态。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
